# Contributing to the DAF-seq Guide

Thanks for helping improve this documentation! There are two ways to contribute.

## Quick edits (no setup required)

Every page has an edit button (<i class="fa fa-edit"></i>) in the top right corner. Clicking it opens the file in GitHub's web editor where you can make changes and submit a pull request directly from your browser.

## Larger changes (local development)

### Prerequisites

Install [mdBook](https://rust-lang.github.io/mdBook/guide/installation.html):

```bash
# With cargo
cargo install mdbook

# Or download a prebuilt binary from
# https://github.com/rust-lang/mdbook/releases
```

### Setup

```bash
git clone https://github.com/fiberseq/dafseq.github.io.git
cd dafseq.github.io
```

### Preview locally

```bash
mdbook serve --open
```

This starts a local server at `http://localhost:3000` with live reload. Any changes you make to files in `src/` will automatically rebuild and refresh in your browser.

### Build

```bash
mdbook build
```

The static site is generated in the `book/` directory.

### Project structure

```
src/
  SUMMARY.md          # Sidebar navigation (edit this to add/reorder pages)
  README.md           # Home page
  glossary.md         # Glossary of key terms
  cite.md             # Citation and BibTeX
  protocol/
    protocol.md       # Wet lab protocol
    primer-design.md  # Primer design guidelines
    protein-purification.md  # Protein purification protocols
  drylab/
    daf-qc.md         # DAF-QC pipeline documentation
book.toml             # mdBook configuration
```

### Adding a new page

1. Create a new `.md` file in the appropriate directory under `src/`.
2. Add an entry for it in `src/SUMMARY.md` (this controls the sidebar navigation).
3. Preview with `mdbook serve` to verify it renders correctly.

### Submitting changes

1. Create a branch for your changes.
2. Make your edits and verify locally with `mdbook serve`.
3. Open a pull request. The site will automatically deploy when changes are merged to `main`.
