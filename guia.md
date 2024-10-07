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
- Vamos a asignar las Ip's A las Maquinas :

Servidor :
<img src="/img/ips.png" alt="red servidor" width="500" />

FAILOVER :
<img src="/img/ipf.png" alt="red Failover" width="500" />

RELAY :
<img src="/img/ipr.png" alt="red Relay" width="500" />

CLIENTE :
<img src="/img/ipc.png" alt="red Cliente" width="500" />

***

## Instalamos Los paquetes necesarios por cada maquina :


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

- En el Cliente no hace falta intalar ningun paquete pero es recomendable actualizar el repositorio

```bash
apt update
```

***
## Comprobacion de connectividad :

- Para comprobar la Connectividad entre el cliente con el Servidor , normalmente hacemos un Ping del Cliente al servidor o del Servidor al Cliente :

  
<img src="/img/pingc.png" alt="red servidor" width="500" />


- Y Ahora editamos el ficher de configuracion Red en el cliente '/etc/network/interfaces' y ponemos la interfaz 'enp0s3' por modo dhcp :

  <img src="/img/ipc2.png" alt="red Cliente" width="500" />

***
## Configuracion de la maquina Server :

### /etc/default/isc-dhcp-server

- Editamos el fichero '/etc/default/isc-dhcp-server' , para configurar la tarjeta que va a escuchar las peticiones del cliente, en este caso seria 'enp0s3'.

    <img src="/img/defaultserver.png" alt="red Cliente" width="500" />

### /etc/dhcp/dhcpd.conf

- Ahora configuramos el servicio dhcp en el Servidor :

    <img src="/img/dhcpserver.png" alt="red Cliente" width="500" />

- Ahora tenemos que reninciar el Servicio DHCP :

```bash
systemctl restart isc-dhcp-server
systemctl status isc-dhcp-server
```

- Ahora el Servicio suele ser Activo

<img src="/img/systemctlserver.png" alt="red Cliente" width="500" />

***





