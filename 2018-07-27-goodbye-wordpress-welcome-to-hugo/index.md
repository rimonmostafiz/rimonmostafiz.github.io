# Goodbye Wordpress, Welcome to HUGO

Do you notice anything new? <br>
Of course not. No one follows my blog and theme does not matter. :unamused:

A weeks ago, I moved this site over from [WordPress](https://wordpress.com/) to [HUGO](https://gohugo.io/)(a static site generator).
Also its now hosted to [Netlify](https://www.netlify.com/)(:free:)

This is my attempt to making everything more simple and content-focused. <br>
In this post, I will talk about some of my reasons for switching away from WordPress to a static site generator.<br>

I will discuss technical details in some future post. :smiley:

### Why I Ditch Wordpress :question:
I’ve been posting on this site for almost a year now. The entire site has been running on Wordpress. At first, I choose WordPress because it was easy(I thought) and popular.

**But that power and flexibility also comes at a cost.** <br>
For me, there’s a lot of bloats. Stuff I actually don’t need.
Plugins are often not well written. And Wordpress itself written in PHP :persevere:<br>
And then there’s speed. Or the lack thereof.

It's 2018 and who wants a slow website? <br>
The average page load time was 5-7 seconds :sob: and as we all know, site speed is essential for user experience. A slow website will even hurt your conversion rate.

I actually use this site to share my learning experiences with others. I want to document my learning. For me, I want to focus on writing.<br>
The writing was taking forever. The WordPress dashboard had become unbearably slow.

**I got tired of fighting the CMS defaults.**

### What and Why Static Site :question:

#### What exactly a Static Site :confused:
It is exactly what it sounds like. It takes a collection of content files(markdown in the case of Hugo) and generates the static HTML, CSS, etc. files that formats and displays that content.

This final content can then be hosted anywhere, without the need for server-side runtime support, such as Python/PHP/Go/Node/etc, because it does not require server-side processing :wink: to handle rendering the pages on the fly.

#### Simplicity :v:
A site generated using a static site generator is usually a combination of content written in Markdown and a theme. Writing in Markdown lets me **focus more on the content rather than formatting**.

Furthermore, I can write Markdown in my favorite editor. I am currently using Atom.
I am now able to edit locally. The default WordPress editor ties you down to editing online but Markdown can be written almost anywhere!

#### Security :closed_lock_with_key:
WordPress powers around 30% of all CMS-based websites on the internet.

**Being this popular does not come without some drawbacks.** The volume of users is especially appealing to hackers trying to steal information. As a result, WordPress websites are often the victim of security breaches. WordPress sites depend on databases to hold the site's content and databases are inherently vulnerable.

A static site does not have some of the security concerns that a WordPress site brings. Pure static sites do not rely on databases. So no security threat.

#### Maintenance :ghost:
In addition to keeping plugins up to date with a WordPress site, you will also want to store backups of your site in case anything happens.<br>
I am tired of updating Wordpress and its plugins every other day.

Static site needs Low maintenance efforts. No regular updates and backups required.
All I need to push my local changes to my github repository and Its live.

#### Speed :rabbit:
WordPress sites serve content to visitors by querying the database for the information for the page that the visitor is requesting. Once the information is retrieved, the server will also need to generate the page.

On the other hand, static sites already have all the content ready to serve as it was pre-generated before the visitor even typed in your domain in their browser.

Servers are great at serving static content so the visitor will be able to read your fantastic post even faster.

### Welcome to HUGO :heart:

![hugo-logo](https://raw.githubusercontent.com/gohugoio/hugoDocs/master/static/img/hugo-logo.png)

From [HUGO's](https://gohugo.io/) website <br>

> Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.

It’s written in Go (aka Golang) and developed by [bep](https://github.com/bep), [spf13](https://github.com/spf13) and [friends](https://github.com/gohugoio/hugo/graphs/contributors).

Hugo is a CLI (command line interface) based static website generator. :heart_eyes: <br>
Basically, you write a few HTML templates, put your CSS (and other assets) in a folder, write your content using _markdown_ and then run the `hugo` command in the terminal. Hugo Will then builds your entire website in static HTML - ready to upload.

So whenever I need to publish a new post, I simply run

    $ hugo new posts/post-title.md

command in terminal and start writing on my favorite editor.

I do not have experience with other static site generators but users have stated that Hugo's generation process is blazingly fast.<br>
Apparently, sites with hundreds of pages can be generated in less than a second. :scream:

Another benefit of Hugo is that you don’t need to futz with an in-browser editor while writing pages. <br>
Hugo comes with a built-in production-grade server, which provides developers the option of watching for any changes in content. When content changes, Hugo will render that content again, and also trigger an update of your local webpage by way of a connected WebSocket. <br>
I can sit comfortably within my code editor of choice, and write a post in markdown. Each time I save the file, my webpage immediately updates to reflect the changes.

### Results and Closing Thoughts :100:
I feel that Hugo fits the needs of my personal blog well and also makes writing content more enjoyable.<br>
So far I love it !!<br>
As the time of writing this post my homepage loads under `~0.87 ms` :heart_eyes:

There is something quite satisfying about having the source of my site is so tangible while being easy to update, and easy to deploy. <br>
I don’t have to worry about a database, or hosting, or Wordpress site and plugin updates. I don’t have to worry about security since there are no dynamic pages or Wordpress vulnerabilities to guard against. I don’t have to mess with backups and exports from a hosting service since I check my entire site into [github](https://github.com/rimonmostafiz/rimonmostafiz.com).

Please, let me know if you find anything broken, I would really appreciate it!

