# Configuring WSL (with Django)

These steps will help you configure WSL so that you can start developing on an virtual environment
with Python (and Django)

## Initial Steps

[Install Ubuntu from the Windows app store and turn on the WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

Once installed and a user has been created run

```bash
apt-get update
apt-get -y upgrade
```

This will give you most packages that you need, namely Python 2 and 3

Run `python -V` to see what version of Python you have. If the default is 2.XX, make
the default python3 by running

```
alias python=python3
```

Then, run `python -V` again to confirm python3 is the default

We're also going to want pip. Run

```
apt-get install -y python3-pip
```

## Opening Files in a Text Editor

Obviously, we're going to want to edit files in a text editor. To do so, we need to create symlink
between our Windows files and the Linux ones. First, create a directory in the Windows file system
that you'd like all your WSL code to go. I created a directory here

`C:\Users\mmcke\linux`

Now that we have our directory in Windows, run this command to create the link between the
Linux filesystem and the Windows one

```
ln -s /mnt/c/Users/%username%/linux ~/linux
```

__It's important that you don't create any directory in Linux until this point. This command will
automatically create the `~/linux` directory for you when you create the symlink__

Since were getting everything confirgured to work with Python, lets install PyCharm IDE
and allow ourselves to open directories in PyCharm from the command line

First, download PyCharm from the official site

Then we need to add Pycharm to PATH in Windows, so navigate to

`Advanced Settings > Environment Variables > Path > Edit > New`

and then enter the path to the `PyCharm.exe` file. For me, it was the following

`C:\Program Files\JetBrains\PyCharm Community Edition 2018.1.4\bin`

Finally, click okay and now close all terminals and reopen

Now, we should be able to run the following from the command line

`pycharm64.exe myproject`

## Getting VirtualEnv Configured

Now, we want to install some packages to help us develop in a virtual environment.

First, install `virtualenv` like so:

```bash
pip3 install virtualenv
```

Test the installation by running

```bash
virtualenv --version
```

Now, we want to install virtualenvwrapper, which provides easier commands when working with
virtual environments

__virtualenv is totally a requirement for virtualenvwrapper, so make sure you install that first__

To install run:

```bash
pip3 install virtualenvwrapper
```

Then open the `.profile` file by running:

```bash
sudo nano ~/.profile
```

and add the following to the end of the file:

```bash
export WORKON_HOME=~/Envs
source /usr/local/bin/virtualenvwrapper.sh
```

Finally run the following to load your profile you've just created:

```bash
. .profile
```

The purpose of doing this is so you can easily reopen the virtualenvs even when closing out
the Linux terminal and coming back later

Now we're ready to create our virtualenv. It's important that we create the env with Python3, so
run the following

```bash
mkvirtualenv -p python3 myproject
```

Finally to run the virtualenv, run:

```bash
workon myproject
```

and to stop it, run:

```bash
deactivate
```

## Setting up Django

For these instructions, make sure you're in the `linux` directory

From here, the steps to getting Django set up should be relatively the same as the ones on the
official site. While in the virutalenv, run the following to install Django:

__Do not run as `sudo` here or you will run into problems__

```bash
pip3 install Django
```

Then confirm that it worked by running the following

```bash
python

>>> import django
>>> print(django.get_verison())
```

if you get an error saying that django is not a module, try

```bash
pip3 uninstall Django
pip install Django
```

and then confirm the version again

And that should be it. Django it successfully installed and now you can go
[create your first app](https://docs.djangoproject.com/en/2.0/intro/tutorial01/)
