# xva-docs
This is Markdown repository for the [Xva documentation](https://docs.xva-lang.org).

## Contributing
The Xva documentation is an [mdBook](https://rust-lang.github.io/mdBook/) repository. mdBook itself is a Cargo utility. 

### Building
Prerequesites:
- [Rust](https://rustup.rs/)
- mdbook
    - To install mdbook, run `cargo install mdbook`.

### Previewing changes
mdBook has a small server built in that you can use to preview your changes before they are deployed to the docs site:

```bash
mdbook serve
```

You can also run mdBook in watch mode, to have hot reloading capabilities while working on your changes:

```bash
mdbook watch
```





## Contents
1. [Getting started](1-getting_started/getting_started.md)
    1. Hello, world!
2. [Basic concepts](2-basic_concepts/basic_concepts.md)
    1. [Variables](2-basic_concepts/variables.md)
    2. Data types
