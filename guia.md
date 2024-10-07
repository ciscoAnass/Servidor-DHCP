## Configuracion de redes

### 1. Configuración de red :
Asumimos la siguiente configuración de red:
    
- **Servidor (Debian 1)** - Red Interna: 192.168.1.1/24

- **Failover (Debian 2)** - Red Interna: 192.168.1.2/24

- **Relay (Debian 3)** - 2 Interfaces (Red Interna ):
  
- - IP en la red del Cliente: 192.168.1.3/24

- - IP en la red del Servidor: 192.168.2.1/24

- **Cliente (Debian 4)** - Red Interna : 192.168.2.10/24


***
- Vamos a asignar las Ip's a las Máquinas :

Servidor :

<img src="/img/ips.png" alt="red servidor" width="500" />

FAILOVER :

<img src="/img/ipf.png" alt="red Failover" width="500" />

RELAY :

<img src="/img/ipr.png" alt="red Relay" width="500" />

CLIENTE :

<img src="/img/ipc.png" alt="red Cliente" width="500" />

***

## Instalamos los paquetes necesarios en cada Máquina :


**Servidor :**
```bash
apt update
apt install isc-dhcp-server
```

**Failover :**
```bash
apt update
apt install isc-dhcp-server
```

**Relay :**
```bash
apt update
apt install isc-dhcp-relay
```

**Cliente :**

- En el cliente no hace falta instalar ningún paquete, pero es recomendable actualizar el repositorio.

```bash
apt update
```

***
## Comprobacion de connectividad :

- Para comprobar la conectividad entre el cliente y el servidor, normalmente hacemos un ping desde el cliente al servidor o desde el servidor al cliente.
  
<img src="/img/pingc.png" alt="red servidor" width="500" />


- Ahora editamos el archivo de configuración de red en el cliente, ubicado en **'/etc/network/interfaces'** , y configuramos la interfaz **'enp0s3'** en modo DHCP.

  <img src="/img/dhcpclient.png" alt="Red Cliente DHCP" width="500" />

***
## Configuracion de la maquina Server :

### /etc/default/isc-dhcp-server

- Editamos el archivo **'/etc/default/isc-dhcp-server'** para configurar la tarjeta que escuchará las peticiones del cliente, que en este caso será **'enp0s3'** .
  
    <img src="/img/defaultserver.png" alt="red Cliente" width="500" />

### /etc/dhcp/dhcpd.conf

- Ahora configuramos el servicio **DHCP** en el Servidor :

    <img src="/img/dhcpserver.png" alt="red Cliente" width="500" />

- Ahora tenemos que reninciar el Servicio **DHCP** :

```bash
systemctl restart isc-dhcp-server
systemctl status isc-dhcp-server
```

- Ahora el Servicio debería estar Activo

<img src="/img/systemctlserver.png" alt="red Cliente" width="500" />




***
## Configuracion de la maquina **Failover** :

### /etc/default/isc-dhcp-server

- Al igual que en el servidor, tenemos que editar el archivo '/etc/default/isc-dhcp-server' para configurar la tarjeta que escuchará las peticiones del cliente, que en este caso será 'enp0s3'.

  <img src="/img/defaultf.png" alt="red Cliente" width="500" />

### /etc/dhcp/dhcpd.conf

- Ahora configuramos el servicio dhcp en el **Failover** :

    <img src="/img/dhcpfail.png" alt="red Cliente" width="500" />

- Ahora tenemos que reninciar el Servicio **DHCP** :

```bash
systemctl restart isc-dhcp-server
systemctl status isc-dhcp-server
```

- Ahora el Servicio debería estar Activo

<img src="/img/systemctlfail.png" alt="red Cliente" width="500" />

***
## Configuracion de la maquina RELAY :

### Habilitar el Forwading :

- Editamos el archivo **'/proc/sys/net/ipv4/ip_forward'** para permitir el reenvío de paquetes entre las interfaces de red:

```bash
echo '1' > /proc/sys/net/ipv4/ip_forward
```

<img src="/img/echo1.png" alt="red Cliente" width="500" />


- Para que este cambio sea persistente tras reiniciar, edita el archivo **'/etc/sysctl.conf'** y agrega la siguiente línea : 

```bash
echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf
```

<img src="/img/sysctl.png" alt="red Cliente" width="500" />


##  /etc/default/isc-dhcp-relay

- En este fichero tenemos que agregar la IP del servidor y el Failover y poner las dos tarjetas  que se conectan al cliente y al servidor y el failover que normalmente por virtualbox son por defecto : **“enp0s3” y “enp0s8”**

<img src="/img/defaultrelay.png" alt="red Cliente" width="500" />




***

## Comprobación de DHCP

### Parte 1 : Comprobación del Servidor

- Hemos terminado de configurar todas las máquinas (Servidor, RELAY, FAILOVER). Ahora toca comprobar si el DHCP funciona bien y si el cliente puede obtener una IP dinámica del servidor.
  
<img src="/img/dhcpcomp1.png" alt="red Cliente" />


### Parte 2 : Comprobación del FAILOVER

- Después de comprobar que el cliente puede obtener una IP dinámica del servidor y todo funciona correctamente, podemos apagar el servidor o detener el servicio 'isc-dhcp-server' para verificar si el cliente puede obtener una IP dinámica de la máquina FAILOVER.

```bash
systemctl stop isc-dhcp-server # En la Maquina Servidor
```

 <img src="/img/dhcpcomp2.png" alt="red Cliente"  />
