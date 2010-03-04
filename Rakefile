def jekyll(opts = "", path = "")
  sh "rm -rf _site"
  sh path + "jekyll " + opts
end
 
desc "Build site using Jekyll"
task :site => [:build] do
  jekyll
end
 
desc "Serve on Localhost with port 4000"
task :serve => [:build] do
  jekyll("--server --auto")
end
 
desc 'Generate tags page'
task :tags do
  puts "Generating tags..."
  sh "rm -rf tags/*"
  require 'rubygems'
  require 'jekyll'
  include Jekyll::Filters
  
  options = Jekyll.configuration({})
  site = Jekyll::Site.new(options)
  site.read_posts('')
  site.categories.sort.each do |category, posts|
    puts " - #{category}"
    html = "---\nlayout: tag\ntag: #{category}\ntitle: Posts in #{category}\n---\n"
    rss = "---\nlayout: tag_rss\ntag: #{category}\n---\n"
    posts.each do |post|
      post_data = post.to_liquid
      html << <<-HTML
        <li><a href="#{post_data['url']}">#{post_data['title']}</a>
           &raquo; <abbr>#{post_data['date'].strftime("%d %b %Y") }</abbr>
      HTML

      rss << <<-RSS
        <item> 
        <title>#{post_data['title']}</title> 
        <link>http://tragicallyleet.com#{post_data['url']}</link> 
        <comments>http://tragicallyleet.com#{post_data['url']}#comments</comments> 
        <pubDate>#{post_data['date'].strftime("%a, %d %b %Y %H:%M:%S -0800") }</pubDate> 
        <dc:creator>Jeffrey Hulten</dc:creator> 
        <guid isPermaLink="true">http://tragicallyleet.com#{post_data['permalink']}</guid> 
        <description>#{post_data['url'] }</description> 
        </item>
      RSS

    end
    sh "mkdir -p tags/#{category}"
    File.open("tags/#{category}/index.html", 'w+') do |file|
      file.puts html
    end
    File.open("tags/#{category}/feed", 'w+') do |file|
      file.puts rss
    end
    
  end
  puts 'Done.'
end

desc 'generate the tagcloud page'
task :tagcloud do
  puts 'Generating tag cloud...'
  require 'rubygems'
  require 'jekyll'
  include Jekyll::Filters

  options = Jekyll.configuration({})
  site = Jekyll::Site.new(options)
  site.read_posts('')
  
  html =<<-HTML
  <h3>Tag cloud</h3>
  <div style="text-align: center">
  HTML
  site.categories.sort.each do |category, posts|
    s = posts.count
    font_size = 10 + (s*1.5);
    html << "<a href=\"/tags/#{category}\" title=\"Postings tagged #{category}\" style=\"font-size: #{font_size}px; line-height:#{font_size}px\">#{category}</a> \n"
  end
  html << "</div>\n"

  File.open('_includes/tagcloud.html', 'w+') do |file|
    file.puts html
  end
  puts 'Done.'
end

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

desc 'publish an existing post' 
task :publish do
  puts "Doesn't do anything yet..."
end

desc 'upload site to host' 
task :upload => [:site, :rsync]

task :rsync do
  sh 'rsync -crpvz --delete -e ssh _site/* autolabs@web102.webfaction.com:/home/autolabs/webapps/tragic_staticblog'
  sh 'scp _site/.htaccess autolabs@web102.webfaction.com:/home/autolabs/webapps/tragic_staticblog'
end

task :require_input do
  begin
    require 'highline/import'
  rescue LoadError => e
    puts "\n ~ FATAL: highline gem is required."
    exit(1)
  end
end

task :build => [:tags, :tagcloud]

task :default => [:serve]

