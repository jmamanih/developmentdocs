# Firmador Digital
## Instalar

Install Java

Install OpenSC
```
download OpenSC.0.16.0.dmg
install OpenSC

```
Testing OpenSC
```
opensc-tool --list-readers

opensc-tool --reader 0 --atr

opensc-tool --reader 0 --name

```
URL Driver connection: /Library/OpenSC/lib/opensc-pkcs11.so

URL Firmador: https://localhost:3200/

Open DemofiFX.jar, config
