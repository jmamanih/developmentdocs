# INSTALACION DE SERVIDORES EN CENTOS LINUX 

## Vi Editor commands

```
	ESC cambiar modo comando
	i		editar
	x		borrar carater adelante
	X		borrar carater atras
	u		deshacer ultimo cambio
	yy		copiar linea actual
	3yy		copiar 3 lineas por debajo del cursor
	dd		borra o corta una linea
	p		pegar linea debajo del cursor
	P		pegar linea por encima del cursor
	:w		guardar sin salir
	:wq		salir grabando
	:q!		salir sin grabar
	/		buscar adelante
	?		buscar atras
	h,j,k,l cursores
	ctrl+u	mover pagina hacia arriba
	ctrl+d	mover pagina hacia abajo
	
	# vi archivo	//	Crear y editar un archivo
```

## NETWORK CONFIG

```sh
Configuración de Red
	# system-config-network
	ó	
	# system-config-network-tui
	# service network restart		//	ó  /etc/init.d/network restart

Puertos activos
	# netstat –l

Ver asignacion de IPs
	# ipconfig --all
```

Habilitar arranque automatico de interface de red (eth0)

```
	# vim /etc/sysconfig/network-scripts/ifcfg-eth0

		BOOTPROTO=none
		DEVICE=eth0
		IPADDR=192.168.1.10 # your IP address
		NETMASK=255.255.255.0 # your netmask
		NETWORK=192.168.1.0 
		ONBOOT=yes				# <- change for yes

	# chkconfig network on
	# service network restart
	# shutdown -r now
```
	
## PORTS

```
	# netstat -lntu    				// Listado de puertos 
	# lsof -i TCP| fgrep LISTEN		// Puertos que estan escuchando
```

## KILL PROCESS

```
// Remove packageKit bloc yum in Centos 7
	# sudo kill $(cat /var/run/yum.pid)
```

=======================================================================================
> INSTALL VMWARETOOLS CENTOS 
=======================================================================================
	>> CentOS 6.x 64-bit, vSphere ESXi 5.1
		# yum -y install http://packages.vmware.com/tools/esx/5.1/repos/vmware-tools-repo-RHEL6-9.0.0-2.x86_64.rpm

		vSphere ESXi 5.5

		# yum -y install http://packages.vmware.com/tools/esx/5.5/repos/vmware-tools-repo-RHEL6-9.4.0-1.el6.x86_64.rpm

		Install VMware-Tools

		# yum -y install vmware-tools-esx-nox
		
	>> For Centos 6.6
	1.
		# yum install make gcc kernel-devel perl kernel-headers glibc-headers -y
	2. Open vShere Client, open Console, Menu VM, Guest, Install/Upgrade VMWare Tools
	3. Mount cd in vSphere: VMwareTools, Copy and extract VMwareTools file:
		# cp /mnt/cdrom/VMwareTools-xxxxxxxx.tar.gz /tmp/
		# cd /tmp/
		# tar xvfz VMwareTools-xxxxxxxx.tar.gz

	4. Install the tools with default settings:
		# cd /tmp/vmware-tools-distrib
		# ./vmware-install.pl -d
		Clean up temporary files in TMP folder:
		# rm -rf /tmp/*	
	
	>> For Centos 7
	# yum -y install open-vm-tools
	# systemctl start vmtoolsd.service
	# systemctl enable vmtoolsd.service
	# vmware-toolbox-cmd -v						// version

=======================================================================================
> RPM
=======================================================================================
Instalación de paquetes
	# rpm –qa | grep paquete    // buscar
	# rpm –e paquete			// desinstalar
	# rpm –ivh paquete-x.rpm	// instalar
	# rpm –Uvh paquete-x.rpm	// instalar y actualizar

