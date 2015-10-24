# Magento Vagrant box with Ansible

**/!\ PLEASE DO NOT USE IN PRODUCTION**  
**This box is made for development environment only.**

**Magento files are not provided into it**. You have to put your files into the `magento` directory (see the "Coding" part).

## Requirements

* Ansible: `brew install ansible` if you have Homebrew
* Vagrant
* Virtual Box or VMWare
* Hostmanager plugin: `vagrant plugin install vagrant-hostmanager`

## Run it

Just run `vagrant up` and tada!

You can change the URL in the `Vagrantfile` which is `mage.dev` by default.

When it's running, just go to <http://mage.dev>.

Of course you can access to the Setup Wizard: <http://mage.dev/setup>.

## Coding

The `magento` folder (which will be created during the provisioning) is the root directory of the virtual host.

So, you can put your Magento into it, or any other PHP project.

Into the Vagrant box, the `/vagrant` directory contains all your files.

Here are the tools (binary names) we provide out of the box:

* **magerun** for Magento 1
* **magerun2** for Magento 2
* **modman**
* **composer**
* vim
* tmux/screen
* tig
* gnupg
* and others. Take a look at `roles/common/tasks/main.yml`.

## Database

We use MariaDB, not MySQL

* Users:
    * `root`: `mysql`
    * `vagrant`: `vagrant-password`

## SSH

* Users:
    * `vagrant`: `vagrant`

## Authors

* Jacques Bodin-Hullin @jacquesbh

