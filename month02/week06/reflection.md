# Week 06

## Task 1

I contributed a new dnf copr page to tldr-pages after confirming that no one else was working on it. I tested the commands locally on Fedora and documented the most useful examples in the project’s concise format.

the [issue](https://github.com/tldr-pages/tldr/issues/17160), and [my pr](https://github.com/tldr-pages/tldr/pull/23133)

## Task 2

For the second task, I created a MkDocs Material site for my [libft project](https://github.com/abusalah0/libft_42) and published it through GitHub Pages. I organized the content using the Diátaxis framework:

- A tutorial for building a first program with libft.
- A how-to guide for integrating libft into another project.
- Reference documentation for the public functions.
- An explanation of memory ownership in C and libft.

The most challenging part was separating the tutorial from the how-to guide. My first version of the how-to repeated the tutorial because both described building and linking the library. I revised it to focus specifically on integrating libft into an existing project and Makefile.

Writing the function reference also exposed inconsistencies in the code. In particular, I found issues in the return type of `ft_strcmp` and the validation behavior of `ft_isnumber`. I fixed both before documenting them. This showed me that writing documentation can improve the software itself because it forces the author to examine the public API carefully.

the [github pages site](https://abusalah0.github.io/libft_42/)

## Task 3

For the third task, I wrote an Architecture Decision Record explaining why the project uses MkDocs Material.

The ADR records the context, the selected solution, the alternatives considered, and the positive and negative consequences of the decision. ADR's should explain why a decision was made, not merely state what tools the project uses so i wish i started using them in earlier projects.

## Task 4

For the final task, I configured Vale with the Microsoft writing style and added it as a separate job in the CSI Portal CI workflow.

Keeping Vale in a separate job prevents the prose check from running once for every Node.js version in the test matrix. I also learned how Vale packages and project vocabularies work. The Microsoft rules can be synchronized automatically, while project-specific terminology can be maintained in a custom vocabulary.