=======================================================================================
> YUM
=======================================================================================
	(*) Error YUM: (28, 'Operation too slow. Less than 1 bytes/sec transfered the last
	30 seconds') Trying other mirror.
	
	Solved:
	# yum clean all
	# vi /etc/yum.conf
		installonly_limit=5
		timeout=300 # <- add, default is 30				
		minrate=100 # <- add, default is 1000
		bugtracker=http:\\...
		
	# shutdown -r now


	# yum update					// 	Actualización del sistema con todas 
										las dependencias que sean necesarias
	# yum search cualquier-paquete	// 	Realizar una búsqueda de algún paquete
										o término en la base de datos en alguno 
										de los depósitos yum configurados en el
										sistema:
	# yum remove cualquier-paquete	// 	Desinstalación de paquetes junto con 
										todo aquello que dependa de éstos
	# yum list available | less		// 	Listado de todos los paquetes disponibles
										en la base de datos yum y que pueden
										instalarse
	# yum list installed | less		//	Listado de todos los paquetes instalados
										en el sistema
	# yum clean all					//	Limpieza del sistema.
	# yum grouplist					// 	Lista grupos de paquetes instalados
	
	
=======================================================================================
> SAMBA
=======================================================================================
Instalación Samba
	# yum install samba
	# yum install samba-client		// Habilita smbpasswd en Centos 7
	# service smb start				//	Habilitar en el firewall los puestos:  
										TCP 139, 445 UDP 137, 138 Samba y Samba Client  
Configurar Samba
	# su admin
	$ cd /home/admin
	$ mkdir Compartido
	$ su -
	# vi /etc/samba/smb.conf
		[Compartido]
        	comment = Carpeta Compartida de Linux
	        path = /home/admin/Compartido
			valid users = admin
			read only = no
    	    guest ok = yes
        	directory mode = 0777
			
	# service smb restart			//	Reiniciar servicio samba
	# chcon –t samba_share_t /home/admin/Compartido	
									//	Change security context for samba
	# chkconfig smb on				//	Configurar arranque automatico
	# chkconfig --list 
	
	# Habilitar en el Firewall el puerto Samba
	
	# chmod 0777 /home/admin/Compartido

Habilitar usuario samba
	# smbpasswd -a admin			//	Asignar password samba
	# smbpasswd -e admin 			//	Habilitar usuario samba 	
	
Probar conexión Samba
	\\servidorsamba\Compartido		//	Ingresar nombre de usuario habilitado samba y
										contraseña samba

***************************************	
>> Enable Samba in Centos 7
***************************************
	# systemctl enable smb.service
	# systemctl enable nmb.service
	# systemctl restart smb.service
	# systemctl restart nmb.service
	
	# firewall-cmd --permanent --zone=public --add-service=samba
	# firewall-cmd --reload
										
										
=======================================================================================
> FIREWALL
=======================================================================================
Instalar
	# yum system-config-firewall
	
Desactivar firewall
	# chkconfig iptables off
	# chkconfig --list |grep iptables

Habilitar puertos tcp
	# vi /etc/sysconfig/iptables
	
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT 
	# service iptables restart			

=======================================================================================
> JAVA
=======================================================================================
Version de Java
	# java –version     

Instalación Java JRE
	# rpm –ivh jre7u10...x.rpm  

Instalar JDK
	# rpm -Uvh jdk7u...rpm

=======================================================================================
> POSTGRES
=======================================================================================
Instalación de Postgres
	(1)
	# yum install postgresql92 postgresql92-devel postgresql92-server 
		      postgresql92-libs postgresql92-contrib
	(2)
	# chmod +x postgresql-9.2.2-1-linux-x64.run
	
	3)
	# ./postgresql-9.2.2-1-linux-x64.run

Servicios Postgres

	# service postgresql-9.2 initdb
	# service postgresql-9.2 start
	# service postgresql-9.2 stop

Configurar el entorno de Postgres
	# vim /var/lib/pgsql/.bash_profile
		PATH=$PATH:$HOME/bin:/usr/pgsql-9.2/bin
		export PATH

