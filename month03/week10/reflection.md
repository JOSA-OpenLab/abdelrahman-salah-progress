# Week 10

A plan for my open-source contribution efforts over the coming three months, covering three candidate projects.

**Contents**

1. [Ruff](#1--ruff)
2. [rust-analyzer](#2--rust-analyzer)
3. [Manim](#3--manim)

---

## 1 — Ruff

> Repository: [astral-sh/ruff](https://github.com/astral-sh/ruff)

**Ruff** is a Python linter and formatter written primarily in Rust. It aims to replace or consolidate tools such as Flake8, isort, pyupgrade, and Black while remaining significantly faster. Ruff currently has roughly 47k GitHub stars, more than 900 lint rules, first-party editor integrations, and a large user base across the Python ecosystem.

The project is maintained by Astral, the team behind tools such as uv. Development is very active: Ruff continues to publish frequent releases containing new lint rules, formatter changes, bug fixes, and performance improvements.

### Why Ruff

Ruff fits my interests because it combines several areas I want to become stronger in:

- Rust development in a large production codebase
- Compilers and source-code analysis
- Parsing and AST manipulation
- Static analysis and linting
- Automated code fixes
- Performance-sensitive software
- Python tooling

I already use both Rust and Python, so Ruff sits directly between two ecosystems I work with.

I also want to improve at making changes in a large mature Rust codebase where correctness is more important than simply getting the implementation to compile.

### Contribution area

Rather than choosing unrelated issues, I would focus the 12 weeks around **lint-rule correctness, autofixes, and performance**.

### 12-week milestones

#### Weeks 1–2 — Understand the project

- Build Ruff locally.
- Run the full and targeted test suites.
- Read the contributor documentation.
- Understand the workspace and major crates.
- Trace one existing lint rule from registration to diagnostic emission.
- Trace one rule that provides an autofix.
- Reproduce several open issues locally.

**Deliverable:** architecture notes and 2–3 candidate issues.

#### Weeks 3–4 — First contribution

Select a small correctness issue. Work would include:

- creating a minimal reproduction,
- locating the responsible rule,
- writing a failing regression test,
- implementing the fix,
- submitting the first PR.

**Target:** first merged or reviewed Ruff contribution.

#### Weeks 5–6 — Semantic analysis

Choose a more involved lint rule that requires understanding semantic information rather than syntax alone.

Focus on:

- symbol resolution,
- scopes,
- type or binding information,
- false-positive avoidance.

**Target:** second contribution.

#### Weeks 7–8 — Autofix correctness

Investigate an issue involving automatic fixes. The work should verify:

- diagnostic correctness,
- source-range selection,
- fix safety,
- preservation of comments and formatting,
- behavior across supported Python versions.

**Target:** one autofix-related contribution.

#### Weeks 9–10 — Performance

Profile a real Ruff workload, for example:

```bash
ruff check large-python-project/
```

or:

```bash
ruff format large-python-project/
```

Use profiling to identify a measurable hot path. Only propose a change if:

- the bottleneck is measurable,
- the optimization is small,
- behavior remains unchanged.

**Target:** performance report and, if appropriate, a PR.

#### Weeks 11–12 — Consolidation

- Follow up on review feedback.
- Fix regressions or edge cases discovered during reviews.
- Improve relevant documentation.
- Summarize the architecture and areas learned.
- Identify longer-term contribution areas.

**Final goal:** several meaningful contributions around one coherent area rather than many unrelated small PRs.

### Risks

- **Issue availability**
- **Codebase complexity**
- **Semantic correctness**
- **Review latency**

### Mentorship needed

I would mainly need mentorship in:

- Ruff's internal architecture.
- Parser and AST representation.
- Semantic-model design.
- Deciding when a diagnostic belongs in syntax analysis versus semantic analysis.
- Evaluating autofix safety.
- Understanding project-specific testing conventions.

---

## 2 — rust-analyzer

> Repository: [rust-lang/rust-analyzer](https://github.com/rust-lang/rust-analyzer)

**rust-analyzer** is the Rust language server and a compiler front-end designed for IDE use. It provides features such as completion, diagnostics, navigation, refactoring, hover information, assists, and semantic analysis.

rust-analyzer is maintained by contributors within the Rust project and has a large active issue queue covering diagnostics, macros, completion, assists, type inference, project loading, and performance.

### Why rust-analyzer

rust-analyzer is especially attractive because it combines several areas I want to understand deeply:

- Compiler architecture
- Parsing and syntax trees
- Macro expansion
- Type inference
- Incremental computation
- IDE and language-server design
- Performance-sensitive tooling

I have already spent time investigating rust-analyzer issues and reviewing contributions, so I am not starting from zero.

For example, I previously investigated incorrect macro diagnostics involving optional `macro_rules!` repetition and reviewed behavior involving `.await` assists. That gives me some initial familiarity with reproducing mismatches between rust-analyzer and rustc.

My main goal would be to move from reproducing and reviewing bugs to implementing fixes in the compiler front-end itself.

### Contribution area and issues

I would focus on **diagnostic correctness around macros, type inference, and assists**. This gives the 12-week work a coherent direction while still exposing me to several major rust-analyzer subsystems.

One concrete issue is:

> **`#22442`** — Incorrect "Leftover tokens" error with `$(…)?` repetition

This open issue concerns incorrect errors in macro expansion involving optional repetition. It directly overlaps with macro behavior I have already investigated, and would require understanding:

- `macro_rules!` expansion,
- token trees,
- optional repetition,
- how rust-analyzer differs from rustc,
- where diagnostics are generated.

Other candidate areas from the current issue queue include incorrect completion behavior in async contexts and type-system errors reported by rust-analyzer but not by rustc. I would use these as a pool rather than promise that every specific issue will remain open for all 12 weeks.

Recent releases also show that first-time contributors are successfully landing diagnostics and performance changes, including parser allocation improvements and new diagnostics.

### 12-week milestones

#### Weeks 1–2 — Architecture and environment

- Build rust-analyzer locally.
- Run targeted and workspace tests.
- Study the contributor architecture documentation.
- Map the relevant crates:
  - `parser`,
  - `syntax`,
  - `hir`,
  - `hir-def`,
  - `hir-ty`,
  - IDE diagnostics,
  - assists.
- Learn how rust-analyzer compares behavior against rustc.
- Reproduce several candidate issues.

**Deliverable:** architecture notes and candidate issue list.

#### Weeks 3–4 — Macro expansion

Start with a macro-expansion correctness issue such as `#22442`. Tasks:

- reduce the issue to a minimal case,
- identify the expansion stage that diverges,
- understand repetition handling,
- add a regression test,
- attempt a focused fix.

**Target:** first implementation PR.

#### Weeks 5–6 — Diagnostics

Move to an incorrect or missing diagnostic. Study:

- where diagnostics originate,
- how HIR information is exposed,
- how rust-analyzer avoids reporting errors that rustc accepts.

**Target:** one diagnostic correctness contribution.

#### Weeks 7–8 — Assists and context awareness

Investigate an assist or completion whose availability depends on semantic context. Potential areas include:

- async context,
- type mismatch fixes,
- completion visibility,
- trait implementation assists.

The emphasis would be on preventing an assist from being offered when its generated code is invalid.

**Target:** one assist/completion contribution.

#### Weeks 9–10 — Type inference or performance

Attempt one deeper task involving either:

- type inference,
- incremental queries,
- memory usage,
- parser/analysis performance.

Recent rust-analyzer releases include frequent performance work, such as reducing parser allocation and sharing proc-macro servers, so performance remains an active area.

The goal would initially be investigation and measurement. A PR would only be attempted if the change is small and understood.

#### Weeks 11–12 — Follow-up and consolidation

- Add missing regression tests.
- Document architecture learned during the project.
- Review related issues and PRs.
- Identify an area for continued contribution after the apprenticeship.

**Final target:** become capable of independently reproducing, locating, and fixing a small-to-medium rust-analyzer correctness issue.

### Risks

- **Compiler complexity** — the largest risk is the learning curve. A behavior visible as a small IDE bug may involve parsing, macro expansion, lowering, type inference, and IDE presentation.
- **Issues may become obsolete** — the project moves quickly and releases weekly, so selected issues may be fixed before I reach them.
  - *Mitigation:* define a contribution area and maintain a pool of candidate issues rather than committing the entire proposal to one ticket.
- **Review expectations** — compiler changes require strong regression tests and careful reasoning.
- **AI contribution restrictions** — rust-analyzer has explicit restrictions around AI usage for some contributor-labelled issues and has tightened policies around AI-generated comments/issues. Recent release notes explicitly mention these policies.

### Mentorship needed

rust-analyzer is where mentorship would be most valuable. I would need guidance in:

- understanding the HIR layers,
- macro-expansion internals,
- Salsa/incremental computation,
- type inference,
- diagnostic architecture,
- deciding which subsystem owns a particular bug,
- understanding differences between rust-analyzer and rustc.

---

## 3 — Manim

> Repository: [ManimCommunity/manim](https://github.com/ManimCommunity/manim)

**Manim Community** is a Python framework for creating mathematical animations. It is used by educators, students, researchers, and developers to programmatically create visual explanations of mathematical and technical concepts.

Manim supports contributions in several areas, including code maintenance, documentation, testing, performance work, DevOps, plugins, and educational content. The project is currently undergoing a major refactor, so contributors are encouraged to discuss substantial work with maintainers before implementation.

### Why Manim

Manim interests me because it combines software engineering with visualization, mathematics, and educational tooling.

I would like to improve my skills in:

- Python library development,
- graphics and rendering systems,
- geometry and coordinate systems,
- performance profiling,
- API design,
- testing graphical software,
- maintaining a mature open-source codebase.

Unlike a typical backend project, Manim gives immediate visual feedback. A bug in geometry, transformation, positioning, or rendering can often be understood both through the implementation and through its visible output.

I am also interested in tools that make technical ideas easier to understand, which makes mathematical visualization a useful area for me to explore.

### Contribution area and issues

Because Manim is currently undergoing a large refactor, I would avoid proposing major new APIs or features. Instead, I would focus the 12 weeks on **correctness, testing, and performance of Manim's geometry and rendering behavior**.

This fits the project's current contribution guidance, which explicitly welcomes maintenance, tests, documentation, and performance work during the refactor.

Recent releases show continued work in exactly these areas. For example, recent changes have fixed incorrect geometric behavior such as `Circle.point_at_angle`, addressed 3D image transformations, cleaned up `TipableVMobject`, improved `MathTex` handling, and added performance-oriented Ruff rules.

I would target issues from three related categories.

#### Geometry and transformation correctness

Investigate bugs involving:

- points and coordinates,
- rotations and transformations,
- vectorized mobjects,
- coordinate systems,
- 2D and 3D geometry.

For each issue, I would create a minimal scene demonstrating the incorrect behavior, trace the relevant implementation, add a regression test, and implement a focused fix where possible.

#### Graphical and unit testing

Manim has dedicated support for unit, graphical, and video tests.

I would work on strengthening tests around the areas I investigate, especially bugs where visual behavior previously lacked regression coverage.

#### Performance

Manim has dedicated contributor documentation for profiling and improving performance, including use of Python profiling tools such as cProfile and SnakeViz.

Later in the project, I would profile a real rendering workload and investigate a measurable hot path. Potential areas include:

- repeated geometry calculations,
- object transformations,
- scene updates,
- SVG or text processing,
- unnecessary allocation or copying,
- rendering preparation.

Any optimization would be measurement-driven rather than speculative.

### 12-week milestones

#### Weeks 1–2 — Learn the architecture

- Set up Manim from source.
- Run the test suite.
- Read the contribution and development documentation.
- Understand the major packages and rendering flow.
- Study how `Mobject`, `VMobject`, `Scene`, animations, and renderers interact.
- Learn how Manim's graphical regression tests work.
- Reproduce several open bugs locally.

**Deliverable:** architecture notes and a shortlist of 2–3 candidate issues.

#### Weeks 3–4 — First correctness contribution

Choose a small geometry or transformation bug. Work through:

- minimal reproduction,
- relevant source path,
- expected behavior,
- failing regression test,
- focused implementation fix.

Discuss the proposed change with maintainers before significant implementation because of the ongoing refactor.

**Target:** first reviewed or merged PR.

#### Weeks 5–6 — Graphical testing

Take a second issue where correctness is most easily demonstrated visually, and learn to use Manim's graphical testing infrastructure.

Add regression coverage that demonstrates:

- the broken output before the fix,
- the expected rendering afterward.

**Target:** a contribution combining a bug fix with graphical regression coverage.

#### Weeks 7–8 — Deeper geometry or rendering work

Investigate a more complex issue involving one of:

- `VMobject`,
- coordinate systems,
- transformations,
- 3D objects,
- scene updates.

The goal is to understand interactions between Manim's object model and rendering behavior rather than only modifying isolated utility functions.

**Target:** one medium-sized correctness or maintenance contribution.

#### Weeks 9–10 — Performance investigation

Select a representative animation and profile it. Manim's own contributor documentation recommends profiling real scenes when investigating performance.

Record:

- rendering time,
- profiler output,
- the most expensive functions,
- a hypothesis about the cause.

If a safe optimization is identified:

- implement it,
- verify visual output remains unchanged,
- rerun the benchmark,
- report before/after numbers.

**Target:** performance report and, if appropriate, a performance PR.

#### Weeks 11–12 — Documentation and consolidation

- Address outstanding review feedback.
- Improve documentation related to the areas I worked on.
- Add or improve examples where APIs were difficult to understand.
- Review related open issues.
- Document the parts of Manim's architecture I learned.
- Identify a longer-term contribution area.

Manim explicitly welcomes documentation examples, and its guidelines encourage short, runnable examples that demonstrate one concept clearly.

**Final target:** several focused contributions around correctness, testing, and performance rather than unrelated one-off changes.

### Risks

- **Ongoing major refactor** — this is the largest risk. Manim currently warns that major new features may not be accepted and that unrelated changes may take longer to review during the refactor.
- **Visual bugs can be difficult to test** — a bug may depend on rendering configuration, backend, resolution, or platform.
- **Rendering architecture complexity** — a visible problem may originate far below the public API, for example in object transformation, geometry calculation, or renderer-specific behavior.
- **External dependencies** — Manim interacts with components such as PyAV, Cairo/OpenGL-related rendering paths, LaTeX, fonts, and other system dependencies. Environment differences may complicate reproductions.
- **Issue availability** — the project currently has hundreds of open issues and many active PRs, so an issue may already have someone working on it.

### Mentorship needed

The main mentorship I would need is understanding where responsibilities lie inside Manim's architecture. In particular:

- the `Mobject` and `VMobject` hierarchy,
- transformation and coordinate-system internals,
- Cairo versus OpenGL rendering paths,
- graphical regression testing,
- deciding whether a problem belongs in geometry, rendering, or the public API,
- identifying work that fits the current refactor direction.

The most useful mentorship would be architectural guidance and feedback on proposed approaches.
