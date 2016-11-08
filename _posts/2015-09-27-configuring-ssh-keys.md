---
layout: post
title: Configuring ssh keys
excerpt: 
author: daxaar
categories:
  - Bash Terminal
  - OSX

tags:

draft: false
---
In this post I'll explain how to setup ssh keys on a Mac so you no longer have to enter a password when connecting to a remote machine (generally *nix based) using ssh.

If you don't have homebrew installed consider <a href="http://brew.sh/">doing so now</a>. To quote the authors: "It's the missing package manager for OSX". Whilst not entirely necessary it will allow us to easily install the prerequisites.

<ol>
    <li>Install <code>ssh-copy-id</code> which allows us to upload the public key to the remote more easily.</li>
</ol>

<code>brew install ssh-copy-id</code>

<ol>
    <li>Create the public and private key pair file locally providing an optional password. This will get stored under ~/.ssh. Specifying a filename is optional.</li>
<ol>
<code>ssh-keygen</code>
</ol>
    <li>Now we need to put the public key on the remote server. The tool we installed in step 1 will allow us to easily do this.</li>
</ol>

<code>ssh-copy-id user@serverip-or-name</code>

<ol>
    <li>That's it! <code>ssh</code> onto the machine using the user you specified in step 3 and if all went well you'll connect without having to provide a password.</li>
</ol>