Configurar clave de Postgres
	# su - postgres
	# psql postgres postgres
	# bash-4.1$ psql postgres postgres
		psql (9.2.1)
		postgres=# alter user postgres with password 'CLAVE';
		ALTER ROLE
		postgres=#
		
Configurar el archivo pg_hba.conf 
	# vi /opt/PostgreSQL/9.3/data/pg_hba.conf

		# IPv4 local connections:
		host all all 127.0.0.1/32 	    md5
		host all all 100.100.100.130/32 md5

Para que los cambios tengan efectos, volver a cargar el archivo pg_hba.conf
	# su - postgres
	-bash-4.1$ pg_ctl reload
    server signaled

Configurar acceso remoto a Postgres
	#vi /opt/PostgreSQL/9.3/data/postgresql.conf
	listen_addresses = '*' # what IP address(es) to listen on;

Configurar el limite de procesos concurrentes
	#vi /var/lib/pgsql/9.2/data/postgresql.conf
	max_connections = 250	# (change requires restart)
	Reiniciar el servicio Postgres
	# service postgresql-9.2 restart

Configurar Postgres para que inicie automáticamente
	# chkconfig postgresql-9.2 on


=======================================================================================
> APACHE TOMCAT
=======================================================================================
Instalación Tomcat
	# mkdir /usr/local/tomcat7
	# tar xvzf apache-tomcat-7.0.37.tar.gz

Configurar usuario Tomcat
	# vi /usr/local/tomcat7/conf/tomcat-users.xml
	<tomcat-users>
		<user name="tomcat" password="tomcat" roles="admin-gui,manager-gui"/>
	</tomcat-users>
Arranque Tomcatcd
	# cd /usr/local/tomcat7/bin/
	# ./startup.sh

Parada Tomcat
	# cd /usr/local/tomcat7/bin/
	# ./shutdown.sh

Ampliar memoria PERM GEN Tomcat
	# vi /usr/local/tomcat7/bin/catalina.sh
	JAVA_OPTS=“-XX:MaxPermSize=1024m”

Configurar tamaño de archivo War a publicar en Tomcat
	# vi /usr/local/tomcat7/webapps/manager/WEB-INF/web.xml. 
		<multipart-config> 
		<!– 50MB max –> yu
		
		<max-file-size>209715200</max-file-size> 
		<max-request-size>209715200</max-request-size> 
		<file-size-threshold>0</file-size-threshold> 
		</multipart-config> 

Configurar Puerto Tomcat
	# vi /usr/local/tomcat7/conf/server.xml
	Connector port="9090" protocol="HTTP/1.1" connectionTimeout="20000" 
			edirectPort="8443"/>
*****************************************************
>> Enable Firewall port 8080 in Centos 7
*****************************************************

	# firewall-cmd --zone=public --add-port=8080/tcp --permanent  
	# firewall-cmd --reload 

=======================================================================================
> FONTS 
=======================================================================================
Configurar fonts de Windows en Linux Centos
	# cp –ru /usr/compartido/fonts/* /usr/share/fonts		// -ru  copiar con 
																directorios y 
																sobrescribir
	# fc-cache –f –v
	# shutdown -r now	


=======================================================================================
> FTP
=======================================================================================
Configuring ftp server on Centos 6:

	Install ftp
	# yum -y install vsftpd
	# vim /etc/vsftpd/vsftpd.conf
		anonymous_enable=NO
		local_enable=YES
		write_enable=YES
		chroot_local_user=YES

	Create a folder where you want to store FTP data
	# mkdir /ftp
	# useradd -d /ftp/carpeta juan				## Lista de Usuarios:  cat /etc/passwd
	# passwd juan								## Asignar propietario a una archivo o carpeta:
		New password:							## chown juan:juan carpeta
	# ls -l /ftp

	Start vsftpd service by issuing the below command.
	# service vsftpd start
	# chkconfig --levels 235 vsftpd on

	//	Enable port 21 FTP from FIREWALL
		
	# vim /etc/selinux/config and find the line
	  SELINUX=disabled
	  
	# chmod 755 /ftp/carpeta	//<- opcional
	# setenforce 0			    //<- opcional para habilitar en el momento
	# shutdown -r now

	Install Client FTP (Example: Core FTP LE)
		Site Name: Test FPT
		Host: 10.10.10.5
		Username: juan
		Password: juan1234
		Port: 21
		Connection: FTP
		-> Connect
		
