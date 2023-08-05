# MacOS Setup with Ansible

This repository contains an Ansible configuration for setting up a Mac from scratch. It's primary purpose is setting up a new Mac from scratch, but I endeavor to also use it for adding new software as I go so that it remains up to date. At the moment it's being used for setting up M1 based Macs running MacOS Monterey.

## Getting Started

Some preliminary steps and information: 

1. **UPDATE THE MAC FIRST BEFORE RUNNING** I ran into a bunch of issues with this by trying to do that after a few attempts at running this. 
2. If you somehow stumbled upon this fork of this repo, make sure you have downloaded Xcode at least once before from the app store or you might get an error telling you that you don't have permissions for that during the `mas install` part.
3. If you get an error during `TASK [geerlingguy.mac.homebrew : Ensure Homebrew is installed.]` it might be because you have not signed the xcode license. Do the following:
  
    ```sh
    sudo xcodebuild -license
    ```

    This is described in [this post](https://github.com/geerlingguy/ansible-role-homebrew/issues/45). If still having trouble then try upgrading ansible.

4. If you manually make changes to ~/.zshrc and then later run `bin/apply` you will overwrite those changes with the template in this project. Make sure you update the template with any changes you make locally.
5. You will need to manually adjust 2 things in iterm settings (`cmd+,`):
    1. You need to navigate to `Profiles > Text` and enable "Use built-in powerline glyphs" in order to use special characters in starship like the git branch symbol.
    2. The Dracula theme will be downloaded to the themes folder but you will need to import and activate this in `Profiles > Colors > Color Presets`.
6. You can install additional environments via `asdf` and rerun the ansible playbook. The environment will not be lost on rerun.

There's a simple shell script in `bin/bootstrap` which will perform the initial steps of:

1. Installing Xcode
2. Installing Ansible
3. Fetching required Ansible roles and collections

And then runs the main playbook `ansible_osx.yml`.

For future updates, `bin/apply` can be used to run just the Ansible playbook without the setup commands.

It's important to note that this isn't designed to be particularly robust, particularly when it comes to required env vars, it may be required to run this. Then close the terminal and open it again and re-run and then repeat this process a few times.

## What's installed

The easiest way to understand what's installed is to read the contents of `ansible_osx.yml`, this configuration is fairly specific to the range of development I do personally, but may serve as a useful starting point for others. The core components are:

- ZSH + Oh My Zsh as the primary shell
- Homebrew for package management
- ASDF for version management (along with plugins and default versions for ruby, python, javascript, elixir and erlang)
- Virtualbox, Vagrant and Docker
- VSCode + default plugins and configuration
- A selection of Android SDK's
- Lots of other tools and utilities

## Customising

Everything can be customised by editing `ansible_osx.yml`.

