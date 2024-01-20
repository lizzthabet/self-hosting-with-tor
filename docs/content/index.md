+++
title = '✨ skillshare is an exercise in imagination ✨'
type = 'docs'
+++

# *Self-hosting websites with Tor*

A developing guide to homemade internets using open-source & privacy-centric tools

---

#### What is Tor?
[Tor](https://torproject.org/) is an open-source, privacy-centric tool for accessing information anonymously over networks. It's used [around the world](https://metrics.torproject.org/) to circumvent censorship and obscure information from third-party data collection and tracking. Much of the Tor network infrastructure is volunteer-run and operates on a model of distributed trust.<!-- define or go into detail here: what's this term mean? -->

At its simplest, the way Tor[^1] works is by routing network requests through a series of proxies that help obscure the identity of the computer that's making the request. It makes your internet traffic more anonymous by obscuring your computer's IP address from your Internet Service Provider (ISP) and the websites you visit.

Onion websites (also called *hidden services* or *onion services*) are websites that can only be accessed through using the Tor network. This is what this guide will focus on. Onion services allow the computer that's hosting the website content&mdash;not just the computer accessing it&mdash;to also remain anonymous while they're communicating.

<!-- TODO: Add more detail to this explanation, and make sure footnote markdown works -->
[^1]Tor is different than BitTorrent, which is a file-sharing protocol that allows people to host, or seed, content as they access it. It's also really neat! But this guide won't cover it.

#### Why self-host?
Self-hosting generally refers to hosting and maintaining applications on your own servers, instead of renting time or space on servers run by cloud providers, like Amazon Web Services. This guide borrows ideas from the [handmade web](https://luckysoap.com/statements/handmadeweb.html) and focuses on self-hosting as the practice of running a website from a computer that you own or share on a local scale.

In [*The Real World of Technology*](https://archive.org/details/the-real-world-of-technology/), Ursula M. Franklin outlines how technologies often begin with promises of liberation from their creators (or perhaps more accurately, their profiteers), but as technologies become more widely adopted and standardized, they often restrict choice, exert control, and provide new surfaces for exploitation.
<!-- Like how the automobile and the disappearance of public railroad infrastructure, like the sewing machine and the rise of sweatshops -->

Self-hosting is one strategy for resisting the narrowing of the internet, of digital commons, and of centralized cloud infrastructure, whether that's driven by for-profit companies, or nation-states that seek to control the flow of information. 

Self-hosting gives us more ownership of our own infrastructure, data, and services, where we can run the kinds of resources that we want and need for ourselves and our communities. It's a site for agency and reclamation.

Lastly, self-hosting is also a site of joy, imperfection, learning, and slowness, where we can play in the [dirt of the internet](https://techlearningcollective.com/2019/07/22/want-to-get-good-with-computers-dont-start-with-code.html).

<!-- A kind of conclusion sentence, linking to other resources, or ...? -->

#### What does Tor offer for self-hosting?
There are many ways to host your own websites. Tor is only one of them! I've found Tor specifically useful, because:
  * You don't need to configure your home router or worry about a firewall. Tor does something called NAT hole punching out-of-the-box, which means you can easily run a website from your own machine that can be accessed outside of your local network.
  * You don't need a domain name or to configure DNS. Tor creates a unique hostname for your website and populates that information over its network.
  * You don't need to worry about exposing your IP address to the wider internet. Tor's onion routing makes it possible for other people to request access to your website while keeping your computer's address anonymous.

But it has some drawbacks, like:
  * It requires that people have a Tor client, like Tor Browser, to access your site
  * Tor may be intimidating to configure confidently, and accessible technical resources can be difficult to find
  * You might need a separate machine that's always on if you want your site to be available always

---

## *How-to guide*

This guide will walk you through running a website from your own computer that's accessible over the Tor network, which is called an *onion website*. It's focused on showing you how easy it is to self-host with Tor and doesn't cover topics like how to make a website or how to maintain your website infrastructure while using Tor. (But maybe you're curious and would like to request that this guide cover more topics!)

This guide is divided into two tracks:
  * a [**fast track**](#track-1-using-onionshare) where you use a helpful program called OnionShare. I like this track because it provides a straightforward interface for getting an onion site running quickly and customizing how it'll run.
  * a [**manual track**](#track-2-using-a-local-web-server) where you set up individual components and run the Tor daemon locally. I like this track because it helps people understand more of what's happening under-the-hood of an onion site. It requires that you have more programs installed locally and are comfortable running commands in a terminal.

<!-- TODO: (possibly) Explain onion urls and links -->

### Track #1: Using OnionShare

#### What you'll need
  * A website that you'd like to host
  * [Tor Browser](https://www.torproject.org/download/) ([onion link](http://2gzyxa5ihm7nsggfxnu52rck2vv4rvmdlkiu3zzui5du4xyclen53wid.onion/download/index.html)) so you can access onion websites
  * [OnionShare](https://onionshare.org/) ([onion link](http://lldan5gahapx5k7iafb3s4ikijc4ni7gx5iywdflkba5y2ezyg6sjgyd.onion/#download)) installed

#### Part 1. Set up a website to host

If you have files for a website that you'd like to host locally, go ahead and skip to the [next step](#part-2-start-your-onion-site-with-onionshare)! Just make sure they're in a single folder and everything in the folder should be available on the website.

If you don't already have a website that you'd like to host, or you'd like a sample website to try this guide with, you can download [a simple html file](https://github.com/lizzthabet/self-hosting-with-tor/blob/main/site/public/index.html) that's included alongside this guide on Github.

Click the "Download raw file" button in the file menu, and save it where you'd like all your website files to live.

#### Part 2. Start your onion site with OnionShare

1. Open OnionShare and go to the "Host a Website" option.

2. Click "Add files" or drag and drop the contents of the `public/` folder into OnionShare.

3. Make sure to check the option `This is a public OnionShare service`, and then click "Start sharing."

*Congratulations, you now have an onion site!*

Copy the `.onion` address so you can share it.

#### How to stop your onion site

When you're done with sharing your site files, click the "Stop sharing" button. That's it!

### Track #2: Using a local web server

This track follows the [Set Up Your Onion Service guide](https://community.torproject.org/onion-services/setup/) ([onion link](http://xmrhfasfg5suueegrnc4gsgyi2tyclcy5oz7f5drnrodmdtob6t2ioyd.onion/onion-services/setup/index.html)) from the Tor Project.

{{< hint info >}}
💡 Command line instructions in this section are macOS-centric, and I'm working on expanding them. (If you'd like to help me do that, reach out!)
{{< /hint >}}

#### What you'll need
  * A website you'd like to host
  * [Tor Browser](https://www.torproject.org/download/) ([onion link](http://2gzyxa5ihm7nsggfxnu52rck2vv4rvmdlkiu3zzui5du4xyclen53wid.onion/download/index.html)) so you can access onion websites
  * A way to run a web server locally, like nginx, apache, or python
  * The `tor` binary (also called *little-t tor*) so you can run an onion service locally. Follow the [installation instructions](https://community.torproject.org/onion-services/setup/install/) ([onion link](http://xmrhfasfg5suueegrnc4gsgyi2tyclcy5oz7f5drnrodmdtob6t2ioyd.onion/onion-services/setup/install/index.html)) for each OS.
    * For macOS, `tor` is most easily installed with Homebrew.
    * For Linux, instructions will vary based on your package manager.
    * For Windows, you'll need to download the [Tor Expert Bundle](https://www.torproject.org/download/tor/index.html) ([onion link](http://2gzyxa5ihm7nsggfxnu52rck2vv4rvmdlkiu3zzui5du4xyclen53wid.onion/download/tor/index.html)). There are detailed [instructions for Windows](https://miloserdov.org/?p=1839&PageSpeed=noscript) in the section titled "How to launch Tor on Windows" from Alexey Miloserdov.

#### Part 1. Set up a website to host

Download the sample files from the `/site` directory on [Github](https://github.com/lizzthabet/self-hosting-with-tor).

If you're familiar with the version control tool called `git`, you can clone the repository:

```sh
git clone https://github.com/lizzthabet/self-hosting-with-tor.git
```

The sample site files include:
*  A `/public` folder that includes all the website files that should be publically accessible
*  A `torrc` file used to configure the Tor daemon
*  An optional `nginx.conf`, if you choose to use Nginx as a web server

If you already have a website, you can copy your own website files into the `/public` directory and replace the existing `index.html` file.

{{< hint info >}}
💡 Search for the `TODO` comments in this directory to find all the changes you'll need to make to run the demo.
{{< /hint >}}

#### Part 2. Run a local web server
The next step is running a local static web server that will serve all the files in the `/public` directory. Below are examples using `python` and `nginx` using the sample configuration file in this repo.

You can also use another web server of your choosing, as long as it's serving content from `/public` and listening on port 3000.

Both code examples assume that you're running the command from the repository's root directory.

<!-- TODO: Add an explanation for why you'd choose one over the other, like how most macs come with python already installed, while nginx is a more secure and production-ready option -->

##### With python

```sh
python3 -m http.server --directory ./public 3000
```

##### With nginx

Update the `nginx.config` file on line 16 with the absolute directory of the `/public` directory on your computer. This is what my updated directory looks like:

```
root            /Users/lizz/Documents/self-hosting-with-tor/site/public;
```

{{< hint info >}}
💡 To get the directory path, you can copy the output of the `pwd` command, or you can run this command to copy the directory path to your clipboard:
```sh
pwd | pbcopy
```
{{< /hint >}}

Then, start the nginx server.
```sh
nginx -c "$(pwd)/nginx.conf"
```

*Note*: The path to the `nginx.conf` should be absolute, not relative to the directory that you're running the command from.

After starting your web server, verify that you can access the site by visiting `localhost:3000` in your browser. (Tor Browser won't connect to `localhost`, so use your default browser instead.) 

*It's important to verify that your local server is up and your website is accessible at this point, otherwise the following steps won't work.*

#### Part 3. Start your `hidden_service` site

Next, we'll configure and start a "location-hidden service" that will connect to your local web server and make it accessible over the Tor network.

A Tor service is configured through a `torrc` file, which is included in the sample website files. The default `torrc` file contains a lot of information about various settings with helpful comments about them. Don't be intimidated by the file size! You're welcome to read through the config to learn more about how to set up various parts of the Tor ecosystem, but here we'll focus on the two settings you'll need to run your onion site, (one of which you'll need to update).

In the `torrc` file, go to line 81. Replace the directory listed next to `HiddenServiceDir` with the `/site` directory. Then add `/hidden_service/` to the end of that path. On my computer, that looks like:

```
HiddenServiceDir /Users/lizz/Documents/self-hosting-with-tor/site/hidden_service
```

*Note*: The directory path should not point to your `/public` folder! The path listed in the `torrc` is where Tor will reference onion-specific metadata about your site that you'd don't want to expose publically. Tor will create the `/hidden_service/` directory with the correct permissions when it runs for the first time.

<!-- TODO: Add more detail about what's in this `hidden_service` folder and what it's doing -->

In your terminal from this directory, run:
```sh
tor -f torrc
```

Tor is now running! In this directory, you should see a new `hidden_service` folder that's been created. You can open up the `hidden_service/hostname` file to view your onion site address, or you can run this command to copy the address to your clipboard:
```sh
pbcopy < ./hidden_service/hostname
```

Open Tor Browser and navigate to your onion site's address. You should see the same website as what's being served on your `localhost:3000`.

*Congratulations, you have an onion site!*

#### Debugging possible issues

##### General questions

For general questions about running `tor` and its configuration, you can look at the `man` page, which contains helpful information about Tor options.
```sh
man tor
```
You can search the `man` page by pressing `/` and typing the term you're searching for. `n` will navigate forward in the search results, `p` will navigate backwards, and `enter` will exit the search. `q` will exit the `man` page.

##### The onion address isn't loading

First, verify that your website is accessible locally at `localhost:3000`. If it's not, then it won't be available over Tor, since Tor is routing network requests to your local server.

Second, check the log output of the `tor -f torrc` process you ran. If you see an error message in the logs, follow their instructions and investigate the specific error.

You can get helpful feedback about the validity of your configuration file by running:
```sh
tor -f torrc --verify-config
```

If both the web server and `tor` are running properly, double-check that you copied the onion address from the `hidden_service/hostname` file correctly.

If none of those solve the problem, it's possible that the onion site is taking a second to become available over Tor. Try accessing your site again in a minute.

#### Stop your `hidden_service` site

To stop Tor, navigate to the terminal session that Tor is running in. You should see logs from the Tor process running. Press `CTRL + C` in the terminal window to stop Tor.

Alternatively, you can find the process id and send a termination signal to `tor`. Here's one way to get the process id:
```sh
ps -ax | grep '\btor\b'
```

To quit Tor:
```sh
kill <process-id>
```

If you make a change to the `torrc` and need to reload the process, you can:
```sh
kill -s hup <process-id>
```

The manual page (accessible through `man tor`) lists additional signals that the `tor` process will handle.

---

## *About this guide*
This guide is part of a larger, work-in-progress workshop series on Tor that explores how power is distributed in networking infrastructure and invests in more playful, DIY internets.

Technology skillshare is an exercise in imagination, since understanding how technologies came to be and how they operate is an opportunity to understand that they're not inevitable or permanent.

There are real alternatives that exist in the world right now, which present avenues, both material and ideological, for disinvesting from present conditions and systems of harm. Tor gives us a real strategy for navigating privacy, surveillance, and censorship on the internet today, as well as models for distributed stewardship of network infrastructure. It's an incomplete and imperfect tool, where we can practice skepticism and technology critique, while actively resisting the search for technological saviors.

This series has been developed with support from many brilliant and kind collaborators and teachers from [Collective Action School](https://school.logicmag.io), the [School for Poetic Computation](https://sfpc.study), and [Tech Learning Collective](https://techlearningcollective.com).

### I'd love your feedback
Feedback is a gift. :) You can reach out to me over email [lizzthabet at proton dot me](mailto:lizzthabet@proton.me) or raise an issue or pull request on [Github](https://github.com/lizzthabet/self-hosting-with-tor), where the source code of this website lives.

I'm looking for collaborators, learning buddies, and places to practice teaching.

<!-- TODO: Add a survey link that makes it very easy for people to give feedback -->