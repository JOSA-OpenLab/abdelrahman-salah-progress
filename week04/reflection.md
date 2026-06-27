# Task 1
For my first review, I examined a [pull request](https://github.com/uutils/grep/pull/54) in the [uutils/grep](https://github.com/uutils/grep) repository, The PR fixes incorrect handling of multi-character Unicode case folds during case-insensitive matching
I checked out the PR locally, ran its test suite, and compared its behavior with the main branch. The change correctly prevented cases such as ß matching SS, while preserving ordinary one-to-one Unicode case folding.

The PR included tests for the behavior being removed, but it did not include a control test confirming that desired non-ASCII case-insensitive matching, such as ä matching Ä, remains supported. [my comment](https://github.com/uutils/grep/pull/54#issuecomment-4818920427)

for the second review I found a [pull request](https://github.com/rust-lang/rust-analyzer/pull/22645) in the [rust-lang/rust-analyzer](https://github.com/rust-lang/rust-analyzer) repository, request that adds an .await quick fix for type mismatches involving futures. The implementation correctly checked whether the future output matched the expected type, but it did not verify whether .await was legal at the expression’s location. I reproduced the issue in a synchronous function and in a non-async closure inside an async function, where the suggested fix still produced invalid Rust.

[my comment](https://github.com/rust-lang/rust-analyzer/pull/22645#issuecomment-4821188122)

#Task 2
There are many pull requests that Im not proud, may be even a majority of them. one that stands out was a pr named `styling and permisions (mostly)`, I was working on a Django project and was supposed to update the UI of several pages and add permission rules for superusers.
the pr was a mess, no description, no tests, does not reference an issue, no formatting, and I added features that were not mentioned or requested, breaking changes, changing order of content for unrelated pages, I even changed the data models. So yes, I was not proud of that PR, and I learned a lot from it after the conequences of it.
If I were reviewing this PR today, I would request that it be split into smaller, focused changes. The permission logic should have included tests, the model changes should have been isolated and explained, and unrelated UI changes should have been removed from the scope. I would also ask for a clear description of the intended behavior and any migration or compatibility concerns.

#Task 3
I examined [rust-analyzer](https://github.com/rust-lang/rust-analyzer) [PR #22044](https://github.com/rust-lang/rust-analyzer/pull/22044), which addressed unwanted completion suggestions from core::intrinsics and std::intrinsics.

The reported problem was narrow, but the PR implemented a general system for identifying and filtering every internal unstable Rust feature. This required parsing unstable feature attributes, exposing new APIs across the HIR layers, interning many additional symbols, and maintaining a hard-coded set of compiler-internal features. The code itself includes a FIXME noting that this list may be difficult to keep synchronized.

A simpler solution would have filtered the specific intrinsics feature or paths involved in the reported issue. That would have solved the current problem with less code and maintenance cost.