fakemesh Overview

fakemesh is a network topology composed of one "controller (AC)" and one or more "Wired APs" and "Satellites (Agents)". It is a hybrid network that mixes the "wireless Mesh" and "AC+AP" networking modes: Wired APs connect to the controller (AC) by Ethernet cable, while Satellites (Agents) join via wireless STA (station) mode, together forming a wireless (and wired) coverage network.

Deployment of fakemesh is relatively convenient: just connect node devices to the correct network and set each node's role, Mesh ID, and other info. Because fakemesh combines wireless Mesh and AC+AP modes, it also easily supports hybrid deployments, increasing coverage and reliability.

fakemesh is integrated by default in X-WRT: https://github.com/x-wrt/x-wrt

Using fakemesh

Unified access address formats after successful networking:

Controller address: http://controller.fakemesh/ or http://ac.fakemesh/
AP address: http://{mac}.ap.fakemesh/ or http://N.ap.fakemesh/
Here, {mac} is the AP's MAC address, for example {mac}=1122334455AB, and N is the AP's auto-assigned number, e.g. N=1, N=2, N=3, ...

Examples: http://1.ap.fakemesh/ http://1122334455AB.ap.fakemesh/

Troubleshooting:

If an AP goes offline for about 3 minutes it enters fault mode. In this mode a default SSID is enabled so you can connect and access the management interface to reconfigure it. The default SSID and password for fault mode are: SSID: X-WRT_XXXX PASSWD: 88888888

In fault mode the AP's management IP is the DHCP gateway address. For example, if your computer receives an IP like 192.168.16.x, then the AP's management IP will be 192.168.16.1.

Basic components of fakemesh

The network is composed of a single controller and one or more APs.

AP types:

Satellite (Agent)
Wired AP
Controller: acts as the AC and the upstream router/gateway, provides internet access, centrally manages connected Satellites and Wired APs, and centrally manages wireless settings.

Satellite (Agent): an AP that joins the network via Wi‑Fi.

Wired AP: an AP that joins the network over Ethernet cable.

fakemesh configuration parameters

Mesh ID This is the common ID for the fakemesh network. The controller, satellites, and wired APs must all use the same Mesh ID.

Key The shared key for the network. Use this for encryption; leave blank if no encryption is required.

Band The wireless band used for the network; set the same band on all nodes (5G or 2G).

Role Can be controller, satellite, or wired AP.

Sync Config Whether to centrally manage Wi‑Fi configuration and similar settings. Wi‑Fi configuration is centrally managed by the controller.

Access IP address Set a specific IP address for the controller so you can access its management interface by that IP.

Fronthaul Disabled When enabled on a node, this disables fronthaul wireless; other APs are not allowed to use this node's Wi‑Fi to connect.