=======================================================================================
> LAMP
=======================================================================================
> Install Apache

	# yum install httpd -y
	# service httpd start
	# chkconfig httpd on

	Allow Apache server default port 80 through your firewall/router if you want to connect from remote systems. To do that, edit file /etc/sysconfig/iptables,
	# vi /etc/sysconfig/iptables
		[...]
		-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEP
		[...]
	# service iptables restart

	Test Apache:
	Open your web browser and navigate to http://localhost/ or http://10.10.10.5

> Install MySQL

	# yum install mysql mysql-server -y
	# service mysqld start
	# chkconfig mysqld on
	
	Setup MySQL root password
	# mysql_secure_installation

		Enter current password for root (enter for none):     ## Press Enter ## 
		Set root password? [Y/n]     ## Press Enter ##
		New password:                ## Enter new password ##
		Re-enter new password:       ## Re-enter new password ##
		Password updated successfully!
		Reloading privilege tables..
		... Success!

		Remove anonymous users? [Y/n]     ## Press Enter ##
		... Success!

		Disallow root login remotely? [Y/n]     ## Press Enter ## 
		... Success!
	
		Remove test database and access to it? [Y/n]     ## Press Enter ##
		- Dropping test database...
		... Success!
		- Removing privileges on test database...
		... Success!

		Reload privilege tables now? [Y/n]     ## Press Enter ##
		... Success!

		Cleaning up...

		Thanks for using MySQL!

> Install PHP
	# yum install php -y

	Test PHP
	# vi /var/www/html/info.php
		<?php
		phpinfo();
		?>
	# service httpd restart	
	
	http://localhost/info.php

	Get MySQL support in your PHP, you should install “php-mysql” package
	
	# yum install php-mysql -y
	# service httpd restart	
	
	Now open the phptest.php file in your browser using 
	http://localhost/info.php       # -> Scroll down and you will see the mysql module
									#    will be presented there.

> Install phpmyadmin
	Add the EPEL Repository
	# rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

	Install phpMyAdmin
	# yum -y update					# opcional
	# yum -y install phpmyadmin
	# service httpd restart
	
	Test PhpMyAdmin
	http://localhost/phpMyAdmin	

	Error: Forbidden
	# vim /etc/httpd/conf/httpd.conf

		<Directory "/usr/share/phpMyaAdmin">
			Order allow,deny     # <- add
			Allow from all     	 # <- add
			...
		</Directory>
	
	# service httpd restart

										
=======================================================================================
> DNS
=======================================================================================
 (*) PERFIL DE CONFIGURACION  	
     ------------------------------------------------------ 
     IP VIRTUAL (FIREWALL): 200.105.174.210 -> 10.10.10.6
						    200.105.174.211 -> 10.10.10.3	
     ------------------------------------------------------ 
	 Servidor Maestro DNS	 
     ------------------------------------------------------
     Dirección IP:     10.10.10.6
     Host-name:        dns.easba.gob.bo
     OS:               Centos 6.7 final
     ------------------------------------------------------
     Servidor Esclavo DNS
     ------------------------------------------------------
     Dirección IP:     10.10.10.7
     Host-name:        dns2.easba.gob.bo
     OS:               Centos 6.7 final
     ------------------------------------------------------
     Máquina Cliente para utilizar DNS
     ------------------------------------------------------
     Dirección IP:     10.10.10.3
     Host-name:        sistema.easba.gob.bo
     OS:               Centos 6.7 final
	 ------------------------------------------------------
	 	
	 # ifconfig | grep inet				// Ver configuracion de IP
	 # hostname							// Verificar nombre Host
	 # cat /etc/redhat-release			// Version de Centos Linux
	 
	 > Cambiar Host Name
	 
	 # vim /etc/sysconfig/network
	 # vim /etc/hosts
		127.0.0.1$		localhost.localdomain	localhost
		10.10.10.6 		dns.easba.gob.bo		dnsserver
	 # hostname
	 # service network restart
	 # hostname 	
	 
	 > Instalar DNS Servidor Maestro
	 # yum install bind* -y
	 
	 > Configuración de BIND
	 # vim /etc/named.conf	
	 

	
