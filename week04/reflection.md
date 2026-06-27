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

#Task 4
# Task 4 — Review Culture in rust-analyzer

For this task, I examined several merged pull requests in the rust-analyzer project, including [#22618](https://github.com/rust-lang/rust-analyzer/pull/22618), [#22486](https://github.com/rust-lang/rust-analyzer/pull/22486), [#21319](https://github.com/rust-lang/rust-analyzer/pull/21319), [#22115](https://github.com/rust-lang/rust-analyzer/pull/22115), and [#22044](https://github.com/rust-lang/rust-analyzer/pull/22044).

The most noticeable review norm was that maintainers focused primarily on correctness, edge cases, and tests rather than minor stylistic preferences. Comments were usually connected to a concrete risk, such as an assist producing invalid code, an implementation failing for a particular syntax form, or a missing test for important behavior.

Tests were treated as part of the feature design rather than as an optional addition. Reviewers frequently requested tests that demonstrated both the intended behavior and relevant edge cases. In one case, the implementation became unnecessary because another pull request fixed the problem first, but the tests were still considered valuable enough for the pull request to be reduced and merged as a test-only change.

The scope of a pull request was also allowed to evolve during review. Authors sometimes marked their work as draft, revised the implementation after feedback, or removed code that was no longer necessary. Reviewers did not insist that every related concern be solved in the same pull request. Some adjacent problems were deliberately deferred to follow-up work so that the current change could remain focused.

The intensity of the review depended on the risk of the change. Small and well-contained fixes were sometimes approved quickly, while large migrations and architectural changes received input from multiple reviewers and went through more iterations.

The discussions were generally direct but focused on the code rather than the contributor. Overall, rust-analyzer’s review culture appears to follow the principle that a pull request should be merged when it clearly improves the codebase, not when it is theoretically perfect.
