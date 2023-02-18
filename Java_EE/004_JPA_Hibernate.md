# JPA Hibernate
## Create Project

* Open Eclipse Neon
* Menu New, Maven Project, check Create a simple project, Next
* Artifact: 
    * Group id: org.unisoft
    * Artifact id: jpa-hibernate
    * Version: 1.0.0-SNAPSHOT
    * Finish

## Config Eclipse Neon Proxy

    Menu Window, Preferences, General, Network Connection
    Active Provider: Manual, click over HTTP, Button Edit
    Host: 127.0.0.1
    Port: 3122
    Ok, Apply, Ok


## Config Plugins

Open Project Explorer
Expand jpa-hibernate, click porm.xml, tab porm.xml
Edit porm.xml

```sh
<project xmls="http://...">
	...
	<version>1.0.0-SNAPSHOT</version>
	<dependencies>
	</dependencies>
	<build>
	</build>
</project>
```


