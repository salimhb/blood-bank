---
title: SMACSS and SASS - The future of stylesheets
slug: smacss-and-sass-the-future-of-stylesheets
author: jakob_hilden
featured_image: http://smacss.com/img/book-covers.png
published: true
author_name: jakob
author_email: jakob@railslove.com
wordpress_id: 1318
wordpress_url: http://blog.railslove.com/?p=1318
published_at: 2012-03-28 18:15:20.000000000 +02:00
categories:
- railslove
- rails
- oss
- css
- sass
tags:
  keyword:
  - smacss
  - sass
  - css
  - stylesheets
  - frontend
  - modular
  - conventions
---
I just had the the pleasure of attending the <a href="http://smacss.com/">SMACSS</a> workshop in Essen by Jonathan Snook (<a href="https://twitter.com/#!/snookca">@snookca</a>) and wanted to share my impression of the "SMACSS approach" to CSS and some considerations on using it together with <a href="http://sass-lang.com/">SASS</a>.
<h2><strong>Overview: The philosophy behind SMACSS
</strong></h2>
On a high level SMACSS aims at changing the way we are turning designs into code (here CSS+HTML).  Instead of working in a "<strong>page mentality</strong>" where you look at a single page's design and try to find the best way of turning that page into code, SMACSS advocates taking a step back and trying to identify repeating <strong>visual patterns</strong>. Those patterns are then supposed to be codified into flexible modules, which should be as independent as possible from the individual page context.  This might not sound so revolutionary from a programmer's point-of-view, but for the web design community this is indeed a new(er) way of thinking.  I myself kind of think of it as <em>"<strong>data modeling from the other side</strong>"</em> instead of trying to structure information (into e.g. a database schema) you are trying to structure visual design into a CSS module architecture.
<h4>Related Works</h4>
Even for CSS such an approach is not entirely new, but in my opinion SMACSS presents it in a very accessible (=> public website),  approachable and pragmatic way.  It has many basic ideas in common with the likes of <a href="http://oocss.org/">OOCSS</a>, <a href="http://csslint.net/">CSS Lint</a> and similar "modular CSS" advocates, but I would say it is less strict and "hardcore" about it.  For example, instead of saying "You should never ever use element selectors!", it rather advocates to keep them to a minimum, and still use them where it makes (semantic) sense.
<h2><strong>Concept of categorization</strong></h2>
The basic concept of SMACSS is to categorize styles into 4* categories: <strong>base</strong>, <strong>layout</strong>, <strong>modules</strong> and <strong>states</strong>.  Each category comes with a set of more ore less loosely defined <strong>naming conventions</strong> and <strong>usage rules</strong>.
<h3><strong>Base</strong></h3>
This is where things like CSS resets (if you use them), element defaults (e.g. link colors), default font sizes, etc. belong.  The category is largely dominated by element selectors.  However, you should always ask yourself "Is this base?" in order to not loose flexibility down the road.
<h3><strong>Layout</strong></h3>
This includes all types of layout containers such as header, footer, content, sidebar, etc.  The layout elements don't really have any styles of their own, but are simply containers.  Obviously, this is the layer where grid systems would be living.  All selectors in this category should be prefixed with <code>.layout-</code> (e.g. <code>.layout-header, .layout-sidebar</code>).
<h3><strong>Modules</strong></h3>
The bulk of (SMA)CSS is made up of independent modules and submodules.  Examples for modules could be things like: <code>search-box, dialog, navigation, menu, content-box</code>.  While submodules are more specific versions of these modules such as:  <code>dialog-wide, navigation-tabbed, menu-dropdown</code>.
The ideal module is completely independent of its context and should work within any layout container or other module.  If a specific context requires changes to a module you rather create a submodule that describes the context, instead changing styles based on the parent (e.g. <code>.content-box-narrow</code> instead of <code>#sidebar .content-box</code>).
<h3><strong>States</strong></h3>
Modules can have different types of states:  class-based states (<code>.is-hidden</code>), pseudo-classes (<code>:hover, :focus</code>), attribute states (<code>data-state=transitioning</code>), or @media query states.  These states belong right to the modules but have a separate category because they have their own naming convention and usage rules.
<h2><strong>The back-story behind SMACSS
</strong></h2>
I think there are two important things to mention in order to understand where SMACSS is coming from and where it makes most sense.  The first is about the role and team setup and the second about the type of product it is designed for.

SMACSS is designed for a "<strong>Prototyper</strong>" job description, who turns design comps into HTML+CSS, <strong>before</strong> they are passed on to the engineers.  If you have a less rigid, more agile developing process, where maybe one engineer works on both the front- and the backend (e.g. in a startup context), you probably need to cut some corners when implementing SMACSS. Also, the approach is ideally accompanied by a <strong>prototyping system/tool</strong>, where you create testing templates for each of the defined modules in order to visually test them - both on their own and within other modules and layout containers.  Jonathan Snook and his team at Yahoo were using such a custom build system for Yahoo Mail, but something like it yet has to be made publicly available for generic projects.  In my opinion this is a very interesting and promising direction to have <a href="http://en.wikipedia.org/wiki/Test-driven_development">TDD</a>-like tools for visual testing of frontend code.  Looking forward to that!

Secondly, the SMACSS approach was born out of experiences building Yahoo Mail and therefore it makes most sense for web <strong>"applications"</strong> and not so much for web <strong>"sites"</strong>.  The application ideally needs to consist of easily definable modules which are long-lived and appear in different contexts, otherwise creating proper SMACSS modules might just be overhead.  The same is probably true, for parts that are a little separate from the application and undergo a lot of design changes, such as landing pages or other ephemeral site areas.  Here it might not always make sense to modularize everything.
<h2><strong>SASS + SMACSS = ?
</strong></h2>
<h3><strong>Themes</strong></h3>
When I was talking about SMACSS having 4 categories earlier, I actually left out the 5th category which is "theme".  I did this because, when using SASS, theming can easily be handled by defining variables for the style properties that you want to be themeable (e.g. <code>$themable-border-color</code>), instead of having to apply special classes to all the themable elements (<code>.theme-border</code>).  Here at Railslove we just had to create a new theme (basically a re-branding with different colors) on short notice for our client <a href="http://9flats.com">9flats.com</a> and we were amazed how quickly we could complete this task on a SASS-based website, which would have taken much longer in "the old days".
<h3><strong>Submodules</strong></h3>
The best and most straightforward application of SASS functionality to the SMACSS approach is for submodules.  Whenever you need a variation of one of your modules, you are supposed to create a submodule, e.g. <code>.dialog-wide</code> is a submodule of <code>.dialog</code>.  While in traditional SMACSS you would need to apply both classes to your element (<code><div class="dialog dialog-weide" ></code>), using SASS you have the perfect use case for the (underutilized) <a href="http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#extend">@extend</a> feature and you would simply do it this way:

~~~css
.dialog
  width: 300px
  color: blue

.dialog-wide
  @extend .dialog
  width: 600px
~~~

The only thing you need to be aware of, is to never to extend across modules, which would violate the concept of SMACSS and could easily lead to unwanted side effects.
<h3><strong>Module component syntax</strong></h3>
One thing that I haven't quite made up my mind about is the syntax within modules.  SMACSS proposes that every component within a module should have a) its own selector (for performance) and b) be prefixed with the module name (for clarity). Like this:
<pre><code>.dialog
  width: 500px

.dialog-header
  font-weight: bold

.dialog-body
  font-size: 13px</code></pre>
This syntax is in some conflict with the way I have gotten used to authoring stylesheets with SASS, making heavy (sometimes too heavy) use of its nesting capabilities & syntax.  Using my traditional SASS style, it would probably look something like this:
<pre><code>.dialog
  width: 500px
  .header
    font-weight: bold
  .body
    font-size: 13px</code></pre>
I feel that all the prefixing adds a lot of distracting verbosity to the stylesheet and by nesting all the components underneath the module selector it actually gives it a nice visual closure.  The important requirement here is that you <strong>keep the component number and nesting depth of your module to a minimum</strong>.  But I think in this case applying the modular SMACSS philosophy is actually one of the best things that could happen to SASS, because the <a href="http://compass-style.org/help/tutorials/best_practices/">best practice</a> to minimize your nesting has been pushed too little and therefore been overlooked far too often by SASS practitioners.  However, the big downside with this approach is that you <strong>loose</strong> a lot of <strong>clarity</strong> in the markup, because now it's not obvious anymore to which module a component class such as <code>.header</code> belongs to.  One idea to alleviate this problem could be to have a more obvious naming convention for module selectors (e.g. <code>.<strong>module</strong>-dialog</code>), so it's easier to trace your way up in the markup from a component class to the next module selector it belongs to.

The other more minor downside of nesting would be the loss in <strong>CSS performance</strong> due to longer selectors caused by nesting.  However, unless you are not working on a super high performance website with massive reflows, lots of old browsers and complex mobile requirements, most  sources [<a href="http://calendar.perfplanet.com/2011/css-selector-performance-has-changed-for-the-better/">1</a>, <a href="http://bindle.me/blog/index.php/493/is-scss-killing-your-sites-performance">2</a>, <a href="http://www.thebrightlines.com/2010/07/28/css-performance-who-cares/">3</a>, <a href="http://www.stevesouders.com/blog/2009/03/10/performance-impact-of-css-selectors/">4</a>] make me believe that heavily optimizing for CSS performance, isn't really worth the effort, especially in a startup environment.

So, if we say that, on the one side we don't care so much about CSS performance and we do like the visual clarity of SASS nesting, but on the other side we also like the idea of always knowing which components belong to each other based on prefixes, a syntax like this could actually be a compromise:
<pre><code>.dialog
  width: 500px
  .dialog-header
    font-weight: bold
  .dialog-body
    font-size: 13px</code></pre>
If you then should start to worry about performance at some point you can easily convert to pure SMACSS.  However, I myself am not really sure yet what syntax I really prefer.  What do you think?

<strong>File structure</strong>

SMACSS already includes quite sensible naming conventions for selectors, but coming from the Rails/SASS world we obviously also value conventions for our file structure.  My suggestion for a SMACSS+SASS file structure would probably look something like this:
<pre><code>+ applications.sass                  // @imports
+ base/
|    _settings.css.sass              // SASS config variables
|    _reset.css.sass
|    _colors.css.sass
|    _fonts.css.sass
|    _element_defaults.css.sass
|    _form_defaults.css.sas
+ layout/
|    _settings.css.sass              // SASS layout/grid variables
|    _containers.css.sass
+ modules/
+ non-modular/</code></pre>
I guess there is nothing too surprising in there.  The only thing that I would add is the folder/area for <strong>non-modular</strong> styles.  As I said earlier there are always cases for pages/styles that are not very long-lived, not "fully baked", and so on.  Those should go to the non-modular folder.  Here it probably also makes sense to write highly specific (maybe even controller/view-specific) styles.  With that I would just want to prevent any half-assed styling attempts to bleed into the modular styles.  If styles in there last longer than expected, you can always go back and "graduate" them to proper SMACSS modules.

Concerning file structure there is a little <a href="https://github.com/pengwynn/dotfiles/blob/master/sass/sass.zsh">shell script</a> by Wynn Netherland to create a (much simpler) SMACSS folder structure for SASS, maybe this could be extended for further integration between the two.
<h3>Submodule vs. component syntax</h3>
The last little thing I want to talk about is a small issue I have with the SMACSS syntax and that is the indifference between the syntax for submodules vs. module components.  If you have for example a selector such as <code>.navigation-header</code>, this could either be a <strong>submodule</strong> of the <code>.navigation</code> module (submoduled for the header context), or it could be a <strong>component</strong> of the <code>.navigation</code> module assigned to the header element of the navigation.  It's not a big issue, but I nevertheless think it would be valuable to be able to discriminate the two on first sight.  Jonathan mentioned that a suggestion for differentiation, that was brought up, was to use two <code>--</code> vs. one <code>-</code> dashes, e.g. <code>.navigation--header</code> (I think for the component) vs. <code>.navigation-header</code> (for the submodule).  Not sure that this is the ideal solution, but I truly think that it would be very good being able to differentiate them.
<h2>tl;dr</h2>
SMACSS is a very user-friendly approach to modular CSS.  It asks for nothing less than a complete shift from a "page mentality" towards webdesign, to a search and codification of visual patterns.  For that it offers a concise and sensible categorization and naming scheme.
It generally goes along very well with SASS, especially using the @extend feature and when it comes to themeing.  It's kind of an open question how SASS's nesting capabilities fit with SMACSS, but in general I think it can bring lots of very valuable and badly needed modularity and conventions to the SASS/Rails community.
