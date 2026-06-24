# Plataforma Web de Gestión Financiera

Aplicación de gestión de finanzas personales que permite crear, leer, actualizar y eliminar transacciones, calcular saldo dinámico y almacenar datos en MongoDB.

## Requisitos del sistema

- Node.js instalado (recomendado 18+)
- npm disponible
- MongoDB instalado y en ejecución localmente, o una instancia de MongoDB Atlas
- Archivo `.env` configurado en la raíz del proyecto

## Estructura del proyecto

- `server.js`: servidor Express principal
- `config/db.js`: conexión a MongoDB
- `models/Transaction.js`: modelo Mongoose de transacciones
- `routes/transactions.js`: rutas REST API
- `public/`: frontend del prototipo

## Instalación y despliegue local

1. Abrir una terminal en la carpeta del proyecto:

```bash
cd c:\GeneracionIA\Actividad1\ProyectoActividad1
```

2. Instalar dependencias:

```bash
npm install
```

3. Crear o verificar el archivo `.env` en la raíz del proyecto con estas variables:

```env
PORT=4000
MONGO_URI=mongodb://localhost:27017/gestion_financiera
```

- `PORT` define el puerto local donde se ejecuta la aplicación.
- `MONGO_URI` define la conexión a la base de datos MongoDB.

4. Si no tienes MongoDB instalado localmente, debes instalarlo o usar MongoDB Atlas.

### Opción A: MongoDB local en Windows

- Instala MongoDB Community desde https://www.mongodb.com/try/download/community
- Inicia el servicio `MongoDB` en Windows Services, o con PowerShell:

```powershell
net start MongoDB
```

### Opción B: MongoDB Atlas en la nube

- Crea una cuenta y un clúster gratuito en https://cloud.mongodb.com
- Crea una base de datos y un usuario
- Copia la URI de conexión y reemplaza `MONGO_URI` en `.env` con la nueva cadena de conexión.

5. Iniciar el servidor:

```bash
npm run dev
```

O si prefieres ejecutar sin nodemon:

```bash
npm start
```

6. Abrir la aplicación en el navegador:

```text
http://localhost:4000
```

## Validación del funcionamiento

- En la consola debe aparecer un mensaje como `MongoDB conectado: ...`.
- También debe verse `Servidor corriendo en http://localhost:4000`.
- La interfaz debe cargar correctamente en el navegador.
- Debes poder crear, editar y eliminar transacciones.

## Detalles técnicos

- `dotenv` carga variables de entorno desde el archivo `.env`.
- `express` sirve el frontend y expone la API REST.
- `mongoose` se encarga de la conexión con MongoDB.
- `cors` permite solicitudes desde el navegador.

## Notas

- Todo el despliegue descrito se realiza en tu equipo local, dentro de la carpeta del proyecto.
- Si usas MongoDB Atlas, no necesitas instalar MongoDB localmente, pero la aplicación de Node.js seguirá ejecutándose localmente.
