# Getting Setup on Debian 9

This guide is a checklist of all the things that need to be done to configure a server
on Debian 9.

### Create a Sudo User

[Linuxize - create sudo user](https://linuxize.com/post/how-to-create-a-sudo-user-on-debian/)

### Auth with SSH

[Digital Ocean - how to set up SSH Keys](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-debian-9)
* create SSH keys by running `ssh-keygen` on client machine (or use the ones that I already have)
* copy public key (`cat ~/.ssh/id_rsa.pub`) to `./~ssh/authorized_keys` file on the server

^^ That article does not go over how to add SSH keys to Git, so...
* run `ssh-keygen` on the server and copy the pub key (`cat ~/.ssh/id_rsa.pub`) over to GitHub

### Misc Getting Stated Tasks

[Linode - Getting started](https://www.linode.com/docs/getting-started/)

* run updates (`sudo apt-get update && sudo apt-get upgrade` - pretty simple)
* set hostname
* update hosts file
* set timezone

### Secure the Server

[Linode - How to Secure Your Server](https://www.linode.com/docs/security/securing-your-server/)

* disallow root login

[Digital Ocean - Add a firewall](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-debian-9)
* configure a firewall with UFW ([Steps located here](https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/))
  * be sure to remember to both activate the firewall and allow port 22 SSH

### Install Nginx Server

[Digital Ocean - Setting up Nginx with server blocks](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-debian-9)

### Getting React-Router working with Nginx

[See here for config fix](https://stackoverflow.com/questions/47025983/getting-404-with-react-router-app-with-nginx)

### Install SSL and redirect to https

[Digital Ocean - Secure Nginx w/ Let's Encrpyt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-debian-9)

This will create a cron job in `/etc/cron.d/certbot`.

Replace the existing cron job with [this script](scripts/crontab)

### Setup up a Mail Server with a Gmail Relay

[Linode - Guide here](https://www.linode.com/docs/email/postfix/configure-postfix-to-send-mail-using-gmail-and-google-apps-on-debian-or-ubuntu/) - 
this will allow for email to be sent from your personal Gmail account

Please note: You'll also need to install `sudo apt-get install mailutils`

### Misc Tasks
* [Install Node.js](https://github.com/nodesource/distributions/blob/master/README.md)
* Install Git - `sudo apt-get install -y git`
* [Install Yarn](https://yarnpkg.com/lang/en/docs/install/#debian-stable)


## Possble Issues

These are things that I ran into that had to be solved in the past

[Postfix `main.cf` permission denied](https://serverfault.com/questions/503642/postfix-main-cf-permission-denied)

[Write permissions inside of `public_html`](https://blog.lysender.com/2015/07/centos-7-selinux-php-apache-cannot-writeaccess-file-no-matter-what/)

[`domain.com` not working in URL bar](https://www.linode.com/community/questions/16962/apache-virtual-hosts-non-www-not-working)

Also when in doubt, try running `sudo`

Happy configuring!