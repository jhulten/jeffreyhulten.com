--- 
wordpress_id: 39
layout: post
title: Keeping Fixtures DRY in Trees
wordpress_url: http://tragicallyleet.com/2006/06/26/keeping-fixtures-dry-in-trees/
---
So I am working on a Rails project that revolves around an acts_as_tree using single table inheritence (STI).  I got tired REALLY quickly with figuring out what id to use for each parent_id field.  I figured that in the spirit of Don't Repeat Yourself I would come up with a DRY way to specify the parents that did not require reapplying the id's to the fixtures when I change things.

Since the YAML fixtures in ruby are parsed through eRb first, I thought I would give this a try.  I made a file called thing_data.yml with my fixtures like so:

<pre lang="yaml">
root:
  name: root item
  parent_id:
first_branch:
  name: a branch
  parent_id: root
second_branch:
  name: another branch
  parent_id: root
a_leaf:
  name: a leaf on the wind
  parent_id: first_branch
</pre>

Notice the utter lack of ids.  Now with a little eRb magic we put the following in the yaml file you plan to load as your fixture.  Lets call it thing.yml:

<pre lang='ruby'>
<%

id_key = 1

data = YAML.load_file( 
  File.expand_path( 
    File.dirname( __FILE__ ) + '/test/fixtures/thing_data.yml'
  )
)

@final = Hash.new
data.each {|key, value|
  
  record = Hash.new
  
  record.update( value )
  record['id'] = id_key 
  record[ 'created_at' ] = Time.now.strftime("%Y-%m-%d %H:%M:%S")
  record[ 'updated_at' ] = Time.now.strftime("%Y-%m-%d %H:%M:%S")
  
  @final[ key ] = record
  
  id_key = id_key.next
}  

thing_ids = Hash.new

@final.each { |key, value| 
  thing_ids[ key ] = value[ 'id' ] 
}

@final.each { |key, value| 
  value[ 'parent_id' ] = thing_ids[ value[ 'parent_id' ] ] 
} 
%>
<%= @final.to_yaml %>
</pre>

To test, run <code>erb thing.yml</code> and see your output.  No more hand coding of ids and hoping you didn't put something in the wrong place!
