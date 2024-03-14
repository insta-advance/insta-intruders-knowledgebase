# Insta Intruders knowledgebase

The Insta Intruders knowledgebase is a repository for information about penetration testing. It has information about common attacks and recommended tooling to be used for these.

## Contributing

If you have any suggestions about what should be added to the knowledgebase, open an issue! You can also open a pull request against the repo with your changes.

### Pull requests

Make sure that the pull request passes the build test. This is ran automatically when new commits are pushed to a branch.

On every push to a branch the book is built to make sure it is valid.

### Editing

The knowledgebase is built as a [mdBook](https://github.com/rust-lang/mdBook). When a new version is done, it can built to HTML using the command ```mdbook build```.

### Deployment

When a pull request is merged to main, a GitHub Action automatically publishes the book to GitHub Pages.

