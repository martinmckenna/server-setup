# Getting Setup on Centos 7

This guide is a checklist of all the things that need to be done to configure a server
on CENTOS 7.

### Create a Sudo User

[Linode - create sudo user](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-centos-quickstart)

### Auth with SSH

[Digital Ocean - how to set up SSH Keys](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-centos7)
* create SSH keys by running `ssh-keygen` on client machine (or use the ones that I already have)
* copy public key (`cat ~/.ssh/id_rsa.pub`) to `./~ssh/authorized_keys` file on the server

^^ That article does not go over how to add SSH keys to Git, so...
* run `ssh-keygen` on the server and copy the pub key (`cat ~/.ssh/id_rsa.pub`) over to GitHub

### Misc Getting Stated Tasks

[Linode - Getting started](https://www.linode.com/docs/getting-started/)

* run updates (`yum update` - pretty simple)
* set hostname
* update hosts file
* set timezone

### Secure the Server

[Linode - How to Secure Your Server](https://www.linode.com/docs/security/securing-your-server/)

* disallow root login
* configure a firewall with FirewallD ([Steps located here](https://www.linode.com/docs/security/firewalls/introduction-to-firewalld-on-centos/))

### Install a LAMP Server

[Linode - Setting up LAMP on Centos 7](https://www.linode.com/docs/web-servers/lamp/lamp-on-centos-7/)

[Install and Configure phpMyAdmin](https://www.liquidweb.com/kb/how-to-install-and-configure-phpmyadmin-on-centos-7/)

### Redirect www to non-www (Optional)

[Digital Ocean Guide](https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-apache-on-centos-7)

### Set up SSL

[Digital Ocean - Secure Apache w/ Let's Encrpyt](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-7)

[Certbot](https://certbot.eff.org/lets-encrypt/centos6-apache)

Also set up with autorenewal by putting [this script](scripts/crontab) into `etc/crontab` file on the server.

Please note that the above will not work without first running `sudo visudo` and appending the [script here](scripts/visudo) to the end of the file,
so that the sudo user can run the command without needing a password

### Setup up a Mail Server with a Gmail Relay

[Guide here](https://devops.profitbricks.com/tutorials/configure-a-postfix-relay-through-gmail-on-centos-7/) - 
this will allow for email to be sent from your personal Gmail account

### Misc Tasks
* [Install Node.js](https://nodejs.org/en/download/package-manager/#enterprise-linux-and-fedora)
* Install Git - `sudo yum install git`
* [Install Yarn](https://yarnpkg.com/lang/en/docs/install/#centos-stable)


## Possble Issues

These are things that I ran into that had to be solved in the past

[Postfix `main.cf` permission denied](https://serverfault.com/questions/503642/postfix-main-cf-permission-denied)

[Write permissions inside of `public_html`](https://blog.lysender.com/2015/07/centos-7-selinux-php-apache-cannot-writeaccess-file-no-matter-what/)

[`domain.com` not working in URL bar](https://www.linode.com/community/questions/16962/apache-virtual-hosts-non-www-not-working)

Also when in doubt, try running `sudo`

Happy configuring!