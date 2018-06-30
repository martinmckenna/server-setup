### Getting Setup on Centos 7

This guide is a checklist of all the things that need to be done to configure a server
on CENTOS 7.

#### Create a Sudo User

[Linode - create sudo user](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-centos-quickstart)

#### Auth with SSH

[Digital Ocean - how to set up SSH Keys](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-centos7)
* create SSH keys on client machine (or use the ones that I already have)
* copy public key to `./~ssh/authorized_keys` file

^^ That article does not go over how to add SSH keys to Git, so
* run `ssh-keygen` on the server and copy the pub key over to GitHub

#### Misc Getting Stated Tasks

[Linode - Getting started](https://www.linode.com/docs/getting-started/)

* run updates (`yum update` - pretty simple)
* set hostname
* update hosts file
* set timezone

#### Secure the Server

[Linode - How to Secure Your Server](https://www.linode.com/docs/security/securing-your-server/)

* disallow root login
* configure a firewall with FirewallD ([Steps located here](https://www.linode.com/docs/security/firewalls/introduction-to-firewalld-on-centos/))

#### Install a LAMP Server

[Linode - Setting up LAMP on Centos 7](https://www.linode.com/docs/web-servers/lamp/lamp-on-centos-7/)

[Install and Configure phpMyAdmin](https://www.liquidweb.com/kb/how-to-install-and-configure-phpmyadmin-on-centos-7/)

#### Redirect www to non-www (Optional)

[Digital Ocean Guide](https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-apache-on-centos-7)

#### Set up SSL

[Digital Ocean - Secure Apache w/ Let's Encrpyt](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-7)

[Certbot](https://certbot.eff.org/lets-encrypt/centos6-apache)

Also set up with autorenewal by putting [this file](scripts/crontab) into `etc/crontab` on the server
Also add the line [here](scripts/visudo) by running `visudo` and appending to the end of the file

#### Setup up a Mail Server with a Gmail Relay

[Guide here](https://devops.profitbricks.com/tutorials/configure-a-postfix-relay-through-gmail-on-centos-7/)

### Misc Requirements
* Install Git, Yarn, and Node


### Possble Issues

These are things that I ran into that had to be solved in the past

[Postfix `main.cf` permission denied](https://serverfault.com/questions/503642/postfix-main-cf-permission-denied)

[Write permissions inside of `public_html`](https://blog.lysender.com/2015/07/centos-7-selinux-php-apache-cannot-writeaccess-file-no-matter-what/)

Also when in doubt, try running `sudo`

Happy configuring!