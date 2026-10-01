# Lab Wiki

Source for the group wiki, built with [MkDocs](https://www.mkdocs.org/) and the
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme, and
published with GitHub Pages.

**Live site:** https://eml-gatech.github.io/lab-wiki/

- Lab members who just want to edit pages: read
  [`docs/how-to-edit.md`](docs/how-to-edit.md) (also on the site as *How to edit*).
- This README is for whoever sets up and maintains the wiki.

---

## Contents

1. [How it works](#1-how-it-works)
2. [Repository layout](#2-repository-layout)
3. [One-time setup](#3-one-time-setup)
4. [Previewing changes on your own computer](#4-previewing-changes-on-your-own-computer)
5. [Changing the structure: pages and tabs](#5-changing-the-structure-pages-and-tabs)
6. [Customizing the look](#6-customizing-the-look)
7. [Optional add-ons](#7-optional-add-ons)
8. [Privacy](#8-privacy)
9. [Long-term maintenance and the Zensical transition](#9-long-term-maintenance-and-the-zensical-transition)
10. [Troubleshooting](#10-troubleshooting)

---

## 1. How it works

```
 docs/*.md  +  mkdocs.yml          ← what people edit (plain text in Git)
        │
        │  push / merge to main
        ▼
 GitHub Actions (.github/workflows/deploy.yml)
   pip install -r requirements.txt
   mkdocs build --strict            ← turns Markdown into a static HTML site
        │
        ▼
 GitHub Pages                       ← serves the site at YOUR-ORG.github.io/lab-wiki
```

- Every page is a Markdown (`.md`) file under `docs/`.
- `mkdocs.yml` holds the site settings and the navigation (which pages appear
  in which tab, in what order).
- Each push to `main` triggers a GitHub Actions run that builds and publishes
  the site. Pull requests are built but not published, so errors show up as a
  failed check before merging.
- `--strict` makes the build fail on warnings such as links to pages that
  don't exist. This catches mistakes early.

## 2. Repository layout

```
lab-wiki/
├── .github/workflows/deploy.yml     # build + deploy pipeline
├── docs/                            # everything in here becomes the website
│   ├── index.md                     # landing page (Home tab)
│   ├── how-to-edit.md               # editing guide for lab members
│   ├── meeting-schedule.md          # Meeting schedule tab
│   ├── group-organization/          # Group organization tab
│   │   ├── index.md                 #   section overview page
│   │   ├── group-tasks.md
│   │   ├── mentors.md
│   │   └── equipment-owners.md
│   ├── equipment-tutorials/         # Equipment tutorials tab
│   │   ├── index.md                 #   section overview page
│   │   ├── evaporator.md
│   │   ├── pl-setup.md
│   │   └── xrd.md
│   ├── assets/images/               # images and favicon
│   ├── javascripts/mathjax.js       # equation rendering config
│   └── stylesheets/extra.css        # small style tweaks
├── templates/
│   └── equipment-tutorial-template.md   # starting point for new instruments
├── mkdocs.yml                       # site config + navigation
├── requirements.txt                 # pinned build dependencies
└── .gitignore
```

`templates/` is outside `docs/`, so nothing in it is published.

## 3. One-time setup

### 3.1 Create a GitHub organization (recommended)

An organization (e.g. `smith-lab`) owns the repo instead of one person's
account, so the wiki survives people graduating.

GitHub → your avatar → **Your organizations** → **New organization** → *Free*
plan.

If you skip this, use your own username wherever this README says `YOUR-ORG`.

### 3.2 Create the repository

GitHub → **New repository**:

- **Owner:** the organization
- **Name:** `lab-wiki` (or anything; just be consistent)
- **Visibility:** *Public* (see [Privacy](#8-privacy) before choosing *Private*)
- Leave **"Add a README"**, **.gitignore**, and **license** unchecked. The
  repo must be empty so the first push doesn't conflict.

### 3.3 Fill in the placeholders

Search the project for `YOUR-ORG` and replace it with your organization name
(and `lab-wiki` with your repo name if different). It appears in:

- `mkdocs.yml` (`site_url`, `repo_url`, `repo_name`)
- `docs/how-to-edit.md`
- `README.md`

Also change `site_name` in `mkdocs.yml` (e.g. `Smith Lab Wiki`).

If your default branch is not `main`, change `edit_uri: edit/main/docs/` in
`mkdocs.yml` and `branches: [main]` in the workflow.

### 3.4 Upload the files

**Option A: Git on the command line (recommended)**

```bash
cd lab-wiki
git init -b main
git add .
git commit -m "Initial wiki"
git remote add origin https://github.com/YOUR-ORG/lab-wiki.git
git push -u origin main
```

If Git asks for a password, use a
[personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
or sign in through [GitHub Desktop](https://desktop.github.com/) /
the [GitHub CLI](https://cli.github.com/) (`gh auth login`).

**Option B: GitHub website only**

1. On the empty repo page, click **uploading an existing file**.
2. Drag in the *contents* of the `lab-wiki` folder (not the folder itself).
3. Commit.
4. Check that `.github/workflows/deploy.yml` arrived. Folders starting with a
   dot are hidden by default on macOS and Windows and are often skipped
   when dragging. If it's missing: **Add file → Create new file**, type
   `.github/workflows/deploy.yml` as the name (the slashes create the
   folders), paste the file's contents, and commit.

### 3.5 Turn on GitHub Pages

Repo → **Settings → Pages → Build and deployment → Source: GitHub Actions**.

That's the only setting needed. There's no `gh-pages` branch with this setup.

### 3.6 Run the first deploy

1. Go to the **Actions** tab. The push in step 3.4 already started a run
   (*Build and deploy wiki*).
2. If that run failed at the **deploy** job, it's because Pages wasn't turned
   on yet. Open the run and click **Re-run all jobs**, or use **Run workflow**
   on the workflow's page.
3. When both jobs are green, the deploy job shows the site URL. It's also on
   **Settings → Pages**.

The first deploy can take a few minutes to go live. After that, each change
takes about 1–2 minutes.

### 3.7 Give lab members edit access

Organization → **Teams → New team** (e.g. `members`) → add people → in the
team's **Repositories** tab, add `lab-wiki` with the **Write** role.

People need a free GitHub account first. Invite them by username or email from
**Organization → People → Invite member**.

### 3.8 Optional: require review before changes go live

If you want a second pair of eyes on edits:

Repo → **Settings → Rules → Rulesets → New branch ruleset** (older UI:
**Settings → Branches → Add rule**) → target `main` → enable **Require a pull request before merging** and **Require
status checks to pass** (select the `build` check).

With this on, the pencil icon still works, but GitHub will ask the editor to
open a pull request. For a small group, leaving this off and relying on the
strict build plus Git history (every change is revertible) is usually fine.

## 4. Previewing changes on your own computer

Not required for editing (the GitHub web editor is enough), but handy for
bigger changes. Needs Python 3.10 or newer (3.8+ works for MkDocs itself;
Zensical needs 3.10+).

```bash
cd lab-wiki
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

mkdocs serve
```

Open http://127.0.0.1:8000. The page reloads automatically each time you save
a file.

Before pushing, you can run the same check as CI:

```bash
mkdocs build --strict
```

You'll see a red banner from Material for MkDocs about MkDocs 2.0. It's
informational; `requirements.txt` pins MkDocs 1.6.1, so it doesn't affect this
site. Set `NO_MKDOCS_2_WARNING=true` in your shell to hide it (the workflow
already does).

## 5. Changing the structure: pages and tabs

All navigation lives in the `nav:` block of `mkdocs.yml`:

```yaml
nav:
  - Home: index.md
  - Group organization:                         # a tab with sub-pages
      - group-organization/index.md             # overview page (no title needed)
      - Group tasks: group-organization/group-tasks.md
  - Meeting schedule: meeting-schedule.md       # a tab that is a single page
```

- **Top-level entries become tabs** (`navigation.tabs` feature).
- **Nested entries become sub-pages** in that tab's left sidebar.
- An **`index.md` listed first** inside a section becomes the page you land on
  when clicking the tab (`navigation.indexes` feature). Remove it and the tab
  goes straight to the first sub-page.
- Order in `nav:` = order on the site.

**Add a page:** create the `.md` file under `docs/`, then add a line in `nav:`.

**Add a tab:** add a new top-level entry. Make a folder under `docs/` if it
will have sub-pages.

**Rename or move a page:** update its `nav:` entry and any links to it. The
strict build lists every broken link, so run it (or push and check Actions)
after renaming.

**Pages not listed in `nav:`** still get built and can be linked to (like
`how-to-edit.md`), but they don't appear in the tabs. MkDocs prints an `INFO`
line about them; that doesn't fail the build.

YAML is indentation-sensitive: spaces only, and keep sibling entries aligned.

## 6. Customizing the look

Everything below goes in `mkdocs.yml` under `theme:`.

**Colors.** Change `primary` and `accent` in both palette entries. Named
options include `red`, `pink`, `purple`, `deep purple`, `indigo`, `blue`,
`light blue`, `cyan`, `teal`, `green`, `light green`, `lime`, `yellow`,
`amber`, `orange`, `deep orange`, `brown`, `grey`, `blue grey`, `black`,
`white`. For exact brand colors, see
[custom colors](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/#custom-colors).

**Logo.** Use any bundled icon:

```yaml
  icon:
    logo: material/flask-outline       # browse: https://pictogrammers.com/library/mdi/
```

or an image file:

```yaml
  logo: assets/images/lab-logo.png
```

**Favicon.** Replace `docs/assets/images/favicon.svg` (or point `favicon:` at
a PNG).

**Tabs behavior.** Remove `navigation.tabs.sticky` if you'd rather the tab
bar scroll away. Remove `navigation.tabs` to put everything in the left
sidebar instead.

**Extra CSS.** Small tweaks go in `docs/stylesheets/extra.css`.

Full reference: https://squidfunk.github.io/mkdocs-material/setup/

## 7. Optional add-ons

### "Last updated" date on each page

Useful for spotting stale tutorials.

1. Add to `requirements.txt`:

    ```
    mkdocs-git-revision-date-localized-plugin
    ```

2. Add under `plugins:` in `mkdocs.yml`:

    ```yaml
    plugins:
      - search
      - git-revision-date-localized:
          type: date
          fallback_to_build_date: true
    ```

3. In `.github/workflows/deploy.yml`, give checkout the full history so dates
   are correct:

    ```yaml
          - uses: actions/checkout@v7
            with:
              fetch-depth: 0
    ```

Check Zensical's [plugin support list](https://zensical.org/compatibility/plugins/)
before relying on third-party plugins if you plan to switch (see section 9).

### Custom domain

If your department gives you a subdomain (e.g. `wiki.smithlab.edu`): Repo →
**Settings → Pages → Custom domain**, set the DNS record your IT office
specifies, and update `site_url` in `mkdocs.yml`.

## 8. Privacy

**The published site is public.** GitHub Pages sites can be read by anyone
with the URL, even when the repository is private. Restricting who can view a
Pages site requires GitHub Enterprise Cloud.

Also, publishing Pages from a *private* repo requires a paid GitHub plan.
Academic groups can usually get GitHub Team for free through
[GitHub Education](https://github.com/education); the site itself will still
be public.

Keep off the wiki: passwords, door codes, personal contact details,
unpublished data, and anything export-controlled. Link to a private shared
drive for those instead.

If the whole wiki needs to be private, options are (a) skip Pages and read the
Markdown directly in a private repo on GitHub (it renders fine, without the
tabs and search), or (b) self-host the built site behind your institution's
login.

## 9. Long-term maintenance and the Zensical transition

**Status as of October 2026.** The Material for MkDocs team put the theme in
maintenance mode in November 2025 and scheduled its end of life for
**5 November 2026**. Development moved to
[Zensical](https://zensical.org/), a new static site generator from the same
team that reads the same `mkdocs.yml`. Separately, upstream MkDocs 2.0 is a
rewrite that is incompatible with Material and its plugins.

**What this means here.**

- `requirements.txt` pins `mkdocs==1.6.1` and `mkdocs-material==9.7.7`. The
  site will keep building exactly as it does now. "End of life" means no
  more fixes, not that the package stops working.
- The output is static HTML, so there's no server-side software to patch.
- The main long-term risk is that an old pinned package eventually stops
  installing on a much newer Python. The workflow pins Python 3.12 to delay
  that.

**Switching to Zensical.** This project builds cleanly with Zensical 0.0.67
(`zensical build --strict`, no config changes). When you're ready, or if the
MkDocs build ever breaks:

1. Replace the contents of `requirements.txt` with:

    ```
    zensical
    ```

    (pin a version once you've confirmed it works, e.g. `zensical==0.0.67`)

2. In `.github/workflows/deploy.yml`, change the build step to:

    ```yaml
          - name: Build site
            run: zensical build --strict
    ```

3. Locally, `zensical serve` replaces `mkdocs serve`.

Keep `mkdocs.yml` as is. Zensical reads it directly, and the
`variant: classic` line already in it keeps the current appearance (Zensical
otherwise defaults to its newer "modern" look). Zensical is still pre-1.0,
so check its [compatibility notes](https://zensical.org/compatibility/) before
adding plugins.

## 10. Troubleshooting

| Symptom | Likely cause | Fix |
| ------- | ------------ | --- |
| Deploy job fails with a *"Not Found"* error or a message that Pages isn't enabled | Pages not enabled, or source not set to GitHub Actions | Section 3.5, then **Re-run all jobs** |
| Deploy job fails: *"Branch … is not allowed to deploy to github-pages"* | Default branch isn't `main`, or environment rule | **Settings → Environments → github-pages → Deployment branches**: allow your branch |
| Build fails with a `WARNING` about a link | Link to a page that was renamed, moved, or misspelled | The log names the file and the bad link; fix the path (relative to the page) |
| Build fails with a YAML error | Indentation in `mkdocs.yml` | Use spaces only; align entries with their siblings |
| Site shows 404 | First deploy still propagating, or wrong URL | Wait a few minutes; check the URL on **Settings → Pages** |
| Pencil icon opens a GitHub 404 | `repo_url` / `edit_uri` placeholders not replaced, or branch isn't `main` | Section 3.3 |
| Changes merged but site looks the same | Run still in progress, or browser cache | Check the Actions tab; hard-refresh (Ctrl/Cmd+Shift+R) |
| Equations show as raw `\[ … \]` | MathJax script blocked (some networks block CDNs) | Try another network; the site loads MathJax from unpkg.com |
| Workflow file never ran | `.github/` folder wasn't uploaded | Section 3.4, Option B, step 4 |
