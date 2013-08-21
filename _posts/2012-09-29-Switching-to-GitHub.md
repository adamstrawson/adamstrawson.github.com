---
layout: post
title: "Migrating from Self-Hosted Git to GitHub"
---

At [Create](http://create.net) we've had a few changes to how we handle our version control over the past year. When I first joined the company the team was using Subversion, I've never been a fan of Subversion so I suggested the move to Git, two of the key reasons for the move was that it's decentralized, and it's faster for larger repositories. 

For various reasons we decided to go self-hosted and ran a VM with git and used [GitLab](https://github.com/gitlabhq/gitlabhq) as an interface.

Recently we questioned ourselves as to why we would want to be hosting our own Git server, and why we wouldn't want to use a service like GitHub. And so, we agreed to shutdown our git VM and move to GitHub.

Below is the process I went through to migrate our existing projects, and I hope that it's useful to others too.

**1) Create the repositories.**

The first step was to create the various repositories on GitHub, this was probably the most time consuming since we have quite a few repositories. 

**2) Make sure you're tracking all the remote branches.**

If you run the below within a git directory, it'll loop through all the remote branches and sets up tracking locally.

This will allow us to push all branches wither you have them cloned or not.

	for branch in `git branch -a | grep remotes | grep -v HEAD | grep -v master`; do git branch --track ${branch##*/} $branch; done

**3) Mirror the repository onto GitHub.**

My preference was to use git push --mirror just to play it safe. This will mirror everything in the repository over to GitHub (Files, History, Commit Logs, everything)

	git push --mirror git@github.com:USERNAME/REPOSITORY.git

If you open the repository in GitHub you should now see everything ready to go.

**4) Switch over the remote URL to use GitHub.**

If you're happy that everything is now on GitHub, run the below to switch the remote URL to use GitHub

	git remote set-url origin git@github.com:USERNAME/REPOSITORY.git

And that's all you need to do.

GitHub is an amazing service, I have used it for the past few years on personal projects and I'm excited to be using it at work too.

If you have any suggestions or improvements to the above, please do [get in touch](http://adamstrawson.com/talk), or Tweet me [@adamstrawson](http://twitter.com/adamstrawson)

*Thanks to [Troy Harvey](https://twitter.com/troyharvey) for cleaning up the `for` cmd*
