### First Pull Request
This week, I contributed to the [rust analyzer project](https://github.com/rust-lang/rust-analyzer), which is a language server that provides IDE functionality for writing Rust programs. Thanks to dotacow for recommending this project to me.
I started by by looking for `FIXME` comments in the codebase, which were added by the developers to indicate areas of the code that needed fixing, announced in this [issue](https://github.com/rust-lang/rust-analyzer/issues/22140). I found a `FIXME` comment in the file `crates/hir-ty/src/infer/pat.rs` describing this missing diagnostic. Producing a user-facing error clarifies the analyzer's behavior and prevents surprising inference results. I tried to follow the recommended pull request template as much as possible.
And it got Merged!!! more details in [this PR](https://github.com/rust-lang/rust-analyzer/pull/22424)

### Second Pull Request
I also contributed to the [tldr project](https://github.com/tldr-pages/tldr), which is collaborative cheatsheets for console commands and community-maintained help pages for command-line tools. I added arabic translation for the scp command, which is a command-line utility for securely copying files and directories between hosts on a network. More details in [this PR](https://github.com/tldr-pages/tldr/pull/22533). It got merged as well!

### Review Commments
I found a pull request in the [tdlr project](https://github.com/tldr-pages/tldr), that adds a new page for the `niri` which is a scrollable-tiling Wayland compositor. The [pr](https://github.com/tldr-pages/tldr/pull/22534) follows the template and is correct, but has a margin for improvement. I suggested to add better examples for the `niri` command, and to clarify a parameter in the description.
The contributor responded (by commits) to my comments and made the necessary changes.
