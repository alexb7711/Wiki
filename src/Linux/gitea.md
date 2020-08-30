---
title: How to set up a Gitea Server
header-includes: 
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# git push results in "fatal: The remote end hung up unexpectedly"
If you are pushing a large commit, nginx is probably at fault here. A quick google search will first suggest that you type

```
git config --global http.postBuffer 157286400
```

Which doesn't fix the issue, but it does show the actual source of the issue. Once you do this, you should get an error that looks like:

```
error: RPC failed; result=22, HTTP code = 413
fatal: The remote end hung up unexpectedly 
fatal: The remote end hung up unexpectedly
```

This is due to nginx not allowing more than a certain amount of data pass at a time. To fix this, simply edit `/etc/nginx/nginx.conf` and add the line under `http`:

```
client_max_body_size 50m;
```

where 50m can be adjusted as needed. Save the document and reload nginx with something like `systemctl restart nginx`. After this, you should be able to push larger commits not problem!

# Sources
[Server Hang Error](https://confluence.atlassian.com/stashkb/git-push-fails-fatal-the-remote-end-hung-up-unexpectedly-282988530.html)
[HTTP code = 413 git error](https://stackoverflow.com/questions/7489813/github-push-error-rpc-failed-result-22-http-code-413#15021750)
