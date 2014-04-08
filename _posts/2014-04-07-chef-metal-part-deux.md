---
layout: page
title: "Chef-Metal in example"
date: 2014-04-07 00:34:20 -0800
author: Ryan Lewon
categories: [chef-metal, ruby] 
---

Well it's now time I show you the awesomeness of chef-metal which John Keiser and the opscode team have been working on.

The tool itself is great, allowing you to use chef as a bootstrap source for your baremetal in the cloud. The configuration is basic and too the point. Below are the example files I partially built for you to get up a chef-metal session and go.

Install chef-metal, easiest way is to simple just let chef install it, as you can see in chef-metal/recipes/default.rb below, i use the chef_gem package method to install the gems required.

Next we create both of the cookbooks below, obviously the templates are shown below, you can copy and paste them if you wish or modify them at will. Once you've create these directories you can easily run chef metal. Note, with the config below, you will be creating a node/client on the chef server, if the install fails or you are unable to access the machine, you will have to delete them manually afterwords.

To run chef-metal, just type the following
{% highlight bash %}
chef-client -z -o chef-metal,app
{% endhighlight %}

You'll notice the -z flag there, that's chef-zero at it's finest, that's another topic all together, but a great feature nevertheless. The -o allows us to specificy which cookbooks to load, we specify chef-metal first, it's essentially our libraries. We then specify app, our app with the default recipe and off it goes. This should, if you've configured the cookbooks/app/recipes/default.rb file correctly, bootstrap a node! Also note that the file demonstrated was for VPC with no public ip addresses, hence the "subnet_id," which is just an extension of Fog. As well, you can specify all kinds of pre-defined config options from fog in that same spot and pass them off to the host.

So we setup our provisioning cookbook with the corresponding recipe:

<h5>STRUCTURE::</h5>
{% gist xorl/94d1d196ab51238fd192 gistfile1.txt %}

<h5>CODE::</h5><br />
<h6>cookbooks/chef-metal/recipes/metadata.rb</h6>
{% gist xorl/94d1d196ab51238fd192 metadata-app.rb %}

<h6>cookbooks/chef-metal/recipes/default.rb</h6>
{% gist xorl/94d1d196ab51238fd192 recipe.rb %}

<h6>cookbooks/app/recipes/metadata.rb</h6>
{% gist xorl/94d1d196ab51238fd192 metadata-chef-meta.rb %}

<h6>cookbooks/app/recipes/default.rb</h6>
{% gist xorl/94d1d196ab51238fd192 site.rb %}
