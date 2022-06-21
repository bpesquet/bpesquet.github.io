# bpesquet.github.io

My [Hugo](https://gohugo.io)-powered personal website.

Current theme: [Anubis](https://github.com/mitrichius/hugo-theme-anubis).

Deployed to [GitHub Pages](https://www.bpesquet.fr) via [Hugo Setup Action](https://github.com/peaceiris/actions-hugo).

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
