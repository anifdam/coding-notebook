<div align="center">

**Model - View - Controller**

Un patrón de diseño para organizar tu código como un profesional

---

</div>

## 🎯 ¿Qué es MVC?

> **MVC** es un **patrón de diseño** que te ayuda a organizar el código de tu aplicación de forma ordenada y profesional. Es como tener tres equipos especializados trabajando juntos para crear algo increíble.

---

## 🏗️ Las 3 Partes del MVC

### 1️⃣ **MODEL** (Modelo) 📊

**¿Qué hace?** → Maneja los **DATOS** y la lógica de negocio

#### Responsabilidades:
- ✅ Conectarse a la base de datos
- ✅ Guardar, actualizar o eliminar información
- ✅ Validar datos
- ✅ Aplicar reglas de negocio

#### Ejemplo de código:
```javascript
class UserModel {
  obtenerUsuario(id) {
    // Consulta a la base de datos
    return database.query('SELECT * FROM users WHERE id = ?', [id]);
  }
  
  guardarUsuario(datos) {
    // Guardar nuevo usuario
    return database.insert('users', datos);
  }
}
```

---

### 2️⃣ **VIEW** (Vista) 🎨

**¿Qué hace?** → Muestra la información al **USUARIO**

#### Responsabilidades:
- ✅ Páginas HTML
- ✅ Formularios y tablas
- ✅ Interfaces de usuario
- ✅ Todo lo visual que el usuario VE

#### Ejemplo de código:
```html
<!-- Vista de perfil de usuario -->
<div class="perfil">
  <h1>Bienvenido, {{nombre}}</h1>
  <p>Email: {{email}}</p>
  <p>Miembro desde: {{fecha}}</p>
</div>
```

---

### 3️⃣ **CONTROLLER** (Controlador) 🎮

**¿Qué hace?** → Es el **INTERMEDIARIO** entre Model y View

#### Responsabilidades:
- ✅ Recibe las peticiones del usuario
- ✅ Pide datos al Model
- ✅ Procesa la lógica de control
- ✅ Envía los datos a la View

#### Ejemplo de código:
```javascript
class UserController {
  mostrarPerfil(req, res) {
    const userId = req.params.id;
    
    // Pide datos al Model
    const usuario = UserModel.obtenerUsuario(userId);
    
    // Envía a la View
    res.render('perfil', { usuario });
  }
}
```

---

## 🔄 ¿Cómo Funciona el Flujo?

```
┌─────────┐
│ USUARIO │ ──────┐
└─────────┘       │
                  ▼
           ┌─────────────┐
           │ CONTROLLER  │
           │     🎮      │
           └─────────────┘
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
┌─────────────┐     ┌─────────────┐
│   MODEL     │     │    VIEW     │
│     📊      │     │     🎨      │
└─────────────┘     └─────────────┘
        │                   │
        └─────────┬─────────┘
                  ▼
           ┌─────────────┐
           │  RESULTADO  │
           │  AL USUARIO │
           └─────────────┘
```

**Paso a paso:**

1. 👤 **Usuario** hace una acción (ej: click en "Ver Producto #5")
2. 🎮 **Controller** recibe la petición
3. 📊 **Model** busca el producto en la base de datos
4. 🎮 **Controller** recibe los datos del Model
5. 🎨 **View** recibe los datos y los presenta bonitos
6. ✅ **Usuario** ve el resultado final en pantalla

---

## 💡 Ejemplo Completo: Tienda Online

Imagina que estás construyendo una tienda online y un usuario quiere ver un producto:

### Escenario:
**Usuario hace click en "Ver Producto #5"**

### El flujo MVC:

```javascript
// 1. CONTROLLER recibe la petición
class ProductController {
  verProducto(req, res) {
    const id = req.params.id; // id = 5
    
    // 2. Pide datos al MODEL
    const producto = ProductModel.obtenerProducto(id);
    
    // 3. Envía datos a la VIEW
    res.render('producto', { producto });
  }
}

// MODEL obtiene los datos
class ProductModel {
  obtenerProducto(id) {
    return db.query('SELECT * FROM productos WHERE id = ?', [id]);
    // Retorna: { nombre: "Laptop HP", precio: 899, stock: 15 }
  }
}

// VIEW muestra los datos
// HTML renderizado:
<div class="producto">
  <h1>Laptop HP</h1>
  <p class="precio">$899</p>
  <p class="stock">Stock disponible: 15</p>
  <button>Agregar al carrito</button>
</div>
```

**Resultado:** El usuario ve toda la información del producto de forma clara y puede comprarlo.

---

## ✅ Ventajas de Usar MVC

| Ventaja | Descripción | Beneficio |
|---------|-------------|-----------|
| 🧹 **Organización** | Código limpio y separado por responsabilidades | Fácil de entender y navegar |
| 👥 **Trabajo en equipo** | Varios desarrolladores trabajando simultáneamente | Mayor productividad |
| 🔧 **Mantenimiento** | Cada parte es independiente | Arreglar bugs es más rápido |
| ♻️ **Reutilización** | Mismo Model para diferentes Views | Menos código duplicado |
| 🧪 **Testing** | Cada componente se prueba por separado | Código más confiable |
| 📈 **Escalabilidad** | Agregar funcionalidades sin romper lo existente | Crece con tu proyecto |

