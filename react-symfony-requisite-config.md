
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

### Using nvm
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
## Setup Babel
- Install React preset
```bash
$ npm install --save-dev @babel/preset-react
```
and add @babel/preset-react to your Babel configuration.
- Install Flow and Type script annotation :
```bash
$ npm install --save-dev @babel/preset-flow
$ npm install --save-dev @babel/preset-typescript

```
##  Create React App project with TypeScript
```bash
$ npx create-react-app my-app --template typescript

# or

$ yarn create react-app my-app --template typescript
```


## To add TypeScript to an existing Create React App project, first install it
```bash

npm install --save typescript @types/node @types/react @types/react-dom @types/jest

# or

yarn add typescript @types/node @types/react @types/react-dom @types/jest

```
