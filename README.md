# Hostify

![PHP](https://img.shields.io/badge/PHP-8.2%2B-777BB4?style=flat-square&logo=php&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![Filament](https://img.shields.io/badge/Filament-4-FFAA00?style=flat-square)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=php,laravel,postgres,tailwind,vite,js,git&theme=light" alt="Tecnologías utilizadas en Hostify" />
  </a>
</p>

**Hostify** es una aplicación web para la gestión operativa de hoteles. El sistema centraliza procesos clave como administración de habitaciones, reservas, huéspedes, check-in, check-out, facturación, pagos, cierres de turno y limpieza desde un panel administrativo construido con **Laravel** y **Filament**.

El proyecto está orientado a hoteles que necesitan reemplazar procesos manuales o dispersos por una plataforma web organizada, trazable y accesible desde navegador.

## Demo

Hostify cuenta con una versión desplegada para probar el panel administrativo:

[Acceder a la demo](https://hostify-main-jpyutf.free.laravel.cloud/admin/login)

Credenciales de prueba:

| Rol | Correo | Contraseña |
|---|---|---|
| Super Admin | `admin@hostify.com` | `hostify2026` |
| Recepcionista | `ana@hostify.com` | `hostify2026` |
| Camarera | `maria@hostify.com` | `hostify2026` |
| Supervisor | `carlos@hostify.com` | `hostify2026` |

## Tabla de contenido

- [Tecnologías utilizadas](#tecnologías-utilizadas)
- [Descripción general](#descripción-general)
- [Funcionalidades principales](#funcionalidades-principales)
- [Roles del sistema](#roles-del-sistema)
- [Modelo de dominio](#modelo-de-dominio)
- [Requisitos previos](#requisitos-previos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Base de datos](#base-de-datos)
- [Ejecución en local](#ejecución-en-local)
- [Credenciales de prueba](#credenciales-de-prueba)
- [Comandos útiles](#comandos-útiles)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Autor](#autor)
- [Licencia](#licencia)

## Tecnologías utilizadas

- **PHP 8.2+**
- **Laravel 12**
- **Filament 4**
- **Filament Shield**
- **Spatie Laravel Permission**
- **PostgreSQL**
- **Blade**
- **Livewire**
- **Vite**
- **Tailwind CSS**
- **Axios**

## Descripción general

Hostify fue desarrollado como una solución administrativa para apoyar la operación diaria de un hotel. Su objetivo es mejorar la visibilidad del estado de las habitaciones, organizar la gestión de reservas, facilitar el control del huésped durante su estadía y mantener trazabilidad sobre procesos operativos como limpieza, pagos y cierre de caja.

La aplicación utiliza un panel administrativo basado en Filament, con recursos separados por módulo y control de acceso mediante roles y permisos. Esto permite que cada tipo de usuario acceda únicamente a las funciones necesarias para su operación.

## Funcionalidades principales

### Panel administrativo

- Acceso al sistema desde `/admin`.
- Login para usuarios autorizados.
- Panel administrativo construido con Filament.
- Navegación organizada por módulos operativos.
- Tema visual personalizado para el panel.
- Redirección desde la ruta principal hacia el panel administrativo.

### Habitaciones

- Registro y administración de habitaciones.
- Asociación de habitaciones con tipos de habitación.
- Control de número, piso, estado, notas y disponibilidad.
- Estados operativos de habitación:
  - Libre.
  - Sucia.
  - Ocupada.
  - No disponible.
- Cambio de estado de habitaciones desde el sistema.
- Historial de cambios de estado con usuario, estado anterior, nuevo estado, origen del cambio y fecha.

### Panel operativo de habitaciones

- Vista visual para consultar habitaciones por estado.
- Agrupación de habitaciones por piso.
- Resumen operativo por estado de habitación.
- Filtro por fecha.
- Actualización periódica del panel.
- Acceso diferenciado según rol.
- Vista adaptada para camareras con habitaciones asignadas.

### Tipos de habitación

- Administración de tipos de habitación.
- Relación entre tipos de habitación y habitaciones.
- Datos iniciales cargables mediante seeders.

### Huéspedes

- Registro y administración de huéspedes.
- Relación de huéspedes con reservas, facturas e incidencias.
- Consulta de información centralizada para la operación de recepción.

### Reservas

- Creación y administración de reservas.
- Asociación de reservas con huésped, habitación y usuario creador.
- Manejo de fechas de entrada y salida.
- Registro de tarifa por reserva.
- Estados de reserva:
  - Pendiente.
  - Aprobada.
  - Rechazada.
  - Activa.
  - Checked out.
  - Cancelada.
- Acciones de negocio para aprobar, rechazar, cancelar, hacer check-in y hacer check-out.
- Cálculo de noches, total de habitación, cargos adicionales y total facturable.

### Check-in y check-out

- Check-in sobre reservas aprobadas.
- Cambio automático de la habitación a estado ocupada al registrar entrada.
- Check-out sobre reservas activas.
- Cambio automático de la habitación a estado sucia al registrar salida.
- Generación de factura durante el checkout.
- Registro del pago asociado al checkout.
- Validaciones para evitar operaciones inválidas, como registrar salida sin turno abierto o generar facturas duplicadas.

### Facturación y pagos

- Generación de factura asociada a una reserva.
- Número de factura generado por el sistema.
- Registro de subtotal, impuestos, total, estado y fecha de emisión.
- Registro de pagos con monto, método de pago, usuario responsable, fecha y observaciones.
- Métodos de pago disponibles:
  - Efectivo.
  - Datáfono.
  - Transferencia.
- Estados de factura:
  - Borrador.
  - Emitida.
  - Pagada.
  - Anulada.

### Cierres de turno

- Administración de cierres de turno.
- Asociación de pagos a cierres de turno.
- Control de estado del cierre:
  - Abierto.
  - Cerrado.
  - Validado.
- Base para conciliación de caja por usuario y turno.

### Limpieza

- Administración de sesiones de limpieza.
- Asignación de habitaciones a camareras.
- Registro del usuario que asigna la limpieza.
- Control de fecha asignada, hora de inicio, hora de finalización y duración.
- Estados de limpieza:
  - Pendiente.
  - En proceso.
  - Terminada.
- Inicio y finalización de limpieza desde el panel operativo.
- Registro de notas y fotografía como evidencia posterior a la limpieza.
- Cambio automático de habitación a estado libre al finalizar la limpieza.

## Roles del sistema

Hostify utiliza roles y permisos para controlar el acceso a módulos, vistas y acciones.

Roles incluidos:

- **Super Admin**: acceso completo al sistema.
- **Supervisor**: gestión operativa general.
- **Recepcionista**: operación de huéspedes, reservas, habitaciones, facturación y caja.
- **Camarera**: acceso operativo al panel de habitaciones y sesiones de limpieza asignadas.

## Modelo de dominio

El proyecto está organizado alrededor de entidades principales del negocio hotelero:

| Entidad | Propósito |
|---|---|
| `User` | Usuarios del sistema y asignación de roles. |
| `RoomType` | Tipos de habitación disponibles en el hotel. |
| `Room` | Habitaciones físicas y estado operativo. |
| `RoomStatusLog` | Historial de cambios de estado de habitaciones. |
| `Guest` | Información de huéspedes. |
| `Reservation` | Reservas asociadas a huéspedes, habitaciones, fechas y estado. |
| `Invoice` | Facturas generadas desde reservas. |
| `Charge` | Cargos adicionales asociados a reservas. |
| `Payment` | Pagos registrados en la operación. |
| `ShiftClose` | Cierres de turno y control de caja. |
| `CleaningSession` | Asignaciones y trazabilidad de limpieza por habitación. |

## Requisitos previos

Antes de instalar el proyecto, asegúrate de tener instalado:

- PHP 8.2 o superior.
- Composer.
- Node.js.
- npm.
- PostgreSQL.
- Git.

Extensiones PHP necesarias para un entorno Laravel con PostgreSQL:

```ini
extension=curl
extension=mbstring
extension=openssl
extension=intl
extension=fileinfo
extension=zip
extension=pdo_pgsql
extension=pgsql
```

## Instalación

Clona el repositorio:

```bash
git clone https://github.com/CristoferGuillen/Hostify.git
```

Entra a la carpeta del proyecto:

```bash
cd Hostify
```

Instala las dependencias de PHP:

```bash
composer install
```

Instala las dependencias de JavaScript:

```bash
npm install
```

Copia el archivo de entorno:

```bash
cp .env.example .env
```

En Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Genera la clave de la aplicación:

```bash
php artisan key:generate
```

## Configuración

Edita el archivo `.env` y configura los datos principales de la aplicación:

```env
APP_NAME=Hostify
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8000
```

Configura la conexión a PostgreSQL:

```env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=hostify
DB_USERNAME=postgres
DB_PASSWORD=tu_password
```

Crea una base de datos llamada `hostify` antes de ejecutar las migraciones.

## Base de datos

Ejecuta las migraciones:

```bash
php artisan migrate
```

Carga los datos iniciales:

```bash
php artisan db:seed
```

También puedes reiniciar la base de datos y cargar los seeders en un solo comando:

```bash
php artisan migrate:fresh --seed
```

## Ejecución en local

Ejecuta el entorno de desarrollo con:

```bash
composer run dev
```

También puedes ejecutar Laravel y Vite por separado.

Terminal 1:

```bash
php artisan serve
```

Terminal 2:

```bash
npm run dev
```

Luego abre el panel administrativo en:

```text
http://localhost:8000/admin
```

## Credenciales de prueba

Al ejecutar los seeders se crean usuarios iniciales para probar los roles principales del sistema.

| Rol | Correo | Contraseña |
|---|---|---|
| Super Admin | `admin@hostify.com` | `hostify2026` |
| Recepcionista | `ana@hostify.com` | `hostify2026` |
| Camarera | `maria@hostify.com` | `hostify2026` |
| Supervisor | `carlos@hostify.com` | `hostify2026` |

## Comandos útiles

Ejecutar migraciones:

```bash
php artisan migrate
```

Ejecutar seeders:

```bash
php artisan db:seed
```

Recrear la base de datos con datos iniciales:

```bash
php artisan migrate:fresh --seed
```

Levantar servidor local:

```bash
php artisan serve
```

Ejecutar Vite:

```bash
npm run dev
```

Compilar assets:

```bash
npm run build
```

Ejecutar el entorno completo de desarrollo:

```bash
composer run dev
```

## Estructura del proyecto

```text
Hostify/
├── app/
│   ├── Enums/
│   ├── Filament/
│   │   ├── Pages/
│   │   └── Resources/
│   ├── Models/
│   └── Providers/
│
├── database/
│   ├── migrations/
│   └── seeders/
│
├── lang/
├── public/
├── resources/
│   ├── css/
│   ├── js/
│   └── views/
│
├── routes/
├── storage/
├── tests/
├── composer.json
├── package.json
└── vite.config.js
```

## Autor

Desarrollado por **Cristofer Guillen**.

- GitHub: [@CristoferGuillen](https://github.com/CristoferGuillen)
- Repositorio: [Hostify](https://github.com/CristoferGuillen/Hostify)

## Licencia

Este proyecto está disponible bajo la licencia **MIT**.

