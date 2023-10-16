# Running a Node.js web site in production (a beginners guide)
In this post I describe my experiences taking my first Node.js website to production, running it on port 80, and hosting it outside my local box so that it's available to the world wide web. The site in question is the site where you are reading this post and it can be described as a typical low-traffic website that uses Node.js, Express.js, and CoffeeScript.

Although I have deployed to production many C# web sites on Windows before, *this is the first time that I host anything in a Linux environment*. Keep this is in mind as you read this blog post.

**Update:** See also [part II of this blog post with my experiences 12 months later](https://hectorcorrea.com/blog/running-a-node-js-web-site-in-production-part-2/53).


## Chosing a Hosting Provider Model

When hosting a Node.js site with a third party provider there are basically two models. 

One hosting model is called **Infrastructure as a Service (IaaS)**. In this model, the hosting company owns the hardware but you are in charge of pretty much everything related to software, including operating system upgrades, security, web server, et cetera. Pretty much any Linux provider that support Linux VPS falls into this category. 

The second hosting model is called **Platform as a Service (PaaS)**. In this model, the hosting company owns the hardware and takes care of most of the software elements (e.g. operating system, web server, security, et cetera). PaaS companies provide you with tools so that you can push your code and configuration files to them and pretty much they take it from there. Examples of companies that use this model are [nodejitsu](http://nodejitsu.com) and [Heroku](http://www.heroku.com). They both support Node.js natively.

In my research I found that most companies that provide traditional and cheap Linux hosting for websites support websites in PHP, Python, and Ruby out of the box but they do not support Node.js. In order to host a Node.js site you need to find companies that provide "Linux VPS" plans and those plans tend to be not very cheap. The lack of cheap Node.js hosting in most traditional Linux hosting companies was somewhat of a surprise to me, but I suspect this is because Node.js is not quite mainstream yet.

In my case I chose an Infrastructure as a Service (IaaS) model to host my site because I wanted to get my hands dirty with all the steps involved in hosting a Node.js website. In particular I am using a Linux Cent OS machine on the [Windows Azure](http://windowsazure.com) cloud to host my site. To my surprise, Windows Azure provides very good Linux VPS plans at reasonable prices and with 3 months free trial period. Oh the irony! ...hosting a Linux machine on the Microsoft Windows Azure. 

To keep things interesting and to help with my learning process, I decided to use Node.js as the web server without putting Apache or Nginx in front of it. There are some advantages to using Apache or Nginx but in my case I wanted to use Node.js all throughout and without any intermediaries.

Although using an IaaS provider is great as a learning exercise, long term I will probably switch to a PaaS service (like nodejitsu or Heroku) where I don't need to worry about any of the infrastructure stuff.


## Running on Port 80

The first issue that I ran into when trying to run my site in a production environment was that in Linux (and Mac OS X) port 80 is reserved for system administrators (root user). As [this post on serverfault indicates](http://serverfault.com/questions/112795/how-can-i-run-a-server-on-linux-on-port-80-as-a-normal-user), this is true for any port below 1024.

Let's take for example the canonical web server example in Node.js but force it to listen for HTTP requests on port 80:

```code
var http = require("http");
var port = 80;
var serverUrl = "127.0.0.1";
console.log("Starting web server at " + serverUrl + ":" + port);

http.createServer( function(req, res) {

  timestamp = new Date();
  console.log("Request for URL " + req.url + " received at " + timestamp);

  if (req.url === '/error') {
    console.log('Throwing an error');
    throw "Oops";
  }

  res.end("Hello World " + timestamp);

}).listen(port, serverUrl);
```

If we save this file as *webserver.js* and run as a non-root user by issuing `node webserver.js` we'll get *"Error: listen EACCES"*. If the port was anything above 1024 (say port 8080 or 3000 as in most Node.js examples) then it would have worked OK.

A quick way around this problem is to run node webserver.js as a root user via sudo: `sudo node webserver.js`

Since we are using `sudo` the operating system will ask you to enter your root password before the command is accepted. After this the site will be running and available on port 80.

Also, since we are using sudo to run this command we need to remember that the PATH is the one assigned to the root user and very likely different from the PATH for a normal user account. This could be problem if Node.js is not in the PATH for the root user. You can specify a full path to Node.js when you issue the `sudo /usr/local/bin/node webserver.js` or change the PATH for the root user (via `visudo`) to include the path where node was installed (e.g. `/usr/local/bin`).

In my particular case, since my application is a CoffeeScript application I needed to be sure that both, Node.js and CoffeeScript, were on the PATH so I ended up altering the PATH for the root user via `visudo`. I believe the steps for this vary from Mac OS X to Linux and even among Linux distros but a quick search on the web should help you with the specifics for your environment.

As noted in the serverfault link mentioned above, instead of using elevated permissions to run on port 80, another option is to configure your Linux system to redirect traffic to port 80 to your site running in a different port. For example keep your site running on port 8080 but configure port 80 to redirect all traffic to port 8080. I did not try those steps, though.


## What Happens When Your Site Crashes?

Another topic to address when hosting a production site is what happens when the site crashes. For example, visiting the `/error` in our sample *webserver.js* will throw an exception. This will effectively stop our web site. How do we restart the site automatically after a crash?

Enter forever. *Forever is a tool that monitors your application and relaunches it as soon as it detects that is not running anymore* (e.g. as soon as your site crashes.) This tool was developed by the guys from nodejitsu and it's open source. You can find instructions on how to use it [here](https://github.com/nodejitsu/forever#readme).

To run our simple webserver.js with forever we could use the following command:

```terminal
sudo forever start -a -l forever.log -o out.log -e err.log webserver.js
```

The log files indicated in the previous command (forever.log, out.log, and err.log) is where forever will redirect its own log information, the standard output, and the standard error respectively. This is important because once you run your program with forever it runs on the background and you won't see any of its output in the console. For example, the timestamp log lines that our webserver outputs will be logged to the `out.log` file rather than the console.

If you hit the site a couple of times in your browser and then view the out.log file (e.g. with `cat out.log`) you'll see the successful requests, the ones that threw the exception, and the ones where the server was restarted. Notice that if you request `/error` you won't get a response in your browser but the site will be re-launched automatically and a request to / immediately after will work as expected.

For example, below is what the `out.log` file will log after a sample run on my box. As you can see I started the server and submitted two requests to `/` and then one to `/error`. Notice how immediately after throwing the error the site was automatically restarted and therefore it responsed OK to the last to request to `/`.

```
Starting web server at 127.0.0.1:80 at Tue Dec 04 2012 23:28:05 GMT-0500 (EST)
Request for URL / received at Tue Dec 04 2012 23:28:10 GMT-0500 (EST)
Request for URL / received at Tue Dec 04 2012 23:28:11 GMT-0500 (EST)
Request for URL /error received at Tue Dec 04 2012 23:28:14 GMT-0500 (EST)
Throwing an error
Starting web server at 127.0.0.1:80 at Tue Dec 04 2012 23:28:14 GMT-0500 (EST)
Request for URL / received at Tue Dec 04 2012 23:28:19 GMT-0500 (EST)
Request for URL / received at Tue Dec 04 2012 23:28:21 GMT-0500 (EST)
```

You can stop the site running on the background with the following forever command: `sudo forever stop webserver.js`


## What Happens When the Machine Reboots?

Now that the site is able to restart automatically when it crashes the last thing to address is to handle restarting the site automatically when the machine reboots. For that we need to write an `init.d` shell script. These are special shell scripts that get automatically executed when the machine reboots. As I indicated at the beginning of this blog post this was all new to me since I am new to Linux but there is plenty information on the web to create and configure an `init.d` script.

The details on how to create and configure an `init.d` script are beyond the scope of this blog post but the gist of it is as follows: Create a shell script (say `forever_init.sh`) and save under `/etc/init.d`. In the *start section of the shell script* include the line to call forever:

```code
forever start -a -l forever.log -o out.log -e err.log /path/to/your/app/webserver.js
```

Since `init.d` scripts are run as root user you won't need to use sudo when running forever. However you do need to make sure that Node.js is in the PATH for the root user. Likewise, when the machine reboots it won't be on the directory where you application lives. You'll need to make sure you fully qualify the path to webserver.js or switch to the application directory before the call to forever.

In the *stop section of the shell script* include a line like the following:

```code
forever stop webserver.js
```

Lastly you need to run the `chkconfig` tool to indicate the operating system when this script should be run. The specifics might depend on your Linux distro but you can use [this page](http://support.suso.com/supki/CentOS_Init_startup_scripts) as a starting point if you are not sure about this. 

You can see my [full blown init.d shell script here](https://github.com/hectorcorrea/hectorcorrea.com/blob/master/etc/forever-initd-hectorcorrea.sh).  Be aware that my site is running with CoffeeScript (which in turn calls node) and that complicates matters a little bit but by and large the skeleton should be pretty similar to what you will end up with.


## Final Thoughts

As I indicated at the beginning of this post, one of my goals to host a site in an infrastructure as a service environment was to get myself familiar with all the steps required to run a website with Node.js. This was a bit complicated for me since I am new to Linux but I got it to work and learned a lot in the process. This process made me appreciate a whole lot more what a professional web server like Apache or IIS do behind the scenes for you while at the same time allowing me to see first hand how a light weight tool like Node.js can be used to host websites end to end.

Had I chosen a platform as a service company to host my site most of these steps would have been taken care for me. For example, when using nodejitsu they provide a command line tool that automatically packages your application and deploys it to their servers. You just have to issue something like `nodejitsu deploy` and voila. They copy the files to their servers, make a backup of your existing application, and deploy the new code for you. You can even rollback to a previous version with the push of a button. Those are really nice features and I am sure eventually I will move my site to a PaaS environment, but I am not quite ready for that yet.

**Update:** I ended up moving this site to [nodejitsu](https://www.nodejitsu.com). Nodejitsu offers Platform as a Service (PaaS) that is targeted for Node.js, it's incredibly easy to use, and reasonably priced.

**Update 2** See also [part II of this blog post with my experiences 12 months later](https://hectorcorrea.com/blog/running-a-node-js-web-site-in-production-part-2/53) in which I moved this site to Amazon's cloud (AWS).