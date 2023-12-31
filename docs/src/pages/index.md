---
title: ''
description: 'Self-hosting websites with Tor is a developing guide to homemade internets using open-source & privacy-centric tools'
hide_table_of_contents: true
---

# *Self-hosting websites with Tor*

A developing guide to homemade internets using open-source & privacy-centric tools

---

#### What is Tor?
[Tor](https://torproject.org/) is an open-source, privacy-centric tool for accessing information anonymously over networks. It's used [around the world](https://metrics.torproject.org/) to circumvent censorship and obscure information from third-party data collection and tracking. Much of the Tor network infrastructure is volunteer-run and operates on a model of distributed trust.<!-- define or go into detail here: what's this term mean? -->

At its simplest, the way Tor works is by routing network requests through a series of proxies that help obscure the identity of the computer that's making the request. It makes your internet traffic more anonymous by obscuring your computer's IP address from your Internet Service Provider (ISP) and the websites you visit.

Onion websites (also called *hidden services* or *onion services*) are websites that can only be accessed through using the Tor network. This is what this guide will focus on. Onion services allow the computer that's hosting the website content&mdash;not just the computer accessing it&mdash;to also remain anonymous while they're communicating.

<!-- TODO: Make this a small footnote -->
*Tor is different than BitTorrent, which is a file-sharing protocol that allows people to host, or seed, content as they access it. It's also really neat!

#### Why self-host?
Self-hosting generally refers to hosting and maintaining applications on your own servers, instead of renting time or space on servers run by cloud providers, like Amazon Web Services. This guide borrows ideas from the [handmade web](https://luckysoap.com/statements/handmadeweb.html) and focuses on self-hosting as the practice of running a website from a computer that you own or share on a local scale.

In [*The Real World of Technology*](https://archive.org/details/the-real-world-of-technology/), Ursula M. Franklin outlines how technologies often begin with promises of liberation from their creators (or perhaps more accurately, their profiteers), but as technologies become more widely adopted and standardized, they often restrict choice, exert control, and provide new surfaces for exploitation.
<!-- (Like how the automobile mand the disappearance of public railroad infrastructure, like the sewing machine and the rise of sweatshops) -->
<!-- (restrict possibility rather than expand it) -->
<!-- (defined as a collection of practices used in specific ways by specific groups of people) -->

Self-hosting is one strategy for resisting the narrowing of the internet, of digital commons, and of centralized cloud infrastructure, whether that's driven by for-profit companies, or nation-states that seek to control the flow of information. 

Self-hosting gives us more ownership of our own infrastructure, data, and services, where we can run the kinds of resources that we want and need for ourselves and our communities. It's a site for agency and reclamation.

Lastly, self-hosting is also a site of joy, imperfection, learning, and slowness, where we can play in the [dirt of the internet](https://techlearningcollective.com/2019/07/22/want-to-get-good-with-computers-dont-start-with-code.html).

<!-- A kind of conclusion sentence, linking to other resources, or ...? -->

#### What does Tor offer for self-hosting?
There are many ways to host your own websites. Tor is only one of them! I've found Tor specifically useful, because:
  * You don't need to configure your home router or worry about a firewall. Tor does something called NAT hole punching out-of-the-box, which means you can easily run a website from your own machine that can be accessed outside of your local network.
  * You don't need a domain name or to configure DNS. Tor creates a unique hostname for your website and populates that information over its network.
  * You don't need to worry about exposing your IP address to the wider internet. Tor's onion routing makes it possible for other people to request access to your website while keeping your computer's address anonymous.

<!-- What are the drawbacks to using Tor? / that I should consider? -->
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

You can download a sample website from [Github](https://github.com/lizzthabet/itp-onion-demo), if you don't already have a website that you'd like to host locally.

<!-- TODO: (possibly) Explain onion urls and links -->

### *(optional)* If you're using the sample website

<!-- TODO: Add a little section on customizing the html file and adding an image -->

### Track #1: Using OnionShare

#### What you'll need
  * A website that you'd like to host
  * [Tor Browser](https://www.torproject.org/download/) ([onion link](http://2gzyxa5ihm7nsggfxnu52rck2vv4rvmdlkiu3zzui5du4xyclen53wid.onion/download/index.html)) so you can access onion websites
  * [OnionShare](https://onionshare.org/) ([onion link](http://lldan5gahapx5k7iafb3s4ikijc4ni7gx5iywdflkba5y2ezyg6sjgyd.onion/#download)) installed

#### Start your onion site with OnionShare

1. Open OnionShare and go to the "Host a Website" option.

2. Click "Add files" or drag and drop the contents of the `public/` folder into OnionShare.

3. Make sure to check the option `This is a public OnionShare service`, and then click "Start sharing."

*Congratulations, you now have an onion site!*

Copy the `.onion` address so you can share it.

#### How to stop your onion site

When you're done with sharing your site files, click the "Stop sharing" button. That's it!

### Track #2: Using a local web server

#### What you'll need
  * A website you'd like to host
  * [Tor Browser](https://www.torproject.org/download/) ([onion link](http://2gzyxa5ihm7nsggfxnu52rck2vv4rvmdlkiu3zzui5du4xyclen53wid.onion/download/index.html)) so you can access onion websites
  * A way to run a web server locally, like nginx, apache, or python
  * The `tor` binary (also called *little-t tor*) so you can run an onion service locally. Follow the [installation instructions](https://community.torproject.org/onion-services/setup/install/) ([onion link](http://xmrhfasfg5suueegrnc4gsgyi2tyclcy5oz7f5drnrodmdtob6t2ioyd.onion/onion-services/setup/install/index.html)) for each OS.
    * For macOS, `tor` is most easily installed with Homebrew.
    * For Linux, instructions will vary based on your package manager.
    * For Windows, you'll need to download the [Tor Expert Bundle](https://www.torproject.org/download/tor/index.html) ([onion link](http://2gzyxa5ihm7nsggfxnu52rck2vv4rvmdlkiu3zzui5du4xyclen53wid.onion/download/tor/index.html)). There are detailed [instructions for Windows](https://miloserdov.org/?p=1839&PageSpeed=noscript) in the section titled "How to launch Tor on Windows" from Alexey Miloserdov.

#### Directory setup

<!-- TODO: Add instructions for setting up your site directory (if you're not cloning the sample repo or downloading the sample files), which will include a `public` folder and a `torrc` and optionally an `nginx.conf` if you're serving your site with nginx. -->

::::note[Tip]

Search for the `TODO` comments in this directory to find all the changes you'll need to make to run the demo.

::::

#### Part 1. Run a local web server
The first step is running a local static web server that will serve all the files in the `/public` directory. Below are examples using `python` and `nginx` using the sample configuration file in this repo.

You can also use another web server of your choosing, as long as it's serving content from `/public` and listening on port 3000.

Both code examples assume that you're running the command from the repository's root directory.

<!-- TODO: Add an explanation for why you'd choose one over the other -->

::::note[Note]

Command line instructions are macOS-centric, and I'm working on expanding them.

::::

##### With python

```sh
python3 -m http.server --directory ./public 3000
```

##### With nginx

Edit the `nginx.conf` file according to the `TODO` comment in that file. Then, start the nginx server.

```sh
nginx -c "$(pwd)/nginx.conf"
```

*Note*: The path to the `nginx.conf` should be absolute, not relative to the directory that you're running the command from.

After starting your web server, verify that you can access the site by visiting `localhost:3000` in your browser. (Tor Browser won't connect to `localhost`, so use your default browser instead.) 

*It's important to verify that your local server is up and your website is accessible at this point, otherwise the following steps won't work.*

#### Part 2. Start your `hidden_service` site

Next, we'll config and start a "location-hidden service" that will connect to your local web server and make it accessible over the Tor network.

A Tor service is configured through a `torrc` file, which is included in this repo. The default `torrc` file contains a lot of information about various settings with helpful comments about them. You're welcome to read through the config to learn more about how to set up various parts of the Tor ecosystem, but here we'll focus on the two settings you'll need to run your onion site, (one of which you'll need to update).

##### Instructions
1. In the `torrc` file, go to line 77 with the `TODO` comment.
2. Replace the directory listed next to `HiddenServiceDir` with the directory of this repository. Then add `/hidden_service/` to the end of that path. *Note*: Do not create the `/hidden_service/` directory yourself. Tor will create the directory with the correct permissions when it runs for the first time.
3. In your terminal from this directory, run:
    ```sh
    tor -f torrc
    ```
4. Tor is now running! In this directory, you should see a new `hidden_service` folder that's been created. You can open up the `hidden_service/hostname` file to view your onion site address, or you can run:
   ```sh
   pbcopy < ./hidden_service/hostname
   ```
   to copy the onion address to your clipboard.
5. Open Tor Browser and navigate to your onion site's address. You should see the same website as what's being served on your `localhost:3000`.

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
<!-- TODO: Add some content here :) -->

### I'd love your feedback
<!-- TODO: Add content here :) -->