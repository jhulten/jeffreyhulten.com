--- 
wordpress_id: 7
layout: post
title: Using Subdomains as Account Keys
wordpress_url: http://tragicallyleet.com/2006/06/07/using-subdomains-as-account-keys/
---
I looked all over for an explanation on how to use the domain or subdomain as the account key (a la campfirenow.com) and now I have it...<!--more-->

All it takes is putting the following in the application controller.
<pre lang="ruby">
attr_writer :account   
attr_reader :account     
before_filter {|c| 
  c.account = Account.find_by_subdomain(
    c.request.subdomains.first
  )  
} 
</pre>
Then you can use it in any controller as follows:

<pre lang="ruby">
class BlogController < ActionController::Base   
  def index     
    render_text account.subdomain   
  end 
end 
</pre>
Check it out <a href="http://wiki.rubyonrails.com/rails/pages/HowToUseSubdomainsAsAccountKeys">here</a>...
