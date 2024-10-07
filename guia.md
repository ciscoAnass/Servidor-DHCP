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

