# MODEM MANAGER

## Instalacion

* Instalar [Modem Manager](https://www.freedesktop.org/wiki/Software/ModemManager/)

```sh
$ sudo apt-get install modemmanager
```
## Obtener datos del modems y verificar funcionamiento

* Escanear los modems conectados

```sh
$ sudo mmcli -S
```

* Listar los modems encontrados

```sh
$ sudo mmcli -L

Found 1 modems:
	/org/freedesktop/ModemManager1/Modem/0 [huawei] E303
```
*Donde 0 indica el ID del modem*

Obtener datos del modem con ID : **0**

```sh
$ sudo mmcli -m 0

-------------------------
 Hardware |   manufacturer: 'huawei'
          |          model: 'E303'
          |       revision: '22.318.35.00.00'
          |      supported: 'gsm-umts'
          |        current: 'gsm-umts'
          |   equipment id: '862567023898625'
 -------------------------
 ...
 -------------------------
 3GPP     |           imei: '862567023898625'
          |  enabled locks: 'none'
          |    operator id: '73603'
          |  operator name: 'TIGO'
          |   subscription: 'unknown'
          |   registration: 'home'
 -------------------------
 SIM      |           path: '/org/freedesktop/ModemManager1/SIM/0'

 -------------------------
 Bearers  |          paths: 'none'

```

## Ver estado del modem
Muestra la linea del modem y el saldo al mismo tiempo

```sh
$ sudo mmcli -m 0 --3gpp-ussd-status

```
## Habilitar el modem

```sh

$ sudo mmcli -m 0 -e

```
## Iniciar y Cerrar sesiones con el modem

Solicitar el estado de cualquier sesión USSD en curso

```sh
$ sudo mmcli -m 0 --3gpp-ussd-status

```
Iniciar session USSD con el modem dado el comando: COMMAND
Ej.
sudo mmcli -m 0 --3gpp-ussd-initiate='*123#'

```sh
$ sudo mmcli -m 0 --3gpp-ussd-initiate=COMMAND

```

Al iniciar una sesión USSD, se requiere de una respuesta para ello se debe responder con el comando:

```sh
$ sudo mmcli -m 0 --3gpp-ussd-respond=RESPONSE

```
donde RESPONSE son las opciones que presenta la red


Cancelar una sesión USSD en curso para un módem determinado.

```sh
$ sudo mmcli -m 0 --3gpp-ussd-cancel

```
## Ver redes disponibles

```sh
mmcli -m 0 --3gpp-scan --timeout=300

```

## Cargar creditos

Enviar una mensaje de texto al 171, con el numero secreto de la tarjeta

## Ver saldo de creditos

Verificar el credito mediante un código USSD

```sh
$ sudo mmcli -m 0 --3gpp-ussd-initiate='*123#'
```

*Donde *123# es el código de consulta de saldo del operador de telefonia celular*

## Comprar paquetes

```sh
    $ sudo mmcli -m 0 --3gpp-ussd-initiate='*222#'
    $ sudo mmcli -m 0 --3gpp-ussd-respond=1
```

## Monitorear acciones de los modems

Monitorear las acciones de los modems

```sh
$ sudo mmcli -M
```


## Envio de mensajes

Preparar un mensaje

```sh
sudo mmcli -m 0 --messaging-create-sms="text='Hola mundo modem manager',number='72067615'"
```

```sh
Successfully created new SMS:
	/org/freedesktop/ModemManager1/SMS/10 (unknown)
```
*El mensaje anterior se identifica con el ID **10***

Enviar mensaje de texto

```sh
sudo mmcli -s 10 --send
```

```sh
successfully sent the SMS
```

Ver lista de mensajes enviados

```sh
sudo mmcli -m 0 --messaging-list-sms
```
El estado del mensaje habrá cambiado de *unknown* a *send*

La respuesta de este comando devolverá algo como

```sh
Found 3 SMS messages:
	/org/freedesktop/ModemManager1/SMS/9 (received)
	/org/freedesktop/ModemManager1/SMS/10 (sent)
```



## Administracion del modem
Identificar modem

    $ sudo mmcli -S
    $ sudo mmcli -L

Comprar paquetes SMS

    $ sudo mmcli -m 0 --3gpp-ussd-initiate='*123#'

    $ sudo mmcli -m 0 --3gpp-ussd-initiate='*222#'

    $ sudo mmcli -m 0 --3gpp-ussd-respond=1
