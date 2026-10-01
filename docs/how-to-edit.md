# How to edit this wiki

Every page is a Markdown file in the `docs/` folder of the
[GitHub repository](https://github.com/eml-gatech/lab-wiki). When a change lands
on the `main` branch, the site rebuilds and updates within a couple of minutes.

## Quick edit from the browser

1. Open the page you want to change on this site.
2. Click the **pencil icon** :material-file-edit-outline: at the top right of
   the page. This opens the file in GitHub's editor.
3. Make your changes. Use the **Preview** tab to check formatting.
4. Click **Commit changes…**, write a short description (e.g. *"Update XRD
   shutdown steps"*), and either:
    - **Commit directly to `main`** for small fixes (if you have permission), or
    - **Create a new branch and start a pull request** if you'd like someone to
      review it first.
5. Check the **Actions** tab on GitHub: a green check means the site rebuilt
   successfully.

!!! tip
    If the build fails (red ✗), click into the run to see the error. The most
    common cause is a link to a page that doesn't exist or was renamed.

## Adding a new page

1. In GitHub, open the folder you want (e.g. `docs/equipment-tutorials/`) and
   click **Add file → Create new file**.
2. Name it with lowercase letters and hyphens, ending in `.md`
   (e.g. `uv-vis.md`).
3. Start the file with a title line: `# UV-Vis spectrometer`.
4. Open `mkdocs.yml` in the repository root and add the page to the `nav:`
   section, indented under the right tab:

    ```yaml
    - Equipment tutorials:
        - equipment-tutorials/index.md
        - Evaporator: equipment-tutorials/evaporator.md
        - UV-Vis: equipment-tutorials/uv-vis.md   # new line
    ```

    Indentation matters in this file: use spaces, not tabs, and line the new
    entry up with its neighbors.

For new instruments, start from `templates/equipment-tutorial-template.md` in
the repository.

## Adding images

Upload the image to `docs/assets/images/` (**Add file → Upload files**), then
reference it from a page. The path is relative to the page's own location:

```markdown
![Evaporator front panel](../assets/images/evaporator-panel.jpg)
```

Resize photos to under ~1 MB before uploading.

## Formatting cheat sheet

### Basics

```markdown
## Section heading
### Subsection heading

**bold**, *italic*, `inline code`

- bullet list
1. numbered list

[Link to another page](../meeting-schedule.md)
[External link](https://example.com)
```

### Tables

```markdown
| Instrument | Owner |
| ---------- | ----- |
| XRD        | Alex  |
```

### Callout boxes

```markdown
!!! warning "Laser on"
    Wear goggles before opening the shutter.
```

!!! warning "Laser on"
    Wear goggles before opening the shutter.

Other types: `note`, `tip`, `info`, `danger`, `success`, `question`,
`failure`, `abstract`. Use `???` instead of `!!!` to make the box collapsed by
default.

### Checklists

```markdown
- [x] Chamber vented
- [ ] Samples loaded
```

- [x] Chamber vented
- [ ] Samples loaded

### Tabs

```markdown
=== "Steady-state"

    Content for the first tab.

=== "Time-resolved"

    Content for the second tab.
```

=== "Steady-state"

    Content for the first tab.

=== "Time-resolved"

    Content for the second tab.

### Equations

```markdown
Inline: $E = h\nu$

Display:

$$
n\lambda = 2d\sin\theta
$$
```

Inline: $E = h\nu$

### Keyboard keys

```markdown
Press ++ctrl+s++ to save the scan.
```

Press ++ctrl+s++ to save the scan.

The full syntax reference is in the
[Material for MkDocs documentation](https://squidfunk.github.io/mkdocs-material/reference/).
