---
title: Git autocomplete in bash on a Mac
slug: git-autocomplete-in-bash-on-a-mac
author: mike_poltyn
published: true
author_name: mike
author_email: mike@railslove.com
author_url: http://mike.poltyn.com
wordpress_id: 1178
wordpress_url: http://blog.railslove.com/?p=1178
published_at: 2011-11-25 11:24:44.000000000 +01:00
categories:
- railslove
---
I've been using Linux and bash for great chunk of time for web development, and it always had great features like autocomplete, that I didn't get by default on a Mac.

So, I've decided to take matters into my on hands, and leave a post for all those, who are also bugged by no git autocomplete in bash on a Mac.

Thankfully, git already <a href="https://github.com/git/git/blob/master/contrib/completion/git-completion.bash">has its autocomplete script</a>, so it's a matter of just two commands:

<script src="https://gist.github.com/1393106.js?file=bash-autocomplete-script"></script>

But I like to take it one step beyond. To save some keystrokes, I've added some aliases to my <tt>~/.gitconfig</tt>:

<script src="https://gist.github.com/1393106.js?file=git-aliases"></script>

Now I can tab on <tt>git co <branch_name></tt> and everywhere else I was used to on my Linux machine.
