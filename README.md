# 🌐 Guía Básica de DHCP, Relay y Failover

## 🧩 ¿Qué es DHCP?

El **Protocolo de Configuración Dinámica de Host** (DHCP) permite que los dispositivos obtengan una dirección IP automáticamente cuando se conectan a una red, eliminando la necesidad de configuraciones manuales.

### Que es Relay  ? 

El **Relay** actúa como intermediario, reenviando las solicitudes del cliente al servidor DHCP cuando están en redes distintas, asegurando que el cliente reciba su configuración de red.

### Que es Failover  ?

El **Failover** garantiza alta disponibilidad. Si el servidor DHCP principal falla, un servidor de respaldo toma el control, asegurando que la red siga operativa.

---

## ⚙️ Configuración de red

La red se configura con cuatro máquinas Debian, cada una con un rol específico:

1. **Cliente (Debian 1)**: IP: `192.168.1.10/24`
2. **Relay/Router (Debian 2)**: IP Cliente: `192.168.1.1/24`, IP Servidor: `192.168.2.1/24`
3. **Servidor DHCP (Debian 3)**: IP: `192.168.2.10/24`
4. **Failover (Debian 4)**: IP: `192.168.2.9/24`

---

## 🔗 Ver configuración

- [Servidor](servidor.md)
- [Failover](failover.md)
- [Relay](relay.md)
- [Cliente](cliente.md)

***


**Autor**: Anass Assim  
**Licencia**: Libre  
