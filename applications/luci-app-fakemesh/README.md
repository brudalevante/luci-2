## Introduction to fakemesh

Fakemesh is a network topology consisting of a `Controller (AC)` and one or more `Wired APs` and `Agents (Satellites)`. It is a hybrid network combining features of both `Wireless Mesh` and `AC+AP` configuration modes. In fakemesh, the `Wired APs` are connected to the `Controller (AC)` via wired connections, while the `Agents (Satellites)` connect wirelessly as STA nodes, forming a unified wireless (and wired) coverage network.

Deploying fakemesh is relatively straightforward. Simply connect the devices to the correct network, set their roles, configure the Mesh ID, and you're good to go. Because fakemesh integrates both wireless Mesh and AC+AP modes, it allows for seamless hybrid networking, enhancing the network's coverage range and reliability.

Currently, [X-WRT](https://github.com/x-wrt/x-wrt) has fakemesh functionality built in by default.

## Using fakemesh

### Unified format for accessing device addresses after a network is set up:

To access the controller:
- `http://controller.fakemesh/` or `http://ac.fakemesh/`

To access an AP:
- `http://{mac}.ap.fakemesh/` or `http://N.ap.fakemesh/`

Where `{mac}` is the MAC address of the AP (e.g., `{mac}=1122334455AB`), and `N` is the automatically assigned AP number (e.g., N=1, N=2, N=3, ...).

Examples:
```
http://1.ap.fakemesh/
http://1122334455AB.ap.fakemesh/
```

### Troubleshooting:

If an AP remains offline for approximately 3 minutes, it enters fault mode. In this mode, a default SSID is enabled to allow reconnection and reconfiguration.

The default SSID and password in fault mode are:
```
SSID: X-WRT_XXXX
PASSWD: 88888888
```

The management IP in fault mode is the gateway IP assigned by DHCP. For example, if a computer gets an IP in the `192.168.16.x` range, the AP management IP will be `192.168.16.1`.

## Basic Components of fakemesh

The network is composed of a `Controller (controller)` and one or more `APs`.

APs include two types:
- `Agent (Satellite)` and `Wired AP`.

**Controller (Controller):** 
Acts as the AC and gateway router, providing internet access, managing all connected Agents and Wired APs, and providing centralized wireless management.

**Agent (Satellite):** 
APs connected wirelessly using Mesh networking.

**Wired AP:** 
APs connected to the Controller via wired connections.

## Configuration Parameters for fakemesh

### 1. Mesh ID
   This is the unified ID for the fakemesh network. The controller, agents, and wired APs must all be configured with the same Mesh ID.

### 2. Key
   A shared encryption key for the network. If no encryption is required, you may leave this blank.

### 3. Band
   The wireless band used for networking. All devices must use the same band, either 5G or 2.4G.

### 4. Role
   Specifies the device type: Controller, Agent, or Wired AP.

### 5. Sync Config
   Determines whether Wi-Fi configurations are managed centrally by the Controller.

### 6. Access IP Address
   Assigns a specific management IP address to the controller for accessing its web interface.

### 7. Fronthaul Disabled
   Disables wireless forwarding at this node, preventing other APs from connecting through it.

### 8. Band Steer Helper
   For roaming assistance, you can select either [DAWN](https://github.com/fakemesh/dawn) or [usteer](https://github.com/fakemesh/usteer).

## Wireless Management

The Controller offers centralized wireless management, including the addition or removal of SSIDs, setting encryption methods, and adjusting channel widths.

## Controller in Bypass Mode

If the Controller is not used as a gateway or DHCP server, manual configuration is required. Users must configure the LAN IP, gateway IP, and DNS on the Controller manually. Additionally, the Controller's LAN port typically connects to a third-party gateway via DHCP to acquire an IP address. If a static IP is used, ensure the Controller and the gateway are on the same subnet and can communicate with each other. Otherwise, synchronization with other APs will fail.

## Introducción a fakemesh

Fakemesh es una topología de red que consta de un `Controlador (AC)` y uno o más `APs cableados (Wired AP)` y `Agentes (Satélites)`. Es una red híbrida que combina características de `Mesh inalámbrico` y configuraciones de `AC+AP`. En fakemesh, los `APs cableados` se conectan al `Controlador (AC)` mediante conexiones por cable, mientras que los `Agentes (Satélites)` se conectan de forma inalámbrica como nodos STA, formando una red unificada de cobertura inalámbrica (y cableada).

La implementación de fakemesh es relativamente sencilla. Basta con conectar los dispositivos al red correspondiente, configurar su rol, asignar el Mesh ID, y estará listo. Al combinar los modos de `Mesh inalámbrico` y `AC+AP`, fakemesh facilita la creación de redes híbridas, mejorando la cobertura y fiabilidad.

Actualmente, [X-WRT](https://github.com/x-wrt/x-wrt) integra fakemesh como función predeterminada.

## Usar fakemesh

### Formato unificado para acceder a las direcciones de los dispositivos una vez configurada la red:

Para acceder al controlador:
- `http://controller.fakemesh/` o `http://ac.fakemesh/`

Para acceder a un AP:
- `http://{mac}.ap.fakemesh/` o `http://N.ap.fakemesh/`

Donde `{mac}` es la dirección MAC del AP (por ejemplo, `{mac}=1122334455AB`), y `N` es el número de AP asignado automáticamente (por ejemplo, N=1, N=2, N=3, ...).

Ejemplos:
```
http://1.ap.fakemesh/
http://1122334455AB.ap.fakemesh/
```

### Solución de problemas:

Si un AP permanece desconectado durante aproximadamente 3 minutos, entra en modo de fallos. En este modo, se habilita un SSID predeterminado para permitir la reconexión y reconfiguración.

El SSID y la contraseña en el modo de fallos son:
```
SSID: X-WRT_XXXX
PASSWD: 88888888
```

La dirección IP de gestión en modo de fallos es la puerta de enlace asignada por DHCP. Por ejemplo, si un equipo recibe una IP en el rango `192.168.16.x`, la IP de gestión del AP será `192.168.16.1`.

## Componentes básicos de fakemesh

La red está compuesta por un `Controlador (Controller)` y uno o más `APs`.

Los APs incluyen dos tipos:
- `Agente (Satellite)` y `AP Cableado`.

**Controlador (Controller):** 
Funciona como AC y enrutador de salida, proporciona acceso a la red, gestiona los Agentes y APs cableados conectados, y centraliza la administración de la red inalámbrica.

**Agente (Satellite):** 
APs conectados de forma inalámbrica usando Mesh Networking.

**AP cableado:** 
APs conectados mediante cables al controlador.

## Parámetros de configuración en fakemesh

### 1. Mesh ID
   ID unificado para la red fakemesh. El controlador, los agentes y los APs cableados deben tener el mismo Mesh ID.

### 2. Clave (Key)
   Clave compartida de cifrado para la red. Si no requiere protección, puede dejarse en blanco.

### 3. Banda (Band)
   Frecuencia de red inalámbrica utilizada. Todos los dispositivos deben usar la misma banda (5G o 2.4G).

### 4. Rol (Role)
   Tipo de dispositivo: Controlador, Agente o AP cableado.

### 5. Configuración sincronizada (Sync Config)
   Permite la gestión centralizada (por el controlador) de las configuraciones Wi-Fi.

### 6. Dirección IP de acceso
   Dirección IP específica para acceder a la interfaz web del controlador.

### 7. Señal de retransmisión desactivada (Fronthaul Disabled)
   Evita que este nodo permita conexiones inalámbricas desde otros dispositivos.

### 8. Asistente de itinerancia (Band Steer Helper)
   Se puede utilizar [DAWN](https://github.com/fakemesh/dawn) o [usteer](https://github.com/fakemesh/usteer) como auxiliares de itinerancia.

## Gestión inalámbrica

El controlador permite gestionar de forma centralizada las configuraciones inalámbricas, como añadir o eliminar SSIDs, configurar métodos de cifrado y ajustar el ancho de banda.

## Implementación del controlador en modo puente

Si el controlador no se utiliza como puerta de enlace ni como servidor DHCP, será necesario configurarlo manualmente. Esto incluye asignar la IP de LAN, la IP de la puerta de enlace, y el DNS. Es importante que el controlador y la puerta de enlace estén en la misma subred y puedan comunicarse, de lo contrario, no será posible sincronizar las configuraciones con otros APs.
