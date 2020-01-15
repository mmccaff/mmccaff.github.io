---
layout: post
title: Secure Tunnels to Laravel Homestead Using ngrok
published: true
adsense: false
twitter_plug: true
---

Have you ever wanted to expose a local server behind a NAT or firewall to the internet? This can be useful when developing 
webhooks that require a public address. It can also be useful if you want to demo or get feedback on in-progress work that is on your
local development environment without a deployment. I recently used [ngrok](https://ngrok.com) to allow a product manager to try in-progress 
work that was hosted on my local Laravel Homestead environment. After getting past one gotcha that wasn't immediately obvious to me, it 
worked perfectly.

<!--excerpt-->

### Laravel Homestead

[Laravel Homestead](https://laravel.com/docs/5.4/homestead) is a "Vagrant Box", a pre-configured Ubuntu virtual machine that, using [Vagrant](https://www.vagrantup.com/), is automatically provisioned and configured to have all of the dependencies that are required to run a Laravel application. It also includes many useful utilities for a Laravel development environent. The virtual machine itself is usually referred to as Homestead.

### Serving Multiple Applications With Homestead

Homestead makes it easy to serve multiple applications from nginx using virtual hosts. It includes a shell script that automates creating a new conf
file for a new virtual host. The script is located at `/vagrant/scripts/serve-laravel.sh` and should already be in your path if logged into Homestead.
Note that in older versions of Homestead, this script was named serve.sh.

If I were starting a new application that I wanted to locally access at myapp.dev, I would run this command in Homestead to add the virtual host

<code>
	serve-laravel myapp.dev /home/vagrant/MyApp/public
</code>

This creates an `/etc/nginx/sites-available/myapp.dev` conf file which has a symbolic link to `/etc/nginx/sites-enabled/myapp.dev`. This is 
what configures nginx, our web server, to use /home/vagrant/MyApp/public as the document root for http requests to the myapp.dev virtual host.

Next, on my local macOS environment, I add a host record so that requests to myapp.dev don't perform a DNS lookup and instead go to the
Homestead guest machine.  That is done by adding a line like this to /etc/hosts/

<code>
	192.168.10.10   myapp.dev
</code>

What is 192.168.10.10, you ask? That is the default ip address of the Homestead virtual machine, which is defined by the line 
`ip: "192.168.10.10"` in ~/.homestead/Homestead.yaml.

### ngrok Pricing

Before running ngrok, I bought it and then installed it on my macOS.

ngrok offers [three pricing tiers](
https://ngrok.com/product#pricing) including a free plan. The setup that I am using requires the Pro plan because it uses both the
"Whitelabel domains" and "Custom subdomains" features. The Pro plan costs $8.25/mo billed annually, or $10/mo billed monthly.

### Running ngrok

*My first attempt almost worked.*

I ran this command from my local environment (the macOS host machine, not the Homestead guest VM) which tunneled traffic from the "whitelabel" mmccaff-myapp.ngrok.io domain to my local myapp.dev host over port 80.

<code>
	ngrok http -subdomain=mmccaff-myapp -host-header=rewrite myapp.dev:80
</code>

This only got me as far as being able to see the application's login page at mmccaff-myapp.ngrok.io from a remote machine. The problem was that any 
url rendered in a view of the application was fully qualified to myapp.dev instead of mmccaff-myapp.ngrok.io. This, of course, does not work for a remote 
user on another machine.


*My second attempt worked.*

It involved making an additional virtual host and host record for mmccaff-myapp.ngrok.io, and running a modified ngrok command.

In Homestead, I made a new virtual host configuration that was the same as myapp.dev's except for the server_name, linked the file,
and then restarted nginx
```
cd /etc/nginx/sites-available 
cp myapp.dev mmccaff-myapp.ngrok.io
edited mmccaff-myapp.ngrok.io to set 
   server_name mmccaff-myapp.ngrok.io;
cd /etc/nginx/sites-enabled
sudo ln -s \
../sites-available/mmccaff-myapp.ngrok.io .
sudo service nginx restart
```

In macOS, I added a host record for mmccaff-myapp.ngrok.io in /etc/hosts
```
192.168.10.10   mmccaff-myapp.ngrok.io
```

Finally, after the additional virtual host and host record were added, I was able to run this command

<code>
	ngrok http -subdomain=mmccaff-myapp -host-header=rewrite mmccaff-myapp.ngrok.io:80
</code>

The application worked perfectly from a remote machine visiting mmccaff-myapp.ngrok.io. The tunnel was to (and from) mmccaff-myapp.ngrok.io, which 
the local host record mapped to Homestead. Because remote requests matched the mmccaff-myapp.ngrok.io virtual host file, nginx set a server_name of mmccaff-myapp.ngrok.io and so the links in the application were correct.

When finished, use ctrl-c to exit ngrok and kill the remote tunnel.

There might be some scenarios where you'll want to change APP_URL in your Laravel .env file, but I did not find a need to do that.

### Replay Requests like Woa

While ngrok is running, try visiting `http://127.0.0.1:4040` in your web browser. This is amazingly useful when using webhooks, as you can
see what calls remote servers have made to your endpoints and even replay them.

From [ngrok's documentaion on inspection](https://ngrok.com/docs#inspect)

>ngrok provides a real-time web UI where you can introspect all of the HTTP traffic running over your tunnels. After you've started ngrok, just open http://localhost:4040 in a web browser to inspect request details.
>
> Try making a request to your public URL. After you have, look back at the inspection UI. You will see all of the details of the request and response including the time, duration, headers, query parameters and request payload as well as the raw bytes on the wire.


### A Possible Time-Saver

The latest version of Homestead now includes ngrok in the Vagrant Box itself, and is packaged with [a "share" command](https://laravel.com/docs/5.4/homestead#sharing-your-environment) that simplifies using it. If you are using the latest version
of Homestead, this is probably a preferable and easier way to share an application in your Homestead environment, but I haven't tried it
yet. 

### More Discussion

A funny coincidence, but the day after I had tried ngrok, it was on the front page of Hacker News. Not because there was any news about it,
it's been around for years, but because it is a cool utility that not everyone knows about.

There is a good discusion of ngrok and some alternatives [there](https://news.ycombinator.com/item?id=14278703). 
