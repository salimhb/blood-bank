---
title: How to clone a repository into another repository from a specific point
slug: clone-a-repository-into-another-repository-from-a-specific-point
author: mike_poltyn
published: true
author_name: mike
author_email: mike@railslove.com
author_url: http://mike.poltyn.com
wordpress_id: 863
wordpress_url: http://blog.railslove.com/?p=863
published_at: 2011-03-07 17:25:05.000000000 +01:00
categories:
- railslove
---
While working on our project I had to create a repository clone up until a specific commit. So, I began researching and after trial and error, I finally made it. Therefore, I thought I will share what I've done with the community, as copying a git repository is not the easiest task.

Below you will find git commands I used to do so, and below the code, quick explanation of the steps

<script src="https://gist.github.com/858599.js?file=git-clone.txt"></script>

First you have to initialize new git repository, then add both remote repositories: <ul><li>the one you want copy into as <em>origin</em></li><li>the one you want to copy from as <em>to-clone</em></li></ul>

Then you have to fetch and checkout <em>to-clone master</em> (or whichever branch you want to clone). By now you should be in a "detached HEAD" state. At this point you can do to the repository whatever you want, including discarding commits, reverting, commiting new changes, etc. You can also use external tools like <tt><a href="http://jonas.nitro.dk/tig/">tig</a></tt>.

So, before we do that, let's reset to the commit we want to copy the repository to. In my case, I wanted to do <tt>git reset --hard 83d81abc...</tt> The parameter <tt>--hard</tt> was necessary to remove commits made after this commit, so I could copy the repository without experimental commits made afterwards.

After you're done, use <tt>git checkout -b master</tt> to save the changes you've done under new branch <em>master</em> and now you're ready to push the changes to the new remote repository you want to copy to.

<tt>git push origin master</tt> makes it's first appearance here, and now you're set. The repository <em>to-clone</em> has been copied at specific point to <em>origin</em>. Hope that little tutorial will help somebody in the future!
