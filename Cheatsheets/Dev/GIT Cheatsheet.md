# Basic Setup Example

``` bat
git init
git add .
git commit -m "first commit"
git remote add REMOTE_ID https://github.com/USER/REPO.git
git branch -M main
```

# Common Use

## Clone from remote cloud

```
git clone https://github.com/GROUP_OR_USER_NAME/REPO_NAME
```

## Push to remote cloud (if you cloned from github/gitlab)

``` bat
git add .
git commit -m "my commit name"
git push -u origin main
```

With prompt to name commit (.bat)

``` bat
@echo off

:: Prompt for commit message
set /p CommitMessage=Enter commit message: 

:: Check if the commit message is empty
if "%CommitMessage%"=="" (
    echo Commit message cannot be empty.
    exit /b 1
)

git add .
git commit -m "%CommitMessage%"
```

## Remotes

```
git remote add GIT_REMOTE_NAME REMOTE_URL
```

if you name the remote "gitlab" or "github" it will error.

Remove remote:
```
git remote remove REMOTE_NAME
```

View remotes:
```
git remote --v
```

---
# Credentials


### Windows Certificates
If you authenticate from any prompt git most likely will make a windows credential automatically
start > credentials manager > windows credentials > (look for something git related)

```text
git config --global credential.https://github.com.useHttpPath true
```
This command makes each unique repo visited at github have to uniquely authenticate 

You can view the git config here:
``` sh
git config --list --global
```

The git config file is here:
C:\Users\USERNAME\.gitconfig

here's an example of what it should look like:

```text
[filter "lfs"]
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
	process = git-lfs filter-process
	required = true
[user]
	name = my_name
	email = my_email@email_provider.com
```


Fix Line ending warning on add

``` sh
git add --renormalize .
```


# Write to multiple git services at the same time

add them as remotes

``` bat
git remote add github https://github.com/user-name/repo-name.git
git remote add gitlab https://github.com/user-name/repo-name.git
```

then run this after commits to upload to both. You can turn this into a .bat file

``` bat
git push -u github main
git push -u gitlab main
```