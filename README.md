# bpesquet.github.io

My [Hugo](https://gohugo.io)-powered personal website.

Current theme: [Anubis](https://github.com/mitrichius/hugo-theme-anubis).

Published to [www.bpesquet.fr](https://www.bpesquet.fr) on [GitHub Pages](https://pages.github.com/) via [Hugo Setup Action](https://github.com/peaceiris/actions-hugo).

## Development notes

### Testing the site locally

```bash
hugo server -D
```

### Generating a PDF version of slides

Use [pandoc](https://pandoc.org/) in the Markdown source file directory (`content/slides/<title>`):

```bash
pandoc index.md -o <PDF file name>.pdf --toc
```

Fix image sizes in PDF output with the following syntax (which doesn't work well in slideshow mode):

```md
 ![large image](landscape.jpg){width=1024 height=768}
 ```
