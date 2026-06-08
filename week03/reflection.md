# task 1 & 2
I searched through dozens of repositories for an issue with a sprawling reproduction or a bug that needs confirmation with no luck. But I found an issue on the [eslint project](https://github.com/eslint/eslint) where a user found a false positive in `use-isnan` where locally shadowed `NaN` or `Number` bindings are reported as if they were the built-in global values [issue](https://github.com/eslint/eslint/issues/20950).

the reproduction provided by the user was great and did not even need reduction. I was able to reproduce the issue locally and confirm that it was indeed a bug. I then looked through the codebase to find the source of the issue and found that the rule was not properly checking for shadowed variables. 

I took a quick look at `lib/rules/use-isnan.js`. The rule appears to route all of these checks through `isNaNIdentifier()`, which currently matches:

```js
astUtils.isSpecificId(nodeToCheck, "NaN") ||
astUtils.isSpecificMemberAccess(nodeToCheck, "Number", "NaN")
```
The helpers check identifier names and AST shape, but I did not find scope resolution in this path. That seems consistent with the false positive: local bindings named `NaN` or `Number` are treated the same as references to the global built-ins.
the maintainer accepted the reproduction and is open for contribution on this bug. 

Then I found an issue on the [rust analyzer project](https://github.com/rust-lang/rust-analyzer) where a user reports a false positive in the macro matcher using optional or zero-or-more repetition reports false diagnostics [issue](https://github.com/rust-lang/rust-analyzer/issues/22431).

I was able to reproduce the issue locally and confirm that it was indeed a bug since the rustc and cargo check both succeed without any errors. Then I minimized the reproduction to remove unnecessary statements, and tested other forms of repetition to see if they were also affected and scope the issue better.

# task 3
while working on the eslint issue, I tried to find if the issue is new or if it has been around for a while using bisect but I was not able to find a commit that introduced the issue. It seems like this has been an issue for a while and has not been noticed until now.

also while working on the cxxgraph issue I could not find a known-good release to bisect from. The issue appears to be present at least as far back as v0.1.4, the earliest release tag where this MCVE compiles for me.

# task 4
After working on the MCVE, I also found a bad [issue](https://github.com/ZigRazor/CXXGraph/issues/497) description in the [cxxgrapgh project](https://github.com/ZigRazor/CXXGraph) describing a segfault behaviour in the weighted directed graph container, the issue had a single sentence description without tests or code, the maintainer commented asking for more details but the user did not respond so I looked at it and found that I reproduce a related failure without a path finding algorithm. That terminates with `std::bad_optional_access` rather than a direct segfault. maybe this will help the maintainer solve this issue if possible.
