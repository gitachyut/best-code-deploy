# Best way to code deploy on any VPS using Git<br>
-------------- Server side Work --------------------- <br>

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
`#!/bin/sh`    
`git --work-tree=/var/www/html --git-dir=/var/repo/repo_name.git checkout -f`<br>
<br>

----------------- client side Work --------------------- <br>

## Inside The project dir initialize git and add new remote to your vps <br>
`git remote add live ssh://user@address/var/repo/repo_name.git`
`git push live master`
<br>

But Before all of these configuration set ssh-keygen features https://github.com/gitachyut/ssh-key-setup  


# One more way to code deploy the whole project (One Time Code Deploy)  
This is not step by step code deploy way it's one time code deploy. 

`
<?php  
	$Local_Root = "/home/site/web/findguwahati.com/public_html";  
	$App_name = "app";  
	$Local_repo = "{$Local_Root}/{$App_name}";  

	$Git_repo = "https://github.com/gitachyut/digital-git-deploy.git";  
	$Git_repo_name = "digital-git-deploy";  
	if(file_exists($Local_repo)){  

		shell_exec("rm -rf {$Local_repo} ");   
	}  

	echo shell_exec(" cd {$Local_Root} && git clone {$Git_repo} && mv {$Git_repo_name} {$App_name}  && git checkout master ");  

	die("dome");  
?>  
`