---

## 📝 Regla de Oro

> ### ⚠️ **Cada parte tiene UNA sola responsabilidad**

```
✅ MODEL    = DATOS
✅ VIEW     = PRESENTACIÓN  
✅ CONTROLLER = LÓGICA DE CONTROL
```

### ❌ **Nunca hagas esto:**
- Poner consultas SQL en la View
- Generar HTML en el Model
- Mezclar lógica de negocio en el Controller

### ✅ **Siempre haz esto:**
- Mantén la separación de responsabilidades
- Cada archivo/clase tiene un propósito claro
- Si algo cambia, solo afecta a una parte

---

## 🎓 Analogía del Restaurante 🍽️

**MVC es como un restaurante:**

| Componente | Rol en el Restaurante | Función en MVC |
|------------|----------------------|----------------|
| 🍳 **MODEL** | La cocina | Prepara los datos (ingredientes → comida) |
| 🤵 **CONTROLLER** | El mesero | Toma tu orden y trae la comida |
| 🍽️ **VIEW** | El plato servido | Lo que ves y consumes |

**Flujo del restaurante:**
1. Llegas y pides un plato (Usuario hace petición)
2. El mesero toma tu orden (Controller recibe)
3. La cocina prepara tu comida (Model procesa datos)
4. El mesero trae el plato (Controller envía a View)
5. Comes tu comida deliciosa (Usuario ve resultado)

**¡Cada uno hace su trabajo y juntos crean una experiencia perfecta!** 🌟

---

## 🛠️ Frameworks Populares que Usan MVC

### JavaScript / TypeScript
- ⚡ **Express.js** - Framework minimalista para Node.js
- 🅰️ **Angular** - Framework completo de Google
- 💚 **Vue.js** - Framework progresivo

### PHP
- 🔴 **Laravel** - El más popular y elegante
- 🔥 **CodeIgniter** - Ligero y rápido
- 🎵 **Symfony** - Robusto y enterprise

### Python
- 🐍 **Django** - "Batteries included" framework
- ⚗️ **Flask** - Microframework flexible

### Ruby
- 💎 **Ruby on Rails** - Convention over configuration

### Java
- 🌱 **Spring MVC** - Framework enterprise

### C#
- 🔷 **ASP.NET MVC** - Framework de Microsoft

---

## 🚀 Cómo Empezar con MVC

### Paso 1: Estructura tu proyecto

```
mi-proyecto/
│
├── models/
│   ├── UserModel.js
│   └── ProductModel.js
│
├── views/
│   ├── home.html
│   └── producto.html
│
├── controllers/
│   ├── UserController.js
│   └── ProductController.js
│
└── app.js (archivo principal)
```

### Paso 2: Crea tu primer Model

```javascript
// models/UserModel.js
class UserModel {
  constructor() {
    this.users = [];
  }
  
  obtenerTodos() {
    return this.users;
  }
  
  agregar(usuario) {
    this.users.push(usuario);
  }
}
```

### Paso 3: Crea tu Controller

```javascript
// controllers/UserController.js
class UserController {
  constructor(model) {
    this.model = model;
  }
  
  listarUsuarios() {
    return this.model.obtenerTodos();
  }
}
```

### Paso 4: Crea tu View

```html
<!-- views/usuarios.html -->
<h1>Lista de Usuarios</h1>
<ul>
  {{#each usuarios}}
    <li>{{nombre}} - {{email}}</li>
  {{/each}}
</ul>
```

---

## 📚 Recursos para Aprender Más

- 📖 [Documentación oficial de Express.js](https://expressjs.com/)
- 🎥 [Tutorial de MVC en YouTube](https://youtube.com)
- 📘 [Patrones de Diseño - Libro](https://refactoring.guru/design-patterns)
- 💻 [Práctica con proyectos reales](https://github.com)

---

## 🎯 Checklist para tu Proyecto MVC

- [ ] Estructura de carpetas clara (models, views, controllers)
- [ ] Models solo manejan datos y lógica de negocio
- [ ] Views solo muestran información
- [ ] Controllers solo coordinan entre Model y View
- [ ] Sin código duplicado
- [ ] Nombres de archivos descriptivos
- [ ] Comentarios donde sea necesario
- [ ] Testing implementado

---

## 💬 Preguntas Frecuentes

### ¿Cuándo NO usar MVC?
- Proyectos muy pequeños (una sola página simple)
- Scripts de automatización
- Prototipos rápidos

### ¿MVC es solo para web?
No, también se usa en aplicaciones de escritorio y móviles.


---

**Recuerda:**
- 📊 Model = Datos
- 🎨 View = Presentación
- 🎮 Controller = Coordinador

---

<div align="center">

</div>