=======================================================================================
> MYSQL ADVANCED SERVER
=======================================================================================
Verificar si esta instalado MySQL
	# rpm -qa | grep -i mysql
	ó
	# rpm -qa | grep MySQL

Instalación y Configuración	
	# rpm -ivh MySQL*.rpm		// 	Instalar MySQL 
	# service mysql status 		// 	Comprombar servicio MySQL
	# cat /root/.mysql_secret	//	Ver clave asignada randomicamente a MySQL 	
									The random password set for the root user
									at Tue Apr  9 16:02:10 2013
									(local time): Vc6WLaX3
	# mysql -uroot -p			//	Ingresar a la consola mysql, escribir la
									contraseña randomica

	mysql>SET PASSWORD FOR 'root'@'localhost'=PASSWORD('mysql');	//	Cambiar
																		contraseña
	mysql>CREATE USER 'admin'@'%' IDENTIFIED BY 'adminmysql'; 		//	Crear un 
																		usuario
																		administrador
																		de mysql
	mysql> GRANT ALL ON *.* TO 'admin'@'%' WITH GRANT OPTION; 		//	Otorgar todos
																		los permisos
	mysql> quit						  								//	Salir de la
																		consola

Habilitar puerto 3306 en el firewall
	# vi /etc/sysconfig/iptables
	
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT	
	
	# service iptables restart				  						//	Reiniar el 
																		Firewall
	# chkconfig mysql --level 2345 on			  					// 	Configurar 
																		Arranque 
																		automatico 
																		de MySQL
	
	// Probar conexion desde Navicat
		Host Name/IP Host: 	100.100.100.30
		Port:				3306
		Username:			admin	
		Password:			**********
		Test Connection		-> Connection Successful!
	
=======================================================================================
> GLASSFISH
=======================================================================================
Instalacion de Glassfish Server
	// Instalar JDK, copiar el archvio  glass...sh a /opt/glassfish
	# chmod +x glassfish-3.0.1-unix-ml.sh
	# ./glassfish-3.0.1-unix-ml.sh 					//	Elegir la opcion personalizada
													//	Habilitar en el firewall los 
														puertos 4848 y 8080
Configurar PermGem 
	-> Ingresar como admin por el puerto 4848
	-> Elegir la opcion: Configurations, Default Config (Server Config), 
	   JVM Settings, JVM Options, 
	   -XX:PermSize=512m  -XX:MaxPermSize=1024m, Save,->Restart Required, Restart

Habilitar administracion remota
	-> http://localhost:4848
	-> Opcion server (Admin Server), Secure Administration, Enable Secury Admin, 
	   Restart Glassfish
	-> https://10.10.10.20:4848 
		
							
=======================================================================================
> PASSWORD ADMIN ADN RESCUE SYSTEM
=======================================================================================
Lista de todos los Usuarios
	#cat /etc/passwd
	#getent passwd | cut –d”:” –f1	
	#ls /home

Crear usuario
	# adduser cliente
	# passwd cliente

Eliminar usuario
	# userdel cliente
	# rm -dfr /home/cliente

Ver configuración de usuario
	# id root

