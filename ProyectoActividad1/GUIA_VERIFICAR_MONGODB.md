# Guía: Verificar datos en MongoDB

Fecha: 2026-06-24

## Opciones para verificar que la información está en la base de datos MongoDB

---

## Opción 1: MongoDB Compass (GUI — Recomendado para principiantes)

MongoDB Compass es una herramienta visual que facilita explorar la base de datos sin escribir código.

### Instalación

1. Descarga desde: https://www.mongodb.com/products/tools/compass
2. Instala en tu Windows.
3. Abre la aplicación.

### Conexión a MongoDB local

1. En la pantalla de conexión, usa:
   ```
   mongodb://localhost:27017
   ```

2. Haz clic en **Connect**.

### Visualizar datos

1. Expande la base de datos `gestion_financiera` (en el panel izquierdo).
2. Expande la colección `transactions`.
3. Verás todos los documentos (transacciones) que creaste en la app.
4. Cada documento mostrará: `_id`, `tipo`, `categoria`, `monto`, `descripcion`, `fecha`, etc.

---

## Opción 2: CLI de MongoDB (mongosh — Para terminal)

Si tienes MongoDB instalado, puedes usar la consola de MongoDB para consultar directamente.

### Pasos

1. Abre PowerShell o CMD.
2. Ejecuta:

```powershell
mongosh
```

3. Conecta a la base de datos:

```javascript
use gestion_financiera
```

4. Consulta las transacciones:

```javascript
db.transactions.find().pretty()
```

### Comandos útiles

- **Ver todas las transacciones:**
  ```javascript
  db.transactions.find()
  ```

- **Contar cuántas transacciones hay:**
  ```javascript
  db.transactions.countDocuments()
  ```

- **Buscar transacciones de un tipo específico (ej. "ingreso"):**
  ```javascript
  db.transactions.find({ tipo: "ingreso" })
  ```

- **Eliminar una transacción por ID:**
  ```javascript
  db.transactions.deleteOne({ _id: ObjectId("xxxx...") })
  ```

- **Ver estructura de una transacción:**
  ```javascript
  db.transactions.findOne()
  ```

---

## Opción 3: API REST + Postman o Thunder Client

Usa tu propia API para consultar los datos y valida que se persistan.

### Con Postman (descargable desde postman.com) o Thunder Client (extensión de VS Code)

1. Asegúrate de que tu servidor corre:
   ```bash
   npm run dev
   ```

2. En Postman/Thunder Client, crea una **GET request** a:
   ```
   http://localhost:4000/api/transactions
   ```

3. Haz clic en **Send**.
4. Verás todas las transacciones en formato JSON.

### Con curl (terminal)

```powershell
curl http://localhost:4000/api/transactions
```

---

## Opción 4: Tests automatizados (Node.js + Jest)

Crea un test que verifique que los datos se persisten correctamente.

### Instalación de herramientas de test

```bash
npm install --save-dev jest supertest
```

### Ejemplo: test/transactions.test.js

```javascript
const mongoose = require('mongoose');
const request = require('supertest');
const app = require('../server');

// Configurar la conexión de prueba
beforeAll(async () => {
  await mongoose.connect(process.env.MONGO_URI || 'mongodb://localhost:27017/gestion_financiera_test');
});

afterAll(async () => {
  await mongoose.connection.close();
});

describe('Transacciones API', () => {
  
  test('Crear una transacción y verificar que se guarda', async () => {
    const nuevoGasto = {
      tipo: 'gasto',
      categoria: 'Comida',
      monto: 50,
      descripcion: 'Almuerzo',
      fecha: new Date()
    };

    const response = await request(app)
      .post('/api/transactions')
      .send(nuevoGasto);

    expect(response.status).toBe(201);
    expect(response.body.monto).toBe(50);
    expect(response.body.categoria).toBe('Comida');
  });

  test('Obtener todas las transacciones', async () => {
    const response = await request(app)
      .get('/api/transactions');

    expect(response.status).toBe(200);
    expect(Array.isArray(response.body)).toBe(true);
  });

  test('Actualizar una transacción', async () => {
    // Primero obtén una transacción existente
    const getResponse = await request(app)
      .get('/api/transactions');
    
    if (getResponse.body.length > 0) {
      const transactionId = getResponse.body[0]._id;
      
      const updateResponse = await request(app)
        .put(`/api/transactions/${transactionId}`)
        .send({ monto: 100 });

      expect(updateResponse.status).toBe(200);
      expect(updateResponse.body.monto).toBe(100);
    }
  });
});
```

### Configurar package.json

Añade a `scripts`:
```json
"test": "jest"
```

### Ejecutar tests

```bash
npm test
```

---

## Opción 5: Verificación manual en la app web

1. Inicia la aplicación:
   ```bash
   npm run dev
   ```

2. Abre `http://localhost:4000`.

3. Crea una transacción en el formulario.

4. Si aparece en la tabla, fue guardada en MongoDB.

5. Recarga la página: si la transacción sigue ahí, está persistida en la BD.

6. Abre MongoDB Compass o usa `mongosh` para confirmar.

---

## Resumen rápido

| Método | Complejidad | Cuándo usar |
|--------|-------------|-----------|
| **Compass** | Fácil | Para explorar visualmente |
| **mongosh** | Media | Para queries rápidas en terminal |
| **API REST** | Media | Para validar endpoints |
| **Tests** | Avanzado | Para automatización y CI/CD |
| **App web** | Fácil | Validación manual rápida |

---

## Próximos pasos

- Si quieres, genero un archivo `test/transactions.test.js` completo listo para ejecutar.
- También puedo crear un script de seed para generar datos de prueba automáticamente.
