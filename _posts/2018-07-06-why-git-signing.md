---
layout: post
title: "git signing Why ?"
description: "Why you should sign your commits."
tags: [git]
---

> Learning-by-doing is a concept in economic theory by which productivity is achieved through practice, self-perfection and minor innovations. - Wikipedia

Have you ever noticied this `Verified` badge to the commits on GitHub ?  
{% include image.html path="blogimages/verified.png" path-detail="blogimages/verified.png" alt="verified" %}
The first thing that came to my mind when I saw the badge was, _What's the point for doing that ?_ And while experimenting, I found that by just changing my git config to any other name and email, all the commit I do thereon will be show the changed name and email, and pushing those commits on server (GitHub or any other service) will also show the changed name and email. For example, I change name and email in config as follows:
{% highlight shell %}
$ git config --local user.name John
$ git config --local user.email john@example.com
{% endhighlight %}  
And now after making some messy changes and commiting them in the repository. This will be shown in the commit details.
{% include image.html path="blogimages/inValidCommit.png" path-detail="blogimages/inValidCommit.png" alt="inValidCommit" %}
If I push it to GitHub using _my_ account credentials, GitHub will still show the author name as `John <john@example.com>` and **not** my actual one i.e. `Akash Jobanputra <akash.jobanputra@hotmail.com>`. This way commits can be forged by anyone. That's what made me go through the process of creating keys, adding them to your github profile, and then using them to sign my commits by entering the passphrase. Because without commit signing, there is no way to verify that the original author is the author in commit details. But with commit signing, these forged commits cannot be signed because the forger does not have the the original author's private key.

Click here to know <a href="/posts/git-signing" target="_blank">How to create key and sign your commits</a>