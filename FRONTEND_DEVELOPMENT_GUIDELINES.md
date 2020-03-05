# Frontend Development Guidelines

This document is currently a work in progress, and presents practical guidelines for developers and others at Rogue Sound who write or contribute to software.

This is a reference document, and as such you are expected to dip into it to read the parts that you need to know something about.

Remember, these guidelines are supposed to make everything we produce better, so that we can say "I was a part of that!". It is important that we don't feel that we lose too much velocity trying to adhere to these guidelines. If you feel that they slow things down too much, we need to review them. These things are not set in stone.

## Things to be aware of before start

_Code for others before coding for yourself._

### File organization

```
src
├─── assets
├─── common
├─── config
├─── context
├─── i18n
├─── Layout
│    ├─── Footer
│    ├─── Header
│    └─── Sidebar
├─── pages
│    └─── Home
├─── routes
├─── services
├─── store
├─── styles
├─── themes
└─── utils
```

- **assets**: All static files we need to run the project such as images, icons or SVGs.
- **common**: Here we place all the _atomic_ React components. This means, reusable and indivisible React components used anywhere in the application. Such as buttons, inputs, dropdowns, etc.
- **config**: Here we place all config files for the application.
- **context**: Everything related to state management is placed here. We use `redux-toolkit`.
- **i18n**: Internationalization.
- **Layout**: This module is formed by the header, sidebar and footer of the application.
- **pages**: Here we place all the pages of the application.
- **routes**: React routing config is placed here.
- **services**: This module contains all the API calls we make in the application (to the backend, to the Spotify API, etc.).
- **store**: This is where we place the Redux store config.
- **styles**: All the common and main SASS files are here. Right now is kind of deprecated, as we are using `styled-components`.
- **themes**: All the themes for the application.
- **utils**: All the functions that can be useful for the application are placed here.


### Naming convention

Following and using a naming convention is very important when writing code. It allows everyone to read and understand the code at first sight and enhances consistency and productivity within a development team.
- We use **camelCase** for names of variables, functions, methods, etc. They should be clear and descriptive, not cryptic. For example, function names might be a verb or a question: `getDevices()`, `playCurrentSong()` or `isDeviceActive`.

- For React Components we always use **PascalCase**. This is used in the component's definition and also in the filename. The name should always reflect what is present in that component/file. If the component is included inside a directory, it will also have its name in PascalCase.

- It is common practice to name simple loop variables `i`, `j` and `k`, so there's no need to give them silly names like `the_index` unless it's necessary for some reason or other. Also, avoid calling arrays `array` and objects `object`, let the reader know a bit more than what's immediately obvious from the code.

- Constants must be uppercase and separated with a low dash. For example, `DURATION_IN_SECONDS`.

### Comments in code

Comments should explain why the code does what it does. What it does should ideally already be evident from the code itself. If the code is cryptic and can't easily be simplified, explanations might well be needed.

A good comment clarifies intent.

### Readability

Even though we use Eslint in the project and it is run automatically before pushing a commit into the repository, you must be responsible of the readability of your code. Try to follow the best programming practices and split the code into parts if needed.

If you have to choose between a efficient but cryptic or non-intuitive way of doing something and a less efficient or more verbose way of solving the same problem, either provide ample documentation to the non-intuitive approach or do it less efficiently and leave a comment pointing this out.

### Sensitive data

Sensitive data includes things like passwords, usernames, server names, and data protected by law.

- Do not ever put sensitive data in files that are pushed to GitHub or made public in any other way.
- Some types of data may even only exist in certain folders or on certain machines. Do not proliferate this kind of data, _not even internally_. Also avoid putting this type of data in Dropbox, Google Drive or in similar cloud storage or shared network drive.

- If a password is published by mistake, you need to change the password (with everything that this entails). It is not enough to remove/reverse the commit or submit a new commit with the password removed.

## Development workflow

1. On one hand, you can start looking for [unassigned issues](https://github.com/rogue-sound/rogue-sound-web/issues?q=is%3Aopen+is%3Aissue+no%3Aassignee) in the repository. On the other hand, it is possible that, at some point, we make a list of improvements or new features for external contributors.
2. Create a dedicated git branch with a name reflecting the feature to be implemented (`feature/some-name`).
3. Write a test (Ejem...)
4. Push your feature branch to your upstream.
5. Once it's ready, make a pull request into the develop branch.
6. Wait for review and let the the reviewer (from the Core Team) merge and delete the feature branch.

### Testing

Move on (for now).

## How we use GitHub

In order to maximize exposure, and to facilitate collaborations with other users, we have opted to use GitHub and the infrastructure that GitHub provides for publishing all our publicly accessible software. This also means that we will be using Git for version control.

The repositories are published through a GitHub organization which is formed by the Core Team.

We are really happy that users want to contribute to our repositories. That's one of the main reasons why we use GitHub.

## How we use Git

When appropriate, we use the _Git-Flow branching model_. This is a way of using Git branches as a help in the development cycle.

With Git-Flow, branches are categorised into

- A **master** branch.
- A **develop** branch.
- One or several **feature** branches.
- One or several **hotfix** branches.

The code on the **master** branch is stable, properly tested and is the version of the code that a typical user should pick. No changes are made directly on the master branch (but see below).

The code on the **develop** branch should be working, but without guarantees. For small projects, development might well happen directly on the develop branch and the code here may therefore sometimes be broken (this should ideally never happen though).

A **feature** branch (often called `feature/some-name` where `some-name` is a very short descriptive name of the feature) is branched off from the develop branch when a new "feature" is being implemented. A new feature is any logically connected set of changes to the code base regardless of how many files are being changed.

Once the feature is finished, it is merged back into the develop branch, and its feature branch is deleted. In larger projects, new features should be implemented in feature branches and undergo review before merging (see below). This may be highly beneficial for small projects too, obviously (just do it!).

A **hotfix** branch (often called `hotfix/some-name`) is a essentially a branch that implements a bugfix to a release. In terms of branching, it is thus very similar to a feature branch but for the master branch rather than for the develop branch. A hotfix should fix critical errors that were not caught in testing before the release was made.

The `master` and `develop` branches are never deleted, while the others are transient (temporary, for the duration of the development and review of the feature or hotfix).

### Good practices when working with Git

Commit often, possibly several times a day. It's easier to roll back a small commit than to roll back large commits. This also makes the code easier to review (see below) as each commit carries its own commit message. Remember to push the commits to GitHub every once in a while too.

Write a helpful commit message with each commit that describes what the changes are and possibly even why they were necessary.

Avoid "force push" unless it makes everyone's life easier.

## How we do code reviews

Through reviewing each other's code, we believe that we will produce better code, that we will learn more about programming, and that we will learn more about what our colleagues are actually doing.

A code review may be an iterative process in which a piece of code is commented upon or discussed, changed by the original author, and reviewed again before being approved.

Reviews can be conducted at any stage in development (just let someone look at the code), but we'd like code to be more formally reviewed at least
- before a feature branch is merged to the develop branch, or
- when a bug is fixed on the master branch before its hotfix/bugfix branch is merged.

To be able to use GitHub or a code review, both the author and the reviewer should have their own personal GitHub accounts.

Once the user has finished writing code in a separate feature branch, it's time to create a Pull Request. The author must assign one or more reviewers from the Core Team in order to merge the feature branch into the develop branch. If needed, the author gives the reviewer(s) some background on the project, and what the code under review is supposed to do (don't hesitate to include some screenshots!).

The reviewer(s) then looks at the code and leaves feedback (comments and/or questions) in the pull request. Note that these comments are public. If the reviewer(s) asks for changes, the author should apply them until its approval. Once it is approved, one of the reviwers will merge the pull request and delete the feature (or whatever) branch. **Note: this is the reviewer's job, not the author's job**.