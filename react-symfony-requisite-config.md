
# React Symfony Prerequisite configuration

## Install nvm
```bash
$ sudo apt install curl
$ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash  
$ source ~/.profile 
```

## Install nodejs via nvm
- Install latest version of node
```bash
$ nvm install node 
```
- Install specific version of node
```bash
$ nvm install 16.6.1
```

## Install yarn
```bash
$ npm install --global yarn
```

## Using nvm
```bash
# You can use the following command to list installed version’s of Node for the current user.
$ nvm ls 
# With this command you can find available Node.js version for the installation.
$ nvm ls-remote 
# You can also select a different version for the current session. This will be current active version for current shell only.
$ nvm use 16.6.1 
# To find the default Node version set for the current user, type:
$ nvm run default --version 
```
