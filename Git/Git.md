---
title:        Git
layout:       default
permalink:    Git
category:     Git
has_children: true
share:        true
shortRepo:

- git
- default

---

<br/>

---

---

<details markdown="block">                
<summary>                
Table of contents                
</summary>                
{: .text-delta }                
1. TOC                
{:toc}                
</details>

# Scripts

## main to master

```shell
git branch -m main master
git fetch origin
git branch -u origin/master master
git remote set-head origin -a
```

## get users gists

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer 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" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/users/14paxton/gists
```

---

# Cheat Sheets

![GitCheatSheet.png](../assets/images/GitCheatSheet.png)

![GitDetailedCheat.png](../assets/images/GitDetailedCheat.png)

---

# Authentication

# There are three main approaches you can take

1. Using a personal authentication token or password
2. Using an SSH key
3. Using your GitHub password with 2-factor authentication

> With either of the first two approaches you can avoid entering a username and password each time

---

## Personal Authentication

```shell
 git config -l
```

In what follows, I'll refer to the account or organization the repository exists in as ACCOUNT and the repository as REPO.

Using HTTPS with a personal authentication token or a password  
The standard way to interact with a repository is via HTTPS.  
You can clone a repository using HTTPS like this:

```shell
 git clone https://github.com/ACCOUNT/REPO
```

> You'll be asked to enter your username and password (where the latter could be either your
> GitHub password or your personal authentication token.

> As of fall 2021, GitHub will no longer allow usage of a password alone.  
> One good option is to use a personal authentication  
> token in place of a password.

> You can create a token using these instructions or simply go here.  
> If you're just interacting with repositories, you probably  
> want to simply select 'repo' as the "scope".

> Saving your password or token to avoid entering it  
> You can save, or cache, your credentials so that you don't have to reenter them each time you interact with the remote repository.

> Your credentials can be stored in the keychain of your operating system or cached in memory
> or in a file.

> To cache in memory, in the MacOS keychain, or in the Windows keychain, choose the relevant
> one of these three invocations:

---

### In memory

```shell
 git config --global credential.helper cache
```

> MacOS

```shell
 git config --global credential.helper osxkeychain
```

> Windows

```shell
 git config --global credential.helper wincred
```

> To set the cache in memory to last for a particular amount of time, here 3600 seconds (i.e., 1 hour):

```shell
 git config --global credential.helper 'cache --timeout=3600'
```

> If you prefer to set the credential helper on a repository-specific basis, you can omit the `--global` flag.

> To check if the credential helper is set up:

```shell
 git config --get credential.helper
```

## SSH keys

To use SSH, you need to put your SSH public key in your GitHub account.  
Your public key file is found in the  
`~/.ssh` directory on a Mac or Linux machine and will generally be a file ending in .pub

Go to <https://github.com/settings/keys> and copy/paste your public key from the public key file.

> You can then clone a repository using syntax of either of the following types:

```shell
 git clone git@github.com:ACCOUNT/REPO.git
 git clone ssh://github.com/ACCOUNT/REPO
```

> To confirm you are using ssh, run

```shell
 git config --get remote.origin.url
```

> If you see either of the following, you know you're using SSH to interact with the repository.

```shell
 git@github.com:paciorek/test-auth.git
```

```shell
 ssh://github.com/paciorek/test-auth
```

> Avoiding having to enter your SSH passphrase  
> Note that you may be asked to enter your SSH passphrase when interacting with a repository.  
> To avoid having to keep doing this, > you can add your passphrase to your running SSH authentication agent, like this (assuming here your key is
> called 'id_rsa'):

```shell
 ssh-add ~/.ssh/id_rsa
```

> Note that you might need to start your SSH agent with:

```shell
 eval `ssh-agent -s
```

> More details on using the SSH agent can be
> found [here](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

> If you have a repository that is using HTTPS and you want to switch to SSH, you can run either of these invocations from within a > directory within
> your repository:

```shell
 git config remote.origin.url git@github.com:ACCOUNT/REPO.git
```

```shell
 git remote set-url origin git@github.com:ACCOUNT/REPO.git
```

> Using a password plus two-factor authentication

> Finally, if you want you can use your GitHub password (potentially saved via credential.helper as discussed above so you don't

> have to enter it), rather than a token or SSH, and enable two-factor authentication.

---

# Diff

## set difftool with config file

```shell
 git config --global -e
```

> text to add

[core]  
`editor = code --wait`

[diff]  
`tool = vscode`

[difftool "vscode"]  
`cmd = code --wait --diff $LOCAL $REMOTE`

[merge]  
`tool = vscode`

[mergetool "vscode"]  
`cmd = code --wait $MERGED`

## set default editor

```shell
git config --global core.editor 'code --wait'
git config --global core.editor 'code --wait --new-window'
```

## unset

```shell
git config --global --unset core.editor
```

## default tool

```shell
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```

## default merge

```shell
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
```