Ver grupos
	# cat /etc/group	
		
Cambiar contraseña (root)
	1. Reiniciar el S.O
	2. ESC al momento de arranque
	3. Seleccionar la opcion: CentOS(2.6...) y presionar la tecla 'e'	
	4. Seleccionar la opcion: kernel /vmlinuz-2.6...  y presionar la tecla 'e' 
	   al final de la linea escribir 1 y ENTER
	5. Al regresar al menu anterior presionar la tecla 'b'		   
	6. Escribir el comando: passwd
	7, Asignar nueva contraseña root y reiterar
	8. reiniciar el S.O.: exit.

	Para cambiar la contraseña de otro usuario escribir: # passwd usuario
	listar todos los usuarios: # cat /etc/passwd
	o ver usuarios de sistema: # ls -l /home

Cambiar descripción de usuario
	# su -
	# vi /etc/passwd			//	Cambiar descripcion entre : ???? :
	# logout
	
=======================================================================================
> FILES
=======================================================================================
Buscar archivos
	# find / -type f -name  archivo*	// Buscar archivos
	# find / -type d -name directorio*	// Buscar directorios

Menú de arranque Linux
	# vi /boot/grub/menu.lst

Reinicio rápido
	# telinit 6

Listar archivos
	# ls –l  							// Con permisos
	# ls –a  							// Ocultos
	
Copiar archivos 
	# cp /usr/local/tomcat/*  /home/admin
	# cp –ru /usr/compartido/fonts/* /usr/share/fonts	// 	-ru copiar con 
															directorios y 
															sobrescribir 
Renombrar o mover archivos
	# mv archivo.dat nombre.dat							//	Para renombrar

Eliminar directorio
	# rm -dfr /carpeta

Otorgar permisos
	# chmod a+x+r archivo

Colores
	Negro	= 	comunes y corrientes
	Azul	= 	directorios
	Verde 	= 	ejecutables
	Cyan 	= 	archivos de mapeo o enlaces o links, 
				sirven para tener rutas alternativas
				a un determinado objetivo

=======================================================================================
> FILES ATTRIBUTES
=======================================================================================	
	#chattr -RV +a 	// R es para que haga efecto en Directorios
					// V para ver atributos
					// +i bloquea todo, no permite copiar ni borrar
					// -i desbloquea todo
					// +a permite copiar archivos pero no borrar
					// -a quita el atributo +a
	  

=======================================================================================
> SERVIDOR
=======================================================================================
Cambiar nombre de servidor
	# hostname
	# hostname nuevo-nombre-srv
	
=======================================================================================
> SERVICIOS ó DEMONIOS
=======================================================================================
Añadir o quitar servicios al inicio del sistema
	# chkconfig --list								//	Estado de servicios
	# chkconfig --level 345 httpd on  				//	Iniciar el servicio httpd en 
														los niveles 3, 4 y 5
	# chkconfig  httpd off							//	Inhabilitar el servicio
	# chkconfig –-add mysql
	# chkconfig --del mysql

Arranque manual de Servicios: directorio init.d
	# /etc/rc.d/init.d/smb start

=======================================================================================
> SERVICIOS DESDE ARRANQUE DE SISTEMA
=======================================================================================	
Iniciando servicios 
	# init 5	//	0 Detener o apagar el sistema
				//	1 Modo monousuario, utilizado para mantenimiento del sistema
				//	2 Modo multiusuario, pero sin soporte de red
				//	3 Modo multiusuario completo, con servicios de red
				//	4 No se usa, puede usarse para un inicio personalizado
				//	5 Modo multiusuario completo con inicio gráfico ( X Window)
				//	6 Modo de reinicio (reset) 
Configurar nivel de arranque
	# vi /etc/inittab 	

		id:5:initdefault:

Forzar Inicio
	# sync; init 0		//	Forzar apagado guardando datos en disco duro
	# sync; init 6 		//	Forzar reinicio	guardando datos -> No usar
	
