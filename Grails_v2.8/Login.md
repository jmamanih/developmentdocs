# Tutorial to create a web application login in Grails
## Version 2.3.8

## Create grails-app 

Windows

```
File, New Project, Grails, Project Name: testLogin 
Run "create app"
```

MacOSX
From the terminal write

```
grails create-app testLogin

```

## Configure Database Postgress

According to the version of Postgres copy the .jar library to the /lib folder

Download [Postgres JDBC Driver](https://jdbc.postgresql.org/download.html)

Copy file: postgresql-9.3-1101.jdbc4 to folder project /lib

Edit file: Configuration/DataSource.groovy

```js
dataSource {
	pooled = false
	jmxExport = true
	driverClassName = "org.postgresql.Driver"
	username = "postgres"
	password = "easbaPostgres"
	dialect  = "org.hibernate.dialect.PostgreSQLDialect"
}
hibernate {
	cache.use_second_level_cache = true
	cache.use_query_cache = true
	cache.provider_class  = 'net.sf.ehcache.hibernate.EhCacheProvider'
}
// environment specific settings
environments {
	development {
		dataSource {
			dbCreate = "update" // one of 'create', 'update', 'create-drop'
			url      = "jdbc:postgresql://localhost:5432/easba"
		}
	}
	test {
		dataSource {
			dbCreate = "update"
			url      = "jdbc:postgresql://localhost:5432/easba"
		}
	}
	production {
		dataSource {
			dbCreate = "update"
			url      = "jdbc:postgresql://localhost:5432/easba"
		}
	}
}	
```

Run Compile for verify config Database Postgres

Windows

```
IntelliJ Menu Run, Run 
```

MacOSX

```
cd folder_app
grail run-app
```


## Install and Configuration Spring Security Core

Edit grails-app/configuration/BuildConfig.groovy file

Example:

```js
	grails.project.dependency.resolution = {
		...
	
		plugins {
      			...  	
			compile ":spring-security-core:1.2.7.3"  // <-- Added
   		}
	}
```

### Compile Spring Security Plugin

RUN Compile Grails Aplication (ssDemo), verify in Plugins->spring-security-core:1.2.7.3 
Verify in console windows of IntelliJ:

```
...
|Installed plugin spring-security-core-1.2.7.3

*******************************************************
* You've installed the Spring Security Core plugin.   *
*                                                     *
* Next run the "s2-quickstart" script to initialize   *
* Spring Security and create your domain classes.     *
*                                                     *
*******************************************************
```

RUN Command Grails: (Ctrl+Alt+G) s2-quickstart org.testlogin.security Usuario Rol
Verify in console windows of intelliJ:

```
.....
|
*******************************************************
* Created domain classes, controllers, and GSPs. Your *
* grails-app/conf/Config.groovy has been updated with *
* the class names of the configured domain classes;   *
* please verify that the values are correct.          *
*******************************************************
```

Or in MacOSX

```
grails s2-quickstart org.test.security Usuario Rol
```


After Run, Created:

```
>Domain clases
 org.easba.security
 -> Rol
 -> Usuario
 -> UsuarioRol

>Controllers
 -> LoginController
 -> LogoutController

>Views
 login
 -> auth.gsp
 -> denied.gsp
```

In File Grails-app/configuration/Config.groovy

```
// Added by the Spring Security Core plugin:
grails.plugins.springsecurity.userLookup.userDomainClassName = 'org.testLogin.security.Usuario'
grails.plugins.springsecurity.userLookup.authorityJoinClassName = 'org.testLogin.security.UsuarioRol'
grails.plugins.springsecurity.authority.className = 'org.testLogin.security.Rol'
```

### Configuration Run Init Login 

Edit grails-app/configuration/UrlMappconfig.groovy file

```js
	static mappings = {
        	"/$controller/$action?/$id?(.$format)?"{
	            constraints {
                // apply constraints here
            }
        }
        "/"(controller: 'login', action: 'index')  //"/"(view:"/index")   <-- EDIT
        "500"(view:'/error')
	}
```

Edit LoginController

```js
		import grails.plugins.springsecurity.Secured
		
		@Secured(['ROLE_USER'])		//<-- Added
		def index = {
			if (springSecurityService.isLoggedIn()) {
				//redirect uri: SpringSecurityUtils.securityConfig.successHandler.defaultTargetUrl
				render (view: '/index')   // <-- Added
			}
			else {
				redirect action: 'auth', params: params
			}
		}
```

### Create Default User, Role 

Edit to file grails-app/configuration/BootStrap.groovy

```js
import grails.plugins.springsecurity.SpringSecurityService
import org.testLogin.security.*

class BootStrap {

	transient SpringSecurityService

	def init = { servletContext ->
		if(!Usuario.count()){
			def passw = 'admin'
			def user = new Usuario(username : 'admin', password:passw, enabled:true,
					accountExpired : false , accountLocked : false, passwordExpired : false).save(flush: true, insert: true)
			def role = new Rol(authority : 'ROLE_USER').save(flush: true, insert: true)
			/*create the first user role map*/
			UsuarioRol.create user, role, true
		}
	}
	def destroy = {
	}
}
```

### Test Login 

Create PruebaController
Create view to PruebaController index
Edit index.gsp of PruebaController

```html	
<%@ page contentType="text/html;charset=UTF-8" %>
<html>
<head>
	<meta name="layout" content="main"/>
	<title></title>
</head>
<body>
Acceso Autorizado!
<br>
<br>
Cerrar Sessión:  <a href="${createLink(controller: 'logout')}"> Logout</a>
</body>
</html>
```

Test write to URL:   http://localhost:8080/testLogin/prueba


## DECLARE RESOURCES FOR GRAILS PROJECTS

Grails 2.0 >
Create or Edit File /Configuration/ApplicationResources.groovy

```js
modules = {

    // default
    application {
        resource url: 'js/application.js'
    }

    // jquery compatibility for jquery > 9.0
    jquery_migrate {
        resource url:'/js/jquery-migrate/jquery-migrate-1.2.1.min.js'
    }

    // flexigrid plugin style javascript Version 1.1
    flexigrid {
        dependsOn 'jquery'  // <- Declared in Plugins
        resource url:'/js/flexigrid/js/flexigrid.js'
        resource url:'/js/flexigrid/js/flexigrid.pack.js'
        resource url:'/js/flexigrid/css/flexigrid.css'
        resource url:'/js/flexigrid/css/flexigrid.pack.css'
    }

    // jquery ui Version 1.11.3
    jquery_ui {
        dependsOn 'jquery, jquery_migrate'
        resource url: '/js/jquery-ui/jquery-ui.min.js'
        resource url: '/js/jquery-ui/jquery-ui.min.css'
		resource url: '/js/jquery-ui/jquery.ui.datepicker-es.js'
    }

    // jqGrid 4.4.3
    jqgrid {
        dependsOn 'jquery, jquery_migrate, jquery_ui'
        resource url: '/js/jqgrid/css/ui.jqgrid.css'
        resource url: '/js/jqgrid/js/jquery.jqGrid.min.js'
        resource url: '/js/jqgrid/js/i18n/grid.locale-es.js'
    }

}
```

## USING RESOURCES FOR GRAILS FILES GSP

Include in Head Layout gsp:
	
```html
<head>
	<g:javascript library="application"/>
	<g:javascript library="jquery" />    <%--  <-- ADD For JQUERY --%>
	<r:layoutResources />
</head>
```

TEST JQUERY (Date in Head)

```html
<head>
	<g:layoutHead/>
	<g:javascript library="application"/>
	<g:javascript library="jquery" />
	<r:layoutResources />
	<script type="text/javascript">
		$(document).ready(function() {
			// Fecha del Sistema
			var meses = new Array ("enero","febrero","marzo","abril","mayo","junio","julio","agosto","septiembre","octubre","noviembre","diciembre");
			var diasSemana = new Array("Domingo","Lunes","Martes","Miércoles","Jueves","Viernes","Sábado");
			var f = new Date();
			$("#lblFecha").text(diasSemana[f.getDay()] + ", " + f.getDate() + " de " + meses[f.getMonth()] + " de "+ f.getFullYear());
		});
	</script>
</head>
<body>
	<label id="lblFecha"></label>
</body>
```

Include in head main.gsp
    
```html
    <script src="//code.jquery.com/jquery-1.11.2.min.js"></script>
    <script src="//code.jquery.com/jquery-migrate-1.2.1.min.js"></script>
```

Or
	
```html
	<g:javascript src="jquery/jquery-1.11.2.min.js"/>
    <g:javascript src="jquery/jquery-migrate-1.2.1.min.js"/>
    <g:javascript src="flexigrid/js/flexigrid.js"/>
    <g:javascript src="flexigrid/js/flexigrid.pack.js"/>
	
	<link rel="stylesheet" href="${resource(dir: 'js/flexigrid/css', file: 'flexigrid.css')}"/>
```

Include in head file *.gsp

```html	
	<r:require modules="jquery, jqmigrate, flexigrid"/>
```

Include in head file main.gsp

```html
	<r:use modules="jquery"/>
```

## REFRESH DEPENDENCIES PLUGINS 

Refresh Dependencies Plugins

```
Ctrl+Alt+G:                                                                                      
 ```

without attempting the defaults you are attempting to override your jquery-ui.

```
Install jquery-ui by adding
    compile ":jquery-ui:1.10.3"
to your BuildConfig
```

grails: refresh-dependencies

Then add this to your main.gsp

```html
<r:require module="jquery-ui"/> 
```

* jquery-ui themes download to: http://jqueryui.com/download/#!themeParams=none

### DISABLE ERROR: resource.ResourceMeta
Message Error: 
ERROR resource.ResourceMeta  - While processing /bundle-app_head.css, ...

Solution:
Edit /Configuration/Config.groovy, in log4j add line 

```
off 'org.grails.plugin.resource.ResourceMeta'
```

Example:

```js
// log4j configuration
log4j = {
    // Example of changing the log pattern for the default console appender:
    //
    //appenders {
    //    console name:'stdout', layout:pattern(conversionPattern: '%c{2} %m%n')
    //}
    error  'org.codehaus.groovy.grails.web.servlet',        // controllers
           'org.codehaus.groovy.grails.web.pages',          // GSP
           'org.codehaus.groovy.grails.web.sitemesh',       // layouts
           'org.codehaus.groovy.grails.web.mapping.filter', // URL mapping
           'org.codehaus.groovy.grails.web.mapping',        // URL mapping
           'org.codehaus.groovy.grails.commons',            // core / classloading
           'org.codehaus.groovy.grails.plugins',            // plugins
           'org.codehaus.groovy.grails.orm.hibernate',      // hibernate integration
           'org.springframework',
           'org.hibernate',
           'net.sf.ehcache.hibernate'

    off 'org.grails.plugin.resource.ResourceMeta'   //<--  Add
}
```

### REFRESH RESOURCES 

Edit File: /Configuration/Config.groovy and add grails.resources.debug = true

Example:

```js
environments {
    development {
        grails.logging.jul.usebridge = true
        grails.resources.debug = true   // <-- Add to refresh resources statics
    }
    production {
        grails.logging.jul.usebridge = false
        // TODO: grails.serverURL = "http://www.changeme.com"
    }
}
```


# SQL SERVER

Configuring Grails application to use SQL Server database
Posted on October 14, 2014 by Devesh Sharma in Grails, SQL Server

1. Create a new Grails application by typing in the following command in terminal window:

grails create-app grailsDbConn

2. Change to the application directory by typing the following command in terminal window:

cd grailsDbConn

3. Create a new Domain Class by typing in the following command in terminal window:

grails create-domain-class db.Employee

4. Open Employee.groovy file in your favorite IDE and edit it to the following:
	
package db
 
class Employee {
     
    String employeeID
    String firstName
    String lastName
    String dateOfBirth
 
    static constraints = {
    }
}

5. Create a new Controller by typing in the following command in terminal window:

grails create-controller db.Employee

6. Open EmployeeController.groovy in your favorite IDE and edit it to the following:
	
package db
 
class EmployeeController {
 
    def scaffold = Employee
}

7. Open DataSource.groovy file located at grails-app/conf in your favorite IDE to include the data source information
	
dataSource {
    dbCreate = "create-drop"
    driverClassName = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
    url="jdbc:sqlserver://localhost:1433;DatabaseName=[YOUR_DB_NAME]"
    username = "sa"
    password = "[YOUR_PASSWORD]"
}

The updated DataSource.groovy file will look like the following:
	
dataSource {
    pooled = true
    driverClassName = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
    url="jdbc:sqlserver://localhost:1433;DatabaseName=[YOUR_DATABASE]"
    username = "sa"
    password = "[YOUR_PASSWORD]"
    dbCreate = "create-drop"
    loggingSql = true
}
hibernate {
    cache.use_second_level_cache = true
    cache.use_query_cache = false
    cache.region.factory_class = 'net.sf.ehcache.hibernate.EhCacheRegionFactory' // Hibernate 3
//    cache.region.factory_class = 'org.hibernate.cache.ehcache.EhCacheRegionFactory' // Hibernate 4
}
  
// environment specific settings
environments {
    development {
        dataSource {
            dbCreate = "create-drop"
            driverClassName = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
            url="jdbc:sqlserver://localhost:1433;DatabaseName=[YOUR_DATABASE]"
            username = "sa"
            password = "[YOUR_PASSWORD]"
        }
    }
    test {
        dataSource {
            dbCreate = "update"
            url = "jdbc:h2:mem:testDb;MVCC=TRUE;LOCK_TIMEOUT=10000"
        }
    }
    production {
        dataSource {
            dbCreate = "update"
            url = "jdbc:h2:prodDb;MVCC=TRUE;LOCK_TIMEOUT=10000"
            properties {
               maxActive = -1
               minEvictableIdleTimeMillis=1800000
               timeBetweenEvictionRunsMillis=1800000
               numTestsPerEvictionRun=3
               testOnBorrow=true
               testWhileIdle=true
               testOnReturn=false
               validationQuery=&amp;quot;SELECT 1 from dual&amp;quot;
               jdbcInterceptors=&amp;quot;ConnectionState&amp;quot;
            }
        }
    }
}

8. Download sqljdbc4.jar and place that in your application’s /lib directory.

9. Start Grails by typing in grails run-app in terminal window.

Please note that a Grails application will be run with the built in Tomcat server on port 8080 by default. If you may have Tomcat running on port 8080, you may want to specify a different port by using the server.port argument. In this case, run Grails by typing in grails -Dserver.port=8090 run-app in the terminal window.

10. Once the application is loaded successfully, you should have an Employee table in the database. Creating a new Employee using the app should create a new record in the table.

