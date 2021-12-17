# lspr

List pull request merge commits.

## Usage

Specify the [ranges of commits](https://git-scm.com/book/en/v2/Git-Tools-Revision-Selection#_commit_ranges) as argument, `lspr` will list the pull request merge commits.

```console
$ lspr HEAD~10..HEAD
482e58ab83fff86ed754b00be27b62a219597e7c        #17     M-x checkdoc    buzztaiki/checkdoc
3029a880d1ae2bbb8ec6280a61515f48e957364d        #16     use lice:comment-enabled-p      buzztaiki/refactor_commenting
8726294b323141dc61425ecd67b1bf00bad81fdb        #15     check the mode supports a comment syntax        buzztaiki/comment_syntax_check
...
```

To show the PR between branches, do the following:

```console
$ lspr production..development
```

To create a release PR using `gh` cli, for example, write the following script:

```bash
#!/bin/bash

title="Release $(TZ=JST-9 date +'%FT%T %z')"
body="\
| Commit | PR | Title |
| -- | -- | -- |
$(lspr production..development | awk -F'\t' -vOFS=' | ' '{print "| "$1, $2, $3" |"}')
"

gh pr create --title "$title" --body "$body" --head development --base production
```


## Requirements
- `git`

## License
MIT

## Alternative
- https://github.com/x-motemen/git-pr-release
- https://github.com/uiur/github-pr-release
- https://github.com/nekonenene/gh-release-pr-generator