=======================================================================================
> TECLADO
=======================================================================================
Configurar Teclado
	# system-config-keyboard
	# shutdown -r now

=======================================================================================
> LOG - Historial de Eventos
=======================================================================================
Ver registro Log
	# lastlog
	# vi /var/log/secure

=======================================================================================
> SSH
=======================================================================================
Instalar SSH
	# yum -y install openssh openssh-server openssh-clients 

Configurar SSH
	# vi /etc/ssh/sshd_config
		Port 22022							//	Cambiar puerto
												default 22 
											//	Habilitar el puerto 
												22022 en el Firewall
		PermitRootLogin no					// 	Restringir acceso 
												usuario root 
												inicialmente
		AllowUsers 	admin@100.100.100.33 
					admin@100.100.100.130	// 	Permitir acceso de 
												usuarios 
	# service sshd restart					// 	Reiniciar servicio ssh

=======================================================================================
> VNC SERVER
=======================================================================================
Instalación	
	# yum install tigervnc-server vnc-server	//	Instalar vnc-server
	# chkconfig vncserver on 					//	Configurar Arranque automatico
	# useradd vncuser							//	adicionar usuario vnc
	# passwd vncuser							//	contraseña usuario
	# su vncuser
	$ vncpasswd									//	Asignar contraseña de conexion
													remota 
	$ su admin									// 	Habilitar usuario admin como
													usuario VNC
	$ vncpasswd									//	Asignar contraseña de conexion
													remota
	$ ls -a /home/admin/.vnc/					//	Verificar creación de contraseña
													VNC
	$ exit
	$ su -
	# vi /etc/sysconfig/vncservers				// Habilitar Usuarios
		
		VNCSERVERS="2:admin 3:vncuser"
		VNCSERVERARGS[2]="-geometry 1024x768"	
		VNCSERVERARGS[3]="-geometry 1024x768"	//	Habilitar en el firewall puertos:
													5900 -> Service vncserver
													5901 -> Reservado
													5902 -> Usuario 2
													5903 -> Usuario 3
													5904 -> etc.	
	# service vncserver start

	# yum install pixman pixman-devel libXfont	//	Instalar libFonts

Conexion remota
	RUN: VNC-Viewer
		-> VNC Server: 100.100.100.31:2			//	Conexion remota mediante Usuario 2
		-> Encryption: Prefer on
 		   -> password:  contraseña usuario 2 (admin)
		   
		-> VNC Server: 100.100.100.31:3			//	Conexion remota mediante Usuario 3
		-> Encryption: Prefer on
 		   -> password:  contraseña usuario 3 (vncuser)   
		
=======================================================================================
> SERVER OFF
=======================================================================================
	# poweroff				// Para apagar
	# shutdown -h now		// Apagar ahora
	# shutdown -r now		// Reiniciar ahora
	# halt					// Forzar apagado
	# reboot				// Forzar reinicio
	# telinit 6    			// Reiniciar en el nivel 6 

=======================================================================================
>> SET DATE-TIME CENTOS 7 
=======================================================================================
	# timedatectl							// get date time
	# timedatectl set-time 2014-12-08
	# timedatectl set-time 10:24:34

=======================================================================================
> MISCELANIA
=======================================================================================
Administración de Servicios en modo Gráfico
	# yum install system-config-services
	# system-config-services

Versión de Linux
	# cat /proc/versión
	# uname –m				// ver arquitectura SO Linux

demonio = servicio

Shortcuts

	Ctrl+Alt+Flecha Izq/Der = Cambiar espacios de trabajo
	Ctrl+Alt+D   			= Minimizar todas las ventanas 
	Ctrl+Alt+L   			= Bloquear pantalla 
	Alt+F7	     			= Mover las ventanas con las teclas de flechas
	Mayús + F10  			= Método abreviado para el botón derecho del ratón












