# ANGULAR JS

Angular JS https://angularjs.org

## Install Tools Scalffolding for Angular
### [Yeoman](http://yeoman.io/)
* The scalffoldings tool (Yo)
* The build tool (Gulp, Grunt)
* The package manager (bower, npm)

### Setting npm proxy config
View config proxy of npm

```sh
npm config list
npm config get proxy
npm config get https-proxy
```

Config Proxy for npm
```sh
npm config set proxy=http://127.0.0.1:3122
npm config set https-proxy=https://127.0.0.0.1:3122
```

```sh
npm config edit
```

Update npm bower
```sh
npm i -g bower to update
```


### Install Yo

Install Yo
```sh
npm install -g yo
npm install -g generator-webapp
npm install -g generator-angular
npm install -g generator-karma
```

Other commands
```sh
yo --help
yo --version
yo --generators
```

```sh
yo doctor
```

## Generate Angular Project

```sh
yo angular_project
```


