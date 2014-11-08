# Expect scripts para automatizar diferentes tareas en Cisco IOS

## SW_CHEN: Cambiar la password de *enable* en un conjunto de switches/routers

### Uso

``` sh
sw_chen <ENABLE> <KEY>
```

Donde:

* ENABLE: Poner password nueva o la password original (NEW o ORG)
* KEY: Llave de cifrado para la password de acceso al dispositivo

### Configuración

Ajustar los siguientes parámetros:

* username: Cuenta de usuario con permisos de administración (por defecto *soporte*).
* cfg_dir: Directorio donde se encuentran los ficheros de configuración (por defecto *./etc*).
* log_dir: Directorio donde se guardarán los ficheros de log (por defecto *./logs*).
* log_name: Nombre del fichero de log (por defecto *fg_vpn.log*).
* ssw_file:  Nombre del fichero con las IPs de los switches/routers accesibles a través de SSH (por defect *ssh_switches.dat*).
* tsw_file:  Nombre del fichero con las IPs de los switches/routers accesibles a través de TELNET (por defect *telnet_switches.dat*).
* swpd: Nombre del fichero con la password cifrada del usuario (por defecto *swpd.enc*).
* org_enablepd: Nombre del fichero con la password cifrada de ENABLE original (por defecto *org_enable.enc*).
* new_enablepd: Nombre del fichero con la password cifrada de ENABLE nueva (por defecto *new_enable.enc*).
* exp_internal: Activación/desactivación de debugging (0=no 1=si).
* log_user: Activar/desactivar la salida del proceso de spawn (0=no 1=si).

#### Ficheros

Se guardan en el subdirectorio `etc` ubicado en el directorio desde el que se lanza el script. Son los siguientes:

* SSL SWITCH/ROUTER: Fichero en texto plano que contiene las IPs de los switches/routers accesibles vía SSH.
* TELNET SWITCH/ROUTER: Fichero en texto plano que contiene las IPs de los switches/routers accesibles vía TELNET.

> Por ejemplo, `ssh_switches.dat`:
>  
>  10.1.1.1    
>  10.1.2.1
>  ...

* PASSWORDS CIFRADAS: Fichero con las password cifradas `swpd.enc`, `org_enable.enc` y `new_enable.enc`.

### Cifrado de passwords

Para cifrar la password, guardada en texto plano en un fichero (swpd.dec):

``` sh
$ openssl des3 -salt -in swpd.dec -out swpd.enc
enter des-ede3-cbc encryption password:
Verifying - enter des-ede3-cbc encryption password:
```

La *KEY* que pasamos al script es la `des-ede3-cbc encryption password` que se solicita en el comando anterior.
