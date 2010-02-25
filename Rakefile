def jekyll(opts = "", path = "")
  sh "rm -rf _site"
  sh path + "jekyll " + opts
end
 
desc "Build site using Jekyll"
task :site do
  jekyll
end
 
desc "Serve on Localhost with port 4000"
task :serve do
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

task :default => [:tags, :serve]