Band Steer Helper Currently you can choose DAWN (https://github.com/fakemesh/dawn) or usteer (https://github.com/fakemesh/usteer) as the roaming helper component.

Wireless Management

Wi‑Fi can be managed centrally from the controller, including adding/removing SSIDs, setting SSID encryption, and bandwidth settings.

Controller bypass deployment

Note: If the controller is not acting as the gateway and does not provide DHCP, the user must configure network settings manually, including the controller LAN IP, gateway IP, and DNS. Typically the controller's LAN interface defaults to using a DHCP client to get an IP and gateway from a third‑party gateway. If you need to use a static IP, ensure the controller and the third‑party gateway are on the same subnet and can communicate with each other. Otherwise controller synchronization with other APs will not work.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

fakemesh es una topología de red compuesta por un "controlador (AC)" y uno o varios "AP cableados" y "satélites (Agent)". Es una red híbrida que mezcla los modos de red "Mesh inalámbrico" y "AC+AP": los AP cableados se conectan al controlador (AC) por cable Ethernet, mientras que los satélites (Agents) se unen mediante modo STA inalámbrico; en conjunto forman una red de cobertura inalámbrica (y cableada).

El despliegue de fakemesh es relativamente sencillo: solo hay que conectar los dispositivos nodo a la red correcta y configurar el rol del nodo, el Mesh ID y otros datos. Debido a que fakemesh combina Mesh inalámbrico y AC+AP, también admite despliegues mixtos con facilidad, lo que mejora la cobertura y la fiabilidad.

Actualmente fakemesh está integrado por defecto en X-WRT: https://github.com/x-wrt/x-wrt

Uso de fakemesh

Formatos unificados de direcciones de acceso tras una configuración de red exitosa:

Dirección del controlador: http://controller.fakemesh/ o http://ac.fakemesh/
Dirección del AP: http://{mac}.ap.fakemesh/ o http://N.ap.fakemesh/
Aquí, {mac} es la dirección MAC del AP, por ejemplo {mac}=1122334455AB, y N es el número automático del AP, p. ej. N=1, N=2, N=3, ...

Ejemplos: http://1.ap.fakemesh/ http://1122334455AB.ap.fakemesh/

Resolución de problemas:

Si un AP está desconectado durante unos 3 minutos entra en modo de fallo. En este modo se activa un SSID por defecto para que puedas conectarte y acceder a la interfaz de gestión para reconfigurarlo. El SSID y la contraseña por defecto en modo de fallo son: SSID: X-WRT_XXXX PASSWD: 88888888

En modo de fallo la IP de gestión del AP es la dirección gateway del servidor DHCP. Por ejemplo, si tu equipo recibe una IP 192.168.16.x, la IP de gestión del AP será 192.168.16.1.

Componentes básicos de fakemesh

La red está formada por un único controlador y uno o varios APs.

Tipos de AP:

Satélite (Agent)
AP cableado
Controlador: actúa como AC y como router/gateway de salida, proporciona acceso a Internet, gestiona centralmente los satélites y los AP cableados conectados, y gestiona la configuración inalámbrica de forma centralizada.

Satélite (Agent): un AP que se conecta a la red mediante Wi‑Fi.

AP cableado: un AP que se conecta a la red por cable Ethernet.

Parámetros de configuración de fakemesh

Mesh ID Este parámetro es el ID común de la red fakemesh. El controlador, los satélites y los AP cableados deben usar el mismo Mesh ID.

Clave (Key) La clave compartida de la red. Se usa para cifrado de la red; si no se requiere cifrado, se puede dejar en blanco.

Banda (Band) La banda inalámbrica usada por la red; todos los nodos deben configurarla igual (5G o 2G).

Rol (Role) Puede ser controlador, satélite o AP cableado.

Sincronizar configuración (Sync Config) Si se desea gestionar la configuración de Wi‑Fi y demás de forma centralizada. La configuración Wi‑Fi la gestiona el controlador.

Dirección IP de acceso (Access IP address) Establece una IP específica para el controlador, con la que se puede acceder a su interfaz de gestión.

Desactivar fronthaul (Fronthaul Disabled) En este nodo se desactiva la señal inalámbrica de fronthaul, es decir, no se permite que otros APs se conecten a través del Wi‑Fi de este nodo.

Componente de roaming (Band Steer Helper) Actualmente se puede elegir DAWN (https://github.com/fakemesh/dawn) o usteer (https://github.com/fakemesh/usteer) como asistente de roaming.

Gestión inalámbrica

Se puede gestionar el Wi‑Fi desde la interfaz del controlador de forma centralizada, incluyendo añadir o eliminar SSIDs, configurar el cifrado de los SSIDs y el ancho de banda.

Despliegue del controlador en bypass

Atención: si el controlador no actúa como gateway y no proporciona servicio DHCP, el usuario debe configurar manualmente los ajustes de red, incluyendo la IP de la LAN del controlador, la IP del gateway y los DNS. Normalmente la interfaz LAN del controlador viene por defecto con un cliente DHCP para obtener IP y gateway de un gateway de terceros. Si se necesita usar una IP estática, hay que asegurarse de que el controlador y el gateway de terceros estén en la misma subred y puedan comunicarse entre sí. Si no, no será posible que el controlador sincronice la configuración con los demás APs.
