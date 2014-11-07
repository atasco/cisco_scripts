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
set username soporte

set cfg_dir ./etc
set log_dir ./logs
set log_name sw_chen.log

set ssw_file $cfg_dir/ssh_switches.dat
set tsw_file $cfg_dir/telnet_switches.dat
set swpd swpd.enc
set org_enablepd org_enable.enc
set new_enablepd new_enable.enc

exp_internal 0
log_user 0

set username soporte                       # user account name 

set cfg_dir ./etc                          # directory with configuration files
set log_dir ./logs                         # directory with log files
set log_name sw_chen.log                   # log file name

set ssw_file $cfg_dir/ssh_switches.dat     # file with IP for ssh access switches
set tsw_file $cfg_dir/telnet_switches.dat  # file with IP for telnet access switches
set swpd swpd.enc                          # file with user encrypted password
set org_enable org_enable.enc              # file with original enable encrypted password
set new_enable new_enable.enc              # file with new enable encrypted password

exp_internal 0                             # debugging: 0=no 1=yes
log_user 1                                 # spawn process output: 0=no 1=yes
