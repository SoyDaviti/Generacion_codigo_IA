# Dependencias del Proyecto

Fecha: 2026-06-24

## Información del proyecto

- **Nombre:** gestion-financiera
- **Versión:** 1.0.0
- **Tipo:** Aplicación web full-stack (Node.js + MongoDB)
- **Runtime recomendado:** Node.js 18+ (LTS recomendado)
- **Gestor de paquetes:** npm 9+

---

## Dependencias de producción

Estas librerías son necesarias para que la aplicación funcione en producción.

| Paquete | Versión | Propósito |
|---------|---------|----------|
| **express** | ^4.18.2 | Framework web HTTP; manejo de rutas y middleware |
| **mongoose** | ^7.5.0 | ODM (Object Data Modeling) para MongoDB; abstracción de esquemas y operaciones |
| **cors** | ^2.8.5 | Middleware para habilitar CORS; permite requests desde diferentes orígenes |
| **dotenv** | ^16.3.1 | Carga variables de entorno desde archivo `.env` |

### Tabla de compatibilidades

```
Node.js 18.x → Compatible con todas las versiones listadas
Node.js 20.x → Compatible con todas las versiones listadas
Node.js 16.x → Verificar compatibilidad de mongoose ^7.5.0
```

---

## Dependencias de desarrollo

Estas librerías son solo para desarrollo y pruebas; no se incluyen en producción.

| Paquete | Versión | Propósito |
|---------|---------|----------|
| **nodemon** | ^3.0.1 | Monitor de cambios; reinicia servidor automáticamente durante desarrollo |

### Recomendadas (opcionales)

Para mejorar la calidad del código y pruebas automatizadas:

| Paquete | Versión | Propósito |
|---------|---------|----------|
| **jest** | ^29.7.0 | Framework de testing (tests unitarios y de integración) |
| **supertest** | ^6.3.3 | HTTP assertion library; facilita tests de rutas API |
| **express-validator** | ^7.0.0 | Validación y sanitización de entradas en Express |

---

## Cómo instalar

### Instalación inicial (todas las dependencias)

```bash
npm install
```

Esto instala todas las dependencias listadas en `package.json` en la carpeta `node_modules/`.

### Instalar solo dependencias de producción

```bash
npm install --production
```

Útil para reducir tamaño en servidores.

### Agregar una nueva dependencia

```bash
npm install nombre-del-paquete
```

O para desarrollo:

```bash
npm install --save-dev nombre-del-paquete
```

---

## Scripts disponibles

| Script | Comando | Descripción |
|--------|---------|-------------|
| **start** | `npm start` | Inicia el servidor en modo producción |
| **dev** | `npm run dev` | Inicia con nodemon (mode desarrollo con auto-reload) |
| **test** | `npm test` | Ejecuta tests (si jest está configurado) |

---

## Archivo package.json (referencia)

```json
{
  "name": "gestion-financiera",
  "version": "1.0.0",
  "description": "Plataforma web de gestión financiera personal con backend en Node.js y MongoDB.",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.3.1",
    "express": "^4.18.2",
    "mongoose": "^7.5.0"
  },
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}
```

---

## Notas sobre versiones

- Las versiones usando `^` (caret) permiten actualizaciones menores y patches automáticos.
  - `^4.18.2` → permite `4.18.x` y `4.19.x`, pero NO `5.x.x`.
- Para fijar versiones exactas, cambiar `^` por nada o usar `~`.

---

## Verificación de dependencias instaladas

Para listar todos los paquetes instalados:

```bash
npm list
```

Para ver solo las dependencias de nivel superior:

```bash
npm list --depth=0
```

Para verificar vulnerabilidades de seguridad:

```bash
npm audit
```

Para actualizar paquetes automáticamente:

```bash
npm update
```

---

## Requisitos del sistema

- **Node.js:** 18.x, 19.x o 20.x (LTS recomendado)
- **npm:** 9.x o superior (incluido con Node.js)
- **MongoDB:** 4.4+ (local o Atlas)
- **Espacio en disco:** ~500 MB (node_modules)
- **RAM:** 512 MB mínimo para desarrollo local

---

## Resumen de instalación

1. Clonar o navegar al proyecto
2. Ejecutar: `npm install`
3. Crear `.env` con `PORT` y `MONGO_URI`
4. Ejecutar: `npm run dev`
5. Acceder a: `http://localhost:4000`

---

## Alternativa: requirements.txt

Si necesitas exportar en formato tipo Python, aquí está la equivalencia:

```
express@4.18.2
mongoose@7.5.0
cors@2.8.5
dotenv@16.3.1
nodemon@3.0.1 (dev)
```

Para instalar desde un archivo equivalente en Node.js, usa `npm install` con `package.json`.
