# git commands - cheatsheet

*Wednesday, February 12th, 2025* by **devP**

### `git log`
`git log --oneline` 
shows git log as one line per commit

`git log --graph` 
shows git log as graph 

### `git cherry-pick` 
If the GIT_AUTHOR_DATE and GIT_COMMITTER_DATE environment variables support are used,m a git commit can be cherry picked by adding date date other than the original date from cherry picked commit. Full or shorthand Commit SHA can be used.

With shorthard Commit SHA
`GIT_AUTHOR_DATE='2025-02-19T12:34:56 -0500' GIT_COMMITTER_DATE='1234567890 -0500' git cherry-pick 34ac98`

With Full Commit SHA
`GIT_AUTHOR_DATE='2025-02-19T12:34:56 -0500' GIT_COMMITTER_DATE='1234567890 -0500' git cherry-pick 34ac98dbd87f1cb866d90d1824504a2124544254`

[More about git commit supported date formats](https://git-scm.com/docs/git-commit#_date_formats)