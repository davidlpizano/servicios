# 🖥️ Infraestructura y Servicios Homelab - dlplab.es

Este repositorio contiene la configuración centralizada mediante Docker Compose, la gestión de volúmenes estáticos y la documentación de todos los servicios autoalojados en el servidor principal.

## ⚙️ Especificaciones de Hardware

La infraestructura física que soporta estos servicios está compuesta por:

| Componente | Especificación |
| :--- | :--- |
| **Servidor / NAS** | Ugreen DXP2800 |
| **Almacenamiento (Datos)** | 4 TB HDD |
| **Almacenamiento (Docker)** | 512 GB M.2 NVMe SSD |
| **Memoria (RAM)** | 8 GB DDR5 |
| **Alimentación (SAI/UPS)** | CyberPower UPS |
| **Red Local** | Switch Gigabit de 5 puertos |

## 💻 Stack de Software Base

El servidor y los servicios se gestionan utilizando el siguiente software principal:

* **Sistema Operativo:** UGOS (basado en Debian Linux) para el NAS principal y entornos Debian virtualizados.
* **Contenedores:** Docker Engine y Docker Compose para el aislamiento y despliegue de todos los servicios.
* **Redes y Enrutamiento:** `nftables` y Keepalived para configuraciones avanzadas y alta disponibilidad (HA).
* **Control de Versiones:** Git para la gestión y respaldo de este repositorio.

## 📂 Estructura de Directorios y Servicios

El repositorio utiliza un modelo unificado. Cada directorio corresponde a una pila de servicios y contiene su propio `docker-compose.yml` junto con sus configuraciones persistentes.

* `📁 proxy/` - **Nginx Proxy Manager**: Gestión de proxy inverso y automatización de certificados SSL.
* `📁 dns/` - **Pi-hole**: Gestión de DNS a nivel de red para bloqueo de telemetría y anuncios.
* `📁 remoto/` - **RustDesk**: Servidor de retransmisión (`hbbs` y `hbbr`) para conexiones de escritorio remoto.
* `📁 media/` - **Automatización y Streaming**: Jellyfin, qBittorrent y la suite *arr (Radarr, Sonarr, Prowlarr, Jellyseerr).
* `📁 nube/` - **Productividad**: Nextcloud (almacenamiento) y Vaultwarden (gestor de contraseñas).
* `📁 dhcp/` - **KEA**: Gestión de red DHCP con alta disponibilidad (HA).

## 🚀 Uso y Despliegue

Para desplegar o actualizar una pila de servicios, navega a su directorio correspondiente. Es imperativo crear y configurar el archivo `.env` local antes de levantar los contenedores.

```bash
# 1. Acceder al directorio del servicio
cd media/

# 2. Levantar los contenedores en segundo plano
docker compose up -d

# 3. Revisar los registros en caso de error
docker compose logs -f
