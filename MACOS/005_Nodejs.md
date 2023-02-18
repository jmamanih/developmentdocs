
# INSTALL NODEJS
# BACKEND

## Install nvm
Node version manager

If message: nvm is not compatible with the npm config "prefix" then:

Uninstall node

```
brew uninstall --force node
rm -rf ~/.npm
rm -rf ~/.node
```

Uninstall nvm

```
brew remove nvm
brew cleanup
```

Install nvm stable

```sh
curl -o-  https://raw.githubusercontent.com/creationix/nvm/v0.31.7/install.sh | bash

```
Appending source string to /Users/user_name/.zshrc

```sh
export NVM_DIR="/Users/juanfer/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
```
close terminal

```sh
nvm --version
0.31.7
```

## Install node

Open [Site Web Node](https://nodejs.org/es/)
view last version LTS

```
nvm install 5.6.0
nvm list
nvm use 5.6.0
nvm current

node --version

```

## Install sequelize
Framework ORM oriented to SQL

```
npm install -g sequelize sequelize-cli
```
## Install pg-hstore
Module for serializing and deserializing JSON data

```
npm install -g pg pg-hstore
```
## Install postgres

```
brew install postgresql-9.4 postgresql-client-9.4
```

### Create Database

```
sudo passwd postgres
su postgres
psql
```

```
CREATE USER asamblea_user WITH PASSWORD 'Developer';
CREATE DATABASE asambleadb;
GRANT ALL PRIVILEGES ON DATABASE asambleadb TO asamblea_user;
\q
exit
```
### Change password postgres user

```
su
su postgres
psql
    =# ALTER ROLE postgres PASSWORD 'postgres';
```
Restart service postgresql

```
sudo su postgres
/Library/PostgreSQL/9.4/bin/pg_ctl restart -D /Library/PostgreSQL/9.4/data/
```

Run project node.js

```
cd /proyecto
npm install
npm start
npm run setup
npm start
```
## Install Apache CouchDB

[Download Apache CouchDB for Mac OS X](http://couchdb.apache.org/#download)

    Double click on the Zip file
    Drag and drop the Apache CouchDB.app into Applications folder

That’s all, now CouchDB is installed on your Mac:

    Run Apache CouchDB application
    Open up Fauxton, the CouchDB admin interface
    Verify the install by clicking on Verify, then Verify Installation.

### Create Database Apache CouchDB

```
curl -X PUT http://127.0.0.1:5984/starwars
```
Result

```sh
{
   "ok":true
}
```
### Verify running couchdb

```
curl http://127.0.0.1:5984/
```
Result

```sh

{"couchdb":"Welcome","version":"2.0.0","vendor":{"name":"The Apache Software Foundation"}}

```

# FRONTEND
## Install bower, yo, gulp, angular

```
npm install -g bower

bower --version

npm install -g grunt-cli
npm install -g grunt
npm install -g yo
npm install –g gulp
npm install -g generator-gulp-angular
npm install -g generator-gulp-angular-sub
```
Displaying Global Packages

```
npm list -g
npm list -g --depth=0

```

Runnig project

```
cd project
bower install
npm install
gulp serve

```

Install gulp angular sub

```
npm install -g generator-gulp-angular-sub

```

Generate view files with angular

```
yo gulp-angular-sub:view
```
```sh
? the view name filename_module
? the view url filename_module
? the parent folder in which the the view folder will be created
modules/subfolder_modules

```

# Bug fix running npm install

Error ssl.....

Solution:

```
npm config set strict-ssl false
npm config set registry="http://registry.npmjs.org/"

```
