---
categories:
- ruby
- rake
- jekyll
date: 2010-02-28T00:00:00Z
title: Moving my Blog to Jekyll
url: /2010/02/28/moving-my-blog-to-jekyll/
---

In the past I have not blogged very often. In fact I seem to blog less often than [Wordpress](http://wordpress.org/) releases a security patch. This was making me nervous and, combined with the issues of writing posts offline at events like NFJS, I decided a change was in order.

Enter [Jekyll](http://github.com/mojombo/jekyll), the static page blog generator behind [Github Pages](http://pages.github.com/). So far the workflow of managing text files in a Git repository is working well for me. Not being able to leave well enough alone I created a Rakefile to manage certain tasks like create a tagcloud for the sidebar, creating tag specific pages listing posts, and creating a draft post. 

Creating a draft post was pretty straightforward:

{{< highlight ruby >}}
desc 'create a new post in draft mode'
task :new => [:require_input] do
  title = ask("Title: ")
  filename = title.downcase.gsub(/[^a-z0-9]/,"-")
  template=File.read "lib/post_template.markdown"
  File.open("_drafts/#{filename}.markdown", 'w+') do |f| 
    f << template.gsub(/POST_TITLE/, title)
  end
  sh "git add _drafts/#{filename}.markdown"
end
{{< / highlight >}}

Publishing a draft to the blog will consist of a `git mv` of the draft file to the \_posts directory with the data appended to the filename.

As for comments I have switched over to Disqus, which allowed me to import my Wordpress comments and link to them on my Jekyll blog. 
