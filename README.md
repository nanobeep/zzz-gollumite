# Gollumite

Gollumite is a setup for easily editing content in order to produce pretty html and pdf versions.

### Gollumite is backed directly by:

- [gollum](https://github.com/nanobeep/gollum) - GitHub's wiki editor engine
- [PrinceXML](http://www.princexml.com/) - best-in-class PDF generator

### Other supporting software:

- [Ansible](http://docs.ansible.com/) - for server setup and orchestration
- [Vagrant](http://www.vagrantup.com/) - VM setup for local development
- [Ubuntu 12.04 "Precise Pangolin"](http://en.wikipedia.org/wiki/List_of_Ubuntu_releases#Ubuntu_12.04_LTS_.28Precise_Pangolin.29) - chosen for its Long Term Support (till April 2017)

## Installation

- Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (the Vagrant VM 'provider' we're using)
- Install [Vagrant](http://www.vagrantup.com/downloads)
- Install [Ansible](http://docs.ansible.com/intro_installation.html)
- `cd` into whatever base directory you want to use on your host machine
- `git clone git@github.com:nanobeep/gollumite.git`
- `cd gollumite`
- `vagrant up` - wait a few seconds after this finishes to allow the VM networking to come up
- `ansible-playbook vagrant-playbook.yml -i hosts`
- `vagrant ssh` - this will log you into the new VM and has ssh key forwarding (required if you use gollum commit hooks)
- `git config --global user.email "me@here.com"`
- `cd projects`
- `git clone git@github.com:your-username/your-project.git`
- `cd your-project`


## Using gollumite

When on the VM and in the relevant project folder (the 'your-project' directory):

- `make start-gollum` to start the gollum web server for editing/viewing the wiki at <http://0.0.0.0:4567/>. Feel free to also edit the files in your regular text editor. Just remember that gollum generates the wiki from git, so the changes will not show in gollum (and generated html/pdf) until they are actually committed to git. If you save a file from within the web interface, the change is committed to git and there are git post-commit hooks that 1) sync the changes with the github repo, and 2) regenerate html/pdf output.
- `make html` generates the html with and without the layout. The gollum web server must be running for this command to work.
- `make pdf` generates the pdf from the html which the previous command created. On OSX, if you open the pdf in the "Preview" app from within the `projects` directory, then Preview will automatically reload the pdf every time you regenerate it.
- `make` just runs the html generation and then the pdf generation commands.

- Note that you will also have the `projects` directory in the `gollumite` directory on your host machine, so that you can edit the files in a local editor if you'd like and they will automatically be synced to your VM when saved.

## Formatting

Gollum uses [Github-flavored markdown](https://help.github.com/articles/github-flavored-markdown) and also has some of its own [special formatting](https://github.com/nanobeep/gollum/wiki). 

Note: We use the `![Guide Cover](images/guide-cover.png)` syntax instead of the `[[images/guide-cover.png|alt=Guide Cover]]` syntax so that the images will show on Github (they are still using an old version of Gollum that doesn't support the new syntax).

Note: Internal anchors are auto-generated from headings and case-sensitive, so double-check that you don't break anchors if you change a heading's text.

