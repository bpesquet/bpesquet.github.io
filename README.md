# bpesquet.github.io

My [Hugo](https://gohugo.io)-powered website.

Current theme: [Anubis](https://github.com/mitrichius/hugo-theme-anubis).

Deployed to [GitHub Pages](https://bpesquet.github.io) via [Hugo Setup Action](https://github.com/peaceiris/actions-hugo).

## Development notes

### Generating a PDF version of slides

Use [pandoc](https://pandoc.org/) in the Markdown source file directory (`content/slides/<title>`):

```bash
pandoc index.md -o <PDF file name>.pdf --toc
```
