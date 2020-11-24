## Provisioning with vagrant
```ruby
# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "private_network", ip: "192.168.10.100"
  # config.hostsupdater.aliases = ["development.local"]

  # Sync the app folder(not copying in. Its syncing)
  #
  config.vm.synced_folder "app", "/app"
  ```
## Core Sections of Provisioning
There are some actions that are core to provisioning.
These concepts are tool and language agnostic.
- making files available / Syncing files (Cover today)
- being able to run commands / scripts (Cover today)
- injecting environment variables
- sending in files

## Syncing in files with VM
Allowing us to send files and sync them into the VM.
This is so we can make code and other necessary files available.


## Running a bash script
This bashscript can install packages, alter files, run code, do actions in our linux servers when we run vagrant up.

This will allow us to set up the machine to a state that is desirable for us and automate processes.
Create a bash file to tell vagrant what to do on vagrant up

1) create a `provision.sh` file
2) include it in vagrant file

```ruby
 # run the provision script
  config.vm.provision "shell", path: "environment/provision.sh"
  ```

## Managing runningservices in linux
- `sudo systemctl <action> <service>`
- `sudo systemctl restart nginx`

## Given new project to create an Environment
When given a new project, you want to ask a few questions to help you get going.
e.g.
1) What language is it in?
2) Is there a framework to install? (rails, flask, django, wordpress)
3) Any specific packages? if so is there a list? (Gemfile, requirements.txt)
4) Any tests?

### What language is it in?
Code is in JS and others.
There are some tests in ruby and rspec

### Is there a framework to install?
No. only the testing framework, rspec


### Any specific packages?
Yes, with the environment file, you have a Gemfile with dependencies

### Any tests?
Yes, 
1) you have integration tests to run outside the machine (rake spec)
2) Potential unit tests in JS inside.



## Gem and bundler VS PIP and packages
Gems are packages in ruby or dependancies
bundler is ruby's package manager
Gemfile keeps a list of dependencies to be installed
To install gems from the Gemfile, you run:
`bundle install`

-> let's go install bundler

## Ruby's testing framework is rspec
rspec needs to be installed 

## JS package manager is npm (node package manager)
npm packages
after a certain version, comes pre loaded with NPM
## Ubuntu package manager
apt-get

## Installing test

1) go to folder with Gemfile
2) run 'bundle'

## Running test
1) rake spec

## End of Day
- run tests
- understand what they test
- solve failed tests

- how to provision your machine with :
1) code
2) instructions