---
layout:     post
title:      "A real website"
subtitle:   "templates, content, and Jekyll"
date:       2015-01-20 08:00:00
author:     "René"
header-img: "img/post-bg-01.jpg"
---

<p>I have a personal homepage since 1995. For the past 5 years, I hosted my pages on Google Sites. In 2014, google changed many things and it was no longer easy to integrate my Google Site with my domain.</p>

<p>So I decided to not waste time on figuring out how to fix this problem with Google, but I created a new site from scratch. Since I am not a web developer, I had to steal a template and fill it with content. My first attempt was <a href="http://startbootstrap.com/template-overviews/clean-blog/">this template</a>.</p>

<p>I changed some pictures and some general configuration and in the end I got some nice pages. But everything was static! I want to blog about my projects and I thought that I needed something more powerful but I don't like to set up a full CMS. One day after the initial release, I switched to the Jekyll version of the template. You can find it <a href="https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll">on github</a>.</p>

<p>I had no idea what Jekyll was, since I am not a web developer. It turned out that it does exactly what I wanted: Jekyll renders static webpages out of templates and content files. I just have to modify the template files and for every blog post, I write a new content file. Jekyll creates the static HTML files that I upload to my ftp server (the same that I used in 1995). GREAT STUFF!</p>

<h2 class="section-heading">Getting started with Jekyll</h2>

<p>There is a quickstart guide on <a href="http://jekyllrb.com/">the Jekyll website</a>.</p>
<blockquote>~$ gem install jekyll
<br>~ $ jekyll new my-awesome-site
<br>~ $ cd my-awesome-site
<br>~/my-awesome-site $ jekyll serve
<br># => Now browse to http://localhost:4000
</blockquote>

<p>I tried it with my Mac and run into many problems. It turned out that my developer system had too many customisations. I had to set up a clean ruby system. And I never used Ruby before! <a href="https://deanpcmad.com/setting-up-a-ruby-on-rails-development-environment-on-mavericks/">This tutorial</a> helped me a lot. </p>

<p>There is also a nice video tutorial on Youtube:</p>
<iframe width="560" height="315" src="//www.youtube.com/embed/iWowJBRMtpc" frameborder="0" allowfullscreen></iframe>

<h2>A podcast?</h2>
<p>I love podcasts. I did the <a href="https://soundcloud.com/rene_bohne">fab lab audio podcast</a> some years ago, but the workflow was too time consuming. I like the podlove project and I just found out that Arne Eilermann integrated Podlove into Jekyll. Maybe I should create a new podcast? You can find his project called <a href="https://github.com/pattex/octopod">octopod on github</a>.</p>