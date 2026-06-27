# Task 1
For my first review, I examined a [pull request](https://github.com/uutils/grep/pull/54) in the [uutils/grep](https://github.com/uutils/grep) repository, The PR fixes incorrect handling of multi-character Unicode case folds during case-insensitive matching
I checked out the PR locally, ran its test suite, and compared its behavior with the main branch. The change correctly prevented cases such as ß matching SS, while preserving ordinary one-to-one Unicode case folding.

The PR included tests for the behavior being removed, but it did not include a control test confirming that desired non-ASCII case-insensitive matching, such as ä matching Ä, remains supported. [my comment](https://github.com/uutils/grep/pull/54#issuecomment-4818920427)

for the second review I found a [pull request](https://github.com/rust-lang/rust-analyzer/pull/22645) in the [rust-lang/rust-analyzer](https://github.com/rust-lang/rust-analyzer) repository, request that adds an .await quick fix for type mismatches involving futures. The implementation correctly checked whether the future output matched the expected type, but it did not verify whether .await was legal at the expression’s location. I reproduced the issue in a synchronous function and in a non-async closure inside an async function, where the suggested fix still produced invalid Rust.

[my comment](https://github.com/rust-lang/rust-analyzer/pull/22645#issuecomment-4821188122)