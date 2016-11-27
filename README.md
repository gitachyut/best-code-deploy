# best-code-deploy
Best way to code deploy any VPS <br>
# Server side Work --------------------- <br>

## Create a Repo dir on the server <br>
`mkdir /var/repo` <br>
<br>
## Create a bare git repo inside `/var/repo` <br>
`mkdir repo_name.git`<br>
<br>
## Initialize the Bare git Repo `inside repo_name.git ` <br>
`git init --bare`<br>
<br>
## Now go inside  `hooks` dir and create a file `post-receive` <br>
`vim post-receive`<br>
<br>

## `post-receive` is bash file so  <br>
`#!/bin/sh 
git --work-tree=/var/www/html --git-dir=/var/repo/repo_name.git checkout -f`<br>
<br>

# client side Work --------------------- <br>

## Inside The project dir initialize git and add new remote to your vps <br>
`git remote add live ssh://user@address/var/repo/repo_name.git`
<br>

* But Before all of these configuration set ssh-keygen features
