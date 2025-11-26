# TFG ASIR - Servidor Doméstico Automatizado

Este proyecto contiene una colección de scripts y configuraciones de Docker Compose para desplegar y gestionar un servidor doméstico completo de forma automatizada. Fue desarrollado como parte de un Trabajo de Fin de Grado (TFG) para el ciclo de Administración de Sistemas Informáticos en Red (ASIR).

## 🚀 Características

- **Despliegue Automatizado**: Script `setup.sh` para instalar dependencias, configurar RAID y levantar contenedores.
- **Gestión de Almacenamiento**: Configuración automática de RAID 0 y servidor Samba.
- **Servicios Dockerizados**: Todos los servicios corren en contenedores para facilitar la gestión y el aislamiento.
- **Seguridad**:
    - **Authelia**: Autenticación de dos factores y SSO.
    - **WireGuard**: VPN para acceso remoto seguro.
    - **Pi-hole**: Bloqueo de publicidad y DNS local.
    - **Nginx Proxy Manager**: Gestión de certificados SSL y proxy inverso.
- **Monitorización**: Stack completo con Grafana, Prometheus, cAdvisor y Node Exporter.
- **Dashboard**: Homarr para tener todos tus servicios a mano.

##  Tecnologías Usadas

- **Docker & Docker Compose**: Para la orquestación de contenedores.
- **Bash**: Para los scripts de automatización (`setup.sh`, `menuSamba.sh`).
- **Linux (Debian/Ubuntu)**: Sistema operativo base recomendado.
- **Samba**: Protocolo para compartir archivos en red local.
- **MDADM**: Gestión de RAID por software.

## 📋 Servicios Incluidos

| Servicio | Descripción |
|----------|-------------|
| **Authelia** | Servidor de autenticación y autorización. |
| **Cloudflare DDNS** | Actualiza automáticamente tu IP pública en Cloudflare. |
| **Filebrowser** | Gestor de archivos web. |
| **Homarr** | Dashboard personalizable para tus servicios. |
| **Grafana** | Visualización de métricas y monitorización. |
| **Prometheus** | Recolección de métricas. |
| **Nginx Proxy Manager** | Proxy inverso con gestión de SSL (Let's Encrypt). |
| **WireGuard** | VPN rápida y moderna (usando wg-easy). |
| **Pi-hole** | Servidor DNS y bloqueo de publicidad (integrado con WireGuard). |
| **Portainer** | Interfaz web para gestionar Docker. |
| **Duplicati** | Sistema de copias de seguridad. |

## 🛠️ Requisitos Previos

- Un servidor o PC corriendo Linux (probado en Debian/Ubuntu).
- (Opcional) Dos discos duros adicionales si deseas configurar RAID 0.
- Conexión a internet.
- Un dominio propio (recomendado para usar con Cloudflare y Nginx Proxy Manager).

## ⚙️ Instalación

1.  **Clonar el repositorio**:
    ```bash
    git clone <url-del-repositorio>
    cd tfg-asir
    ```

2.  **Configurar variables de entorno**:
    Copia el archivo de ejemplo y rellena tus datos.
    ```bash
    cp .env.example .env
    nano .env
    ```
    Asegúrate de rellenar campos críticos como:
    - `CLOUDFLARE_API_KEY` y `ZONE`
    - `WG_HOST` y `PASSWORD`
    - `GRAFANA_ADMIN_PASSWORD`

3.  **Ejecutar el script de instalación**:
    ```bash
    chmod +x setup.sh
    ./setup.sh
    ```
    El script te guiará a través de:
    - Creación de RAID (si tienes los discos).
    - Instalación de dependencias (Docker, Samba, etc.).
    - Despliegue de los contenedores.

## 📂 Estructura del Proyecto

```
.
├── docker/                 # Configuraciones de Docker Compose por servicio
│   ├── authelia/
│   ├── cloudflare/
│   ├── filebrowser/
│   ├── homarr/
│   ├── monitorizacion/     # Grafana, Prometheus, etc.
│   ├── nginx/
│   └── wg-pihole/
├── menuSamba.sh            # Script interactivo para gestionar recursos compartidos Samba
├── setup.sh                # Script principal de instalación
├── .env.example            # Plantilla de variables de entorno
└── README.md               # Documentación del proyecto
```

## 🔧 Gestión Post-Instalación

### Gestión de Samba
Para añadir o eliminar carpetas compartidas y usuarios de Samba, utiliza el script interactivo:
```bash
sudo ./menuSamba.sh
```

### Acceso a Servicios
Una vez desplegado, podrás acceder a los servicios a través de los puertos configurados (o dominios si configuraste Nginx Proxy Manager):

- **Portainer**: `http://<IP-Servidor>:9443`
- **Nginx Proxy Manager**: `http://<IP-Servidor>:81`
- **Homarr**: `http://<IP-Servidor>:7575`
- **Grafana**: `http://<IP-Servidor>:3000`
- **WireGuard UI**: `http://<IP-Servidor>:51821`
- **Pi-hole**: `http://<IP-Servidor>:8050/admin`

## 🤝 Contribución
Si deseas mejorar este proyecto, siéntete libre de hacer un fork y enviar un Pull Request.

## ✒️ Autores

- **Esteban** - *Desarrollo y Documentación*

## 📝 Licencia

Este proyecto está bajo la Licencia MIT. Eres libre de usarlo, modificarlo y distribuirlo.
