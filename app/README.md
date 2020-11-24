# Sparta Node Sample App

## Description

This app is intended for use with the Sparta Global Devops Stream as a sample app. You can clone the repo and use it as is but no changes will be accepted on this branch. 

To use the repo within your course you should fork it.

The app is a node app with three pages.

## Solution
1) In order to get the app homepage to load, we must pass the tests that require Ubuntu packages to be installed.
2) `rake spec` is used to perform the tests.
3) Once tests are complete the packages which need to be installed are identified
4) In order to pass the tests the following packages must be installed when `vagrant up` is entered.
This is done by adding the following to the provision.sh file.
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install nginx -y
sudo apt-get install nodejs -y
sudo apt-get install npm -y
sudo npm install -g pm2
```
5) `vagrant up` is used to create a virtual machine instance with the packages inside the provision.sh file.
6) The tests are rerun and they should all pass.
7) Enter the virtual machine with vagrant ssh
8) Once inside the virtual machine run the following commands
```
npm install
npm start
```
9) Once ran go to your browser and type the address within your `config.vm.network` inside your Vagrantfile with :3000 at the end.
10) You should now have the page visible.

### Homepage

``localhost:3000``

Displays a simple homepage displaying a Sparta logo and message. This page should return a 200 response.

### Blog

``localhost:3000/posts``

This page displays a logo and 100 randomly generated blog posts. The posts are generated during the seeding step.

This page and the seeding is only accessible when a database is available and the DB_HOST environment variable has been set with it's location.

### A fibonacci number generator

``localhost:3000/fibonacci/{index}``

This page has be implemented poorly on purpose to produce a slow running function. This can be used for performance testing and crash recovery testing.

The higher the fibonacci number requested the longer the request will take. A very large number can crash or block the process.


### Hackable code

``localhost:3000/hack/{code}``

There is a commented route that opens a serious security vulnerability. This should only be enabled when looking at user security and then disabled immediately afterwards

## Usage

Clone the app

```
npm install
npm start
```

You can then access the app on port 3000 at one of the urls given above.

## Tests

There is a basic test framework available that uses the Mocha/Chai framework

```
npm test
```

The test for posts will fail ( as expected ) if the database has not been correctly setup.




