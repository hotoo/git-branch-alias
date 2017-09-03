# README

branch-alias subcommand for git

## Install

```
npm i git-branch-alias -g
```

## Usage

```
${command} <alias> [ <branch> ]
${command} [ --delete | -d ] <alias>
```

Creates a symbolic reference `<alias>` referring to `<branch>`.

`<branch>` defaults to the current checked-out branch.

This symbolic reference acts as an alias for `<branch>`, and can be
used in its place. More specifically, it WILL be dereferenced to
its target in nearly all situations, so for any given command you
should treat every usage of `<alias>` as if it were actually `<branch>`.

To safely delete a branch alias, use:

```
${command} --delete <alias>
```

WARNING: These symbolic references appear in your branch list as:

```
 <alias> -> <branch>
```

and so you might be tempted to try to delete them like a branch:

```
 git branch -d <alias>
```

However this can cause problems. In git versions prior to 1.8.0.1
`<alias>` will be dereferenced and you will instead delete the
branch it refers to (git will allow this even if you currently
have that branch checked out), and the symbolic reference will
still remain (referencing a branch which is no longer available).
In later versions of git the `<alias>` will be deleted rather than
the branch; however git will still not check to see whether you
currently have `<alias>` checked out, and will not prevent you
from deleting it in that situation. This will leave your HEAD ref
in an invalid state. Using `${command} -d <alias>` resolves this
situation by switching HEAD to <alias>'s target.

## Thanks

- https://gist.github.com/mauricerkelly/0b12b20a870d1e38081e
