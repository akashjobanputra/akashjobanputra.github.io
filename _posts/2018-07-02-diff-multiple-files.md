---
layout: post
title: "how to see differences between files"
description: "For analysing difference between 2 or more files."
tags: [vim]
---

Have you seen the file differences git shows between WIP and the last commit file ? Easiest way to analyse the differences. I like the way VSCode shows the diff, _damn so neat_. Being VSCode user, I first tried to open diff in it and found that VSCode does not display diff between more than 2 files. **ლ(ಠ益ಠლ)**  
Still, to see diff between 2 files using VSCode you can use hit the below command:
{% highlight shell %}
$ code --diff file1.txt file2.txt
{% endhighlight %}

**vim**diff to the rescue, for difference between 2 or more files you can use below command:
{% highlight shell %}
$ vimdiff file1.txt file2.txt file3.txt
{% endhighlight %}
### Result:
{% include image.html path="blogimages/multiDiff.png" path-detail="blogimages/multiDiff.png" alt="vimdiff" %}

### Bonus:
If you want to share the diff to others, you can export it in HTML Format too. Press `Esc` key, type `:TOhtml` and hit `Enter`. This will create an HTML file and will display its code, to save it press `Esc`, type `:wqa` and hit `Enter` This will place Diff.html in the working directory and exit from vimdiff.
#### HTML Result:
{% include image.html path="blogimages/TOhtmlDiff.png" path-detail="blogimages/TOhtmlDiff.png" alt="vimdiff :TOhtml" %}

