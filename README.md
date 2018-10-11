# Git emoji hook

A simple git hook to provide strong guidelines for commit message with emojis.

The commit message rules are the ones from Angular. I just augmented them by substituting their textual types with emojis. So it should look like this:

```
🚑 (authentication): remove buggy function that allowed to login w/o passwd
```

You'll notice another slight change from Angular's rules: I added a space between type and (scope). It is indeed visually more pleasant after the emojis.

__Emojis are actual unicode emojis and not markdown emojis like `:fire:`. So it will work virtually everywhere as long as unicode is supported.__

There are two hooks, one that makes the actual substitution and another one that prints the git commit message helper in the editor.

## Syntax
Here are the types, their respective codes and the corresponding emojis:
* __revert__: `:revert:` • 🔨
* __build__: `:build:` • 📦
* __ci__: `:ci:` • 🤖
* __docs__: `:docs:` • 📖
* __feat__: `:feat:` • 🌟
* __fix__: `:fix:` • 🚑
* __perf__: `:perf:` • ⚡
* __refactor__: `:refactor:` • 🚧
* __style__: `:style:` • 💄
* __text__: `:test:` • ✅

In addition to these, I added `:tada:` 🎉 that's often used for the first commit!


## How to use
For each project, add the two files in in the `.git/hooks` directory.

It might be handy to place the two files in a directory withing your directory and add a bash alias to automate the deploy.

For exemple, in your home diretory, you could organize things like this:
```
.gitemojis/
    commit-msg
    prepare-commit-msg
```

And in your `.bash_profile` or `.bashrc`
```
alias ginit='git init && cp ~/.gitemojis/* .git/hooks/'
```

Now, when in a new project directory, `ginit` will both initialize the project and add the git-emojis' hooks.

## Based on Angular's commit message guidelines
Angular enforces succint and yet very clear guidelines for their commit messages. Let's have a look at the rules. The following is directly copied from [their repo](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#-commit-message-guidelines).

We have very precise rules over how our git commit messages can be formatted. This leads to more readable messages that are easy to follow when looking through the project history. But also, we use the git commit messages to generate the Angular change log.

### Commit Message Format
Each commit message consists of a **header**, a **body** and a **footer**.  The header has a special
format that includes a **type**, a **scope** and a **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The **header** is mandatory and the **scope** of the header is optional.

Any line of the commit message cannot be longer 100 characters! This allows the message to be easier
to read on GitHub as well as in various git tools.

The footer should contain a [closing reference to an issue](https://help.github.com/articles/closing-issues-via-commit-messages/) if any.

Samples: (even more [samples](https://github.com/angular/angular/commits/master))

```
docs(changelog): update changelog to beta.5
```
```
fix(release): need to depend on latest rxjs and zone.js

The version in our package.json gets copied to the one we publish, and users need the latest of these.
```

### Revert
If the commit reverts a previous commit, it should begin with `revert: `, followed by the header of the reverted commit. In the body it should say: `This reverts commit <hash>.`, where the hash is the SHA of the commit being reverted.

### Type
Must be one of the following:

* **build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
* **ci**: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
* **docs**: Documentation only changes
* **feat**: A new feature
* **fix**: A bug fix
* **perf**: A code change that improves performance
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **test**: Adding missing tests or correcting existing tests

### Scope
The scope should be the name of the npm package affected (as perceived by the person reading the changelog generated from commit messages.
