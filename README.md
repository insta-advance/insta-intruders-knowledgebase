# Insta Intruders knowledgebase

The Insta Intruders knowledgebase is a repository for information about penetration testing. It has information about common attacks and recommended tooling to be used for these.

The knowledgebase is available for reading publicly on [GitHub Pages](https://insta-advance.github.io/insta-intruders-knowledgebase/).

## Contributing

If you have any suggestions about what should be added to the knowledgebase, open an issue! You can also open a pull request against the repo with your changes.

### Pull requests

Make sure that the pull request passes the build test. This is ran automatically when new commits are pushed to a branch.

On every push to a branch the book is built to make sure it is valid.

### Editing

The knowledgebase is built as a [mdBook](https://github.com/rust-lang/mdBook). 

The page can be built to HTML by following these steps:

#### 

Follow the steps on the [mdBook website](https://rust-lang.github.io/mdBook/guide/installation.html)

In essence you need to install Rust and Cargo, and then run 
```cargo install mdbook```

#### Viewing the knowledgebase locally

Run the command

```bash
mdbook serve
```

This will serve the knowledgebase locally on port 3000.

#### Building the knowledgebase

Run the command

```bash
mdbook build
```

This will build the knowledgebase in the 'book' directory. A web server can be launched to view the knowledgebase, for example with Python by running ```python3 -m http.server```

### Deployment

When a pull request is merged to main, a GitHub Action automatically publishes the book to GitHub Pages.

