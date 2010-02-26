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
    posts.each do |post|
      post_data = post.to_liquid
      html << <<-HTML
        <li><a href="#{post_data['url']}">#{post_data['title']}</a>
           &raquo; <abbr>#{post_data['date'].strftime("%d %b %Y") }</abbr>
      HTML
    end
    File.open("tags/#{category}.html", 'w+') do |file|
      file.puts html
    end
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

task :require_input do
  begin
    require 'highline/import'
  rescue LoadError => e
    puts "\n ~ FATAL: highline gem is required."
    exit(1)
  end
end

task :build => [:tags]

task :default => [:serve]

