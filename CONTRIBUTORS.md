# Contributors

## Environment

To edit, preview, and render documents, you need the following prerequisites:

- [Quarto 1.8.25 or newer](https://quarto.org/docs/download/)
- An editor such as [RStudio 2025.09.2 or newer](https://posit.co/download/rstudio-desktop/), [Positron](https://positron.posit.co/), or [VS Code](https://code.visualstudio.com/)
- The R packages used by the documents you author/edit

## Quick start

- Fork/Clone the repository
- Install Quarto
- Preview: `quarto preview`
- Render: `quarto render`
- Commit changes in source and `_freeze` folder and send a pull request
- Rendered folder `docs` is not committed

## Adding or Modifying Topics

- Fork/Clone the repository
- If your topic doesn't exist, create a branch from `main` branch and add your topic
- Keep the topic name simple, preferably one word
- To add a **topic**, create
  - **slides/topic/index.qmd**
  - **labs/topic/index.qmd**
  - Add an **assets** folder with a featured image named `featured.png` with dimensions 800x600px
  - The YAML metadata should minimally look like this for labs:

    ```         
    ---
    title: "Topic"
    author: "Author"
    description: "This topic covers this and that."
    image: "assets/featured.png"
    format: html
    ---
    ```

- `format` must be `html` for reports and `revealjs` for presentations
- The YAML metadata should minimally look like this for slides:

    ```         
    ---
    title: "Topic"
    author: "Author"
    description: "This topic covers this and that."
    image: "assets/featured.png"
    format: revealjs
    ---
    ```

- For assets relating to the document (figures, files etc), add them to the **assets** folder
  - **slides/topic/assets/**
  - **labs/topic/assets/**

> [!TIP]
> The document can be live previewed to view changes. Preview is also automatically updated on saving the document. Preview will attempt to render the whole website. If freeze was used correctly, everything should work just fine.

- To preview, run in terminal
  - `quarto preview`
  - Saving the file updates the preview

- To render, run in terminal
  - `quarto render`
  - Rendered files are written to **/docs**
  - To view in browser, open
    - **docs/slides/topic/index.html**
    - **docs/labs/topic/index.html**

> [!IMPORTANT]
> Rendered documents in **docs/** are only for local preview and are excluded from git. The HTML files for the website are rendered by GitHub Actions. Make sure to commit the **_freeze/** folder. We use freeze to cache chunks so rendering works without the original environment (R, packages etc) on GitHub Actions.

- Finally commit changes (`docs` is not committed)

```
git status
git add slides/topic-name labs/topic-name _freeze/slides/topic-name _freeze/labs/topic-name
git commit -m "Added topic-name"
```

- Pull latest changes from the repo or from main branch to your branch
- Resolve conflicts as needed
- Push your changes to your fork or branch and send a pull request like one of the options below

```
nbisweden/raukr-2027:main <- nbisweden/raukr-2027:your-branch (preferred)
nbisweden/raukr-2027:main <- your-fork/raukr-2027:main
nbisweden/raukr-2027:main <- your-fork/raukr-2027:your-branch
```

- Documents can be excluded from project-wide rendering through the `project.render` setting in `_quarto.yml`.

## Updating schedule

- Update **schedule.tsv**
- Then re-render **home_schedule.qmd** and push the contents of *_freeze/home_schedule*

## Tips & Conventions

- Be selective about packages used. Drop packages and dependencies that are not crucial
- Opt for packages with fewer dependencies
- For compute-heavy steps, use freeze, caching, or saved intermediate results
- Be mindful of the size of files
  - Store large data files elsewhere (dropbox, google drive etc) and link them
  - If you have images that are more than a few hundred KB in size, scale them down to under 2000px and [compress](https://compressjpeg.com/) them and/or use more efficient formats like webp
- Use simple topic labels and do not make them needlessly complex
- Preview and render `.qmd` files from their intended project location so they inherit the repository configuration
- Declare all R packages at the beginning of every qmd document
- Set `format: html` for labs and `format: revealjs` for slides
- The default `execute` settings in `_quarto.yml` apply to all documents. Override them in a document's YAML metadata only when needed:

  ```
  execute:
    eval: true
    echo: false
  ```

- Use level 2 heading (##) as the highest level heading
- Use `-` for bullet points
- Define code-cell options with `#|`, for example `#| echo: true`
- Set image dimensions with attributes, for example `![Caption](path/to/image.jpg){width="50%"}`
- Define fenced divs with `:::` and classes with `{.class}`
  - Example of a class on a div

  ```
  ::: {.callout-note}
  content
  :::
  ```
  - Example of a class on a span `[Content]{.class}`
- Columns are defined as such

  ```
  :::: {.columns}
  ::: {.column width="50%"}
  Contents
  :::
  ::: {.column width="50%"}
  Contents
  :::
  ::::
  ```

- Spell-check documents using US English (`en-US`)

- To view a demo report, click [here](https://nbisweden.github.io/raukr-2027/labs/demo/)

### Reveal.js (Slides)

These notes describe differences from xaringan, which RaukR used previously.

- Start slides with level 2 headings (`##`). Quarto also supports `---` as an explicit slide break.
- Use `. . .` for a manual incremental pause
- Define presenter notes as follows:

  ```
  :::{.notes}
  content
  :::
  ```

- For small notes at the bottom of a slide, use:

  ```
  ::: {.aside}
  Contents
  :::
  ```

- To view a demo presentation, click [here](https://nbisweden.github.io/raukr-2027/slides/demo/)

## Quarto extensions

Quarto extensions in use:

```bash
# landing page visual effects
quarto add royfrancis/particles
# interactive schedule
quarto add royfrancis/toastui
# interactive map
quarto add royfrancis/leaflet
# fontawesome icons
quarto add quarto-ext/fontawesome
# collapsible output in code chunks
quarto add mcanouil/quarto-collapse-output
# accordion layout
quarto add royfrancis/quarto-accordion
# top logos in revealjs slides
quarto add royfrancis/quarto-revealjs-header
# pointer in slides
quarto add royfrancis/quarto-revealjs-pointer
# shinylive
quarto add quarto-ext/shinylive
```
