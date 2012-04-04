---
title: Installing MacVim with Ruby support and Command T on OSX Lion
slug: installing-macvim-with-ruby-support-and-command-t-on-osx-lion
author: paul_wittmann
published: true
author_name: paul
author_email: paul@railslove.com
author_url: http://
wordpress_id: 1119
wordpress_url: http://blog.railslove.com/?p=1119
published_at: 2011-10-17 19:21:31.000000000 +02:00
categories:
- railslove
- vim
---
When I set up my new Macbook Air recently, I ran into some unexpected problems setting up MacVim - mostly related to Ruby versions linked against MacVim and the Command T plugin. Here are some notes that might help you.

<em>Note</em>
In case you wonder: MacVim uses it own separate version of vim (installed here: /Applications/MacVim.app/Contents/MacOS/Vim), which is not linked against your own /user/local/bin/vim (or wherever your vim resides), which you or your package manager installed separately. The reason I'm mentioning this is that if you lack Ruby support in MacVim, compiling vim by hand won't help, since MacVim doesn't use it.
<h2>Howto</h2>
<ul>
	<li>activate your favourite version of Ruby via RVM or rbenv.</li>
</ul>
in my case:
$ ruby -v
ruby 1.9.2p290 (2011-07-09 revision 32553) [x86_64-darwin11.0.1]
<ul>
	<li>run (in case you haven't already, download and install the excellent <a href="http://mxcl.github.com/homebrew/">Homebrew</a>):</li>
</ul>
$ brew install macvim

* start MacVim with
$ mvim
run :version and make sure it lists +ruby (instead of -ruby)
test Ruby support by invoking
:ruby nil[]
which should return a NoMethodError
<ul>
	<li> $ mkdir ~/.vim</li>
</ul>
<ul>
	<li> install <a href="http://www.vim.org/scripts/script.php?script_id=2332">Pathogen</a> (better management of vim plugins, each living in its own subfolder inside ~/.vim/bundle)</li>
</ul>
&nbsp;
<ul>
	<li>to install <a href="https://github.com/wincent/Command-T">Command T</a>:</li>
</ul>
$ cd ~/.vim
$ git submodule add git://git.wincent.com/command-t.git bundle/command-t
$ git submodule init
$ git clone git://git.wincent.com/command-t.git bundle/command-t
<ul>
	<li>with the <strong>same</strong> version of Ruby activated you used to install MacVim (Ruby 1.9.2p290 in my case), run:</li>
</ul>
$ cd ~/.vim/bundle/command-t
$ rake make

more details in section 4 "MANAGING USING PATHOGEN" of: <a href="https://github.com/wincent/Command-T/blob/master/doc/command-t.txt">https://github.com/wincent/Command-T/blob/master/doc/command-t.txt</a>
	<li>create a symlink under Applications:
$ ln -s /usr/local/Cellar/macvim/7.3-62/MacVim.app /Applications/MacVim.app&nbsp;
<h2>Troubleshooting</h2>
<em>1) Lacking Ruby support inside MacVim</em>
<span style="text-decoration: underline;">Symptom:</span> Plugins written in Ruby, like Command T or Lusty Juggler, don't work.
Check: $ mvim --version or :version inside of MacVim should list "-ruby", if your version lacks Ruby support ("+ruby" if it has Ruby support built in).
<span style="text-decoration: underline;">Cause:</span> This happens when your version of MacVim was compiled without the --enable-rubinterp flag. This usually happens when you install a binary off MacVim's Google Code Project.
<span style="text-decoration: underline;">Remedy:</span> Best use Homebrew to install MacVim from source. Although the Homebrew command's output does not explicitly list the --enable-rubyinterp flag, you should be fine and :version should list +ruby.

<em>2) Can't compile MacVim or vim</em>
<span style="text-decoration: underline;">Cause:</span> You probably didn't install Xcode. Unfortunately you need proprietary Cocoa headers for MacVim, which are not included in this Kenneth Reitz' GCC OSX installer (<a href="https://github.com/kennethreitz/osx-gcc-installer">https://github.com/kennethreitz/osx-gcc-installer</a>; cf. related problem: <a href="https://github.com/mxcl/homebrew/issues/7576">https://github.com/mxcl/homebrew/issues/7576</a>).
<span style="text-decoration: underline;">Remedy:</span> Install the full Xcode package via Apple's App Store. Make sure to check your Launchpad for download activity - it took me half an hour to figure out that the app store's Install button was actually doing something and not broken.

<em>3) Command T complains about lacking C extensions</em>
<span style="text-decoration: underline;">Symptom:</span> Command T doesn't start and informs me about missing C extensions.
<span style="text-decoration: underline;">Remedy:</span> run rake make inside ~/.vim/bundle/command-t

<em>4) Command T causes SIGTERMS</em>
<span style="text-decoration: underline;">Symptom:</span> After having compiled Command T's C extensions, as soon as you try to invoke Command T inside MacVim, it causes the program to crash with a SIGTERM exception.
<span style="text-decoration: underline;">Cause:</span> Usually the reason for the SIGTERM is that your MacVim was compiled with a link to a different version of Ruby than Command T. However, I encountered the same problem when linking everything against system Ruby (1.8.7 in my case).
<span style="text-decoration: underline;">Remedy:</span> Be very careful about your RVM/rbenv settings and ensure the exact same version of Ruby is active when you compile MacVim (installing via Homebrew triggers a compilation process) or Command T. My issue was resolved by using Ruby 1.9.2 instead of system Ruby.</li>
<h2>Resources</h2>
<ul>
	<li><a href="https://github.com/ralph/dotvim">https://github.com/ralph/dotvim</a> Ralph's .vim files - certainly more well-honed and better organized than my own.</li>
	<li><a href="https://github.com/paulwittmann/vimrc-osx">https://github.com/paulwittmann/vimrc-osx</a> my current .vimrc & plugins on OSX. Still lacking some features, but more cleaned up than my <a href="https://github.com/paulwittmann/vimrc">old one</a> for Ubuntu.</li>
</ul>
