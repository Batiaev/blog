---
layout: post
title:  "Chef installation"
date:   2015-11-11 12:07:00
categories: linux rsync ssh
---

### Install Chef DK 
{% highlight bash %}
wget https://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/12.04/x86_64/chefdk_0.10.0-1_amd64.deb
sudo dpkg -i chefdk_0.10.0-1_amd64.deb
chef verify
which ruby
echo 'eval "$(chef shell-init bash)"' >> ~/.bash_profile
sudo aptitude install git
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR EMAIL ADDRESS"
#Set up the chef-repo
mkdir -p ~/chef-repo/.chef
chef generate repo ~/chef-repo
chef generate app <APP_NAME>
{% endhighlight %}

### Install Chef Server
{% highlight bash %}
sudo apt-get install wget -y
wget https://packagecloud.io/chef/stable/packages/ubuntu/trusty/chef-server-core_12.2.0-1_amd64.deb/download
sudo dpkg -i chef-server-core_12.2.0-1_amd64.deb
sudo vim /etc/opscode/chef-server.rb
{% endhighlight %}

	server_name = "CHEF_SERVER_FQDN"
	api_fqdn server_name
	bookshelf['vip'] = server_name
	nginx['url'] = "https://#{server_name}"
	nginx['server_name'] = server_name
	nginx['ssl_certificate'] = "/var/opt/opscode/nginx/ca/#{server_name}.crt"
	nginx['ssl_certificate_key'] = "/var/opt/opscode/nginx/ca/#{server_name}.key"


{% highlight bash %}
sudo chef-server-ctl reconfigure
{% endhighlight %}
