# Documentación de StoreFrontend

**Una Aplicación React Moderna para la Gestión de Productos**

## Visión General

**StoreFrontend** es una aplicación web elegante y moderna diseñada para gestionar un inventario de productos. Construida con **React** y potenciada por **Vite**, ofrece una experiencia de usuario rápida y receptiva. La interfaz de usuario está creada utilizando **Chakra UI**, lo que proporciona un sistema de diseño consistente y accesible con soporte integrado para modo oscuro.

La aplicación permite a los usuarios ver una lista de productos, agregar nuevos productos, actualizar los existentes y eliminarlos. Interactúa con una API externa de Express.js alojada en Vercel.

## Stack Tecnológico

- **Framework Frontend:** React 18
- **Herramienta de Construcción:** Vite
- **Librería UI:** Chakra UI (v3) con Emotion
- **Gestión de Estado:** Zustand
- **Enrutamiento:** React Router (v7)
- **Iconos:** React Icons
- **Animaciones:** Framer Motion
- **Tema:** Next-themes para Modo Oscuro/Claro

## Instalación y Configuración

Sigue estos pasos para configurar el proyecto localmente:

1. **Clonar el repositorio:**

   ```bash
   git clone https://github.com/tuusuario/StoreFrontend.git
   cd StoreFrontend
   ```

2. **Instalar dependencias:**

   ```bash
   npm install
   ```

3. **Ejecutar el servidor de desarrollo:**

   ```bash
   npm run dev
   ```

4. Abre `http://localhost:5173` (o el puerto que se muestre en tu terminal) para ver la aplicación.

## Estructura del Proyecto

```tree
src/
├── components/          # Componentes de UI reutilizables
│   ├── ui/              # Componentes específicos de Chakra UI (snippets)
│   ├── Modal.jsx        # Modal de actualización de productos
│   ├── Navbar.jsx       # Barra de navegación superior
│   └── ProductCard.jsx  # Tarjeta de visualización de producto individual
├── pages/               # Componentes a nivel de ruta
│   ├── CreatePage.jsx   # Página para crear nuevos productos
│   └── HomePage.jsx     # Página principal listando productos
├── store/               # Gestión de estado global
│   └── product.js       # Store de Zustand para operaciones de productos
├── App.jsx              # Diseño principal de la aplicación y rutas
└── main.jsx             # Punto de entrada envolviendo App con proveedores
```

## Desglose de Componentes

### Navbar (`src/components/Navbar.jsx`)

El encabezado de navegación. Presenta:

- **Diseño Responsivo:** Se adapta a pantallas móviles y de escritorio.
- **Cambio de Tema:** Cambia entre modo Claro y Oscuro usando `useColorMode`.
- **Enlace de Creación:** Acceso rápido a la página "Create Product".

### ProductCard (`src/components/ProductCard.jsx`)

Muestra información individual del producto, incluyendo imagen, nombre y precio. Incluye botones de acción para:

- **Editar:** Abre el componente `Modal`.
- **Eliminar:** Activa la acción `deleteProduct` del store.

_Nota de Diseño:_ Utiliza un efecto glassmorphism en la UI (`backdropBlur`).

### Modal (`src/components/Modal.jsx`)

Un componente de diálogo construido con los primitivos Dialog de Chakra UI. Maneja la funcionalidad de **Actualización**. Gestiona su propio estado local para los inputs del formulario antes de sincronizarse con el store global al enviar.

### CreatePage (`src/pages/CreatePage.jsx`)

Una página dedicada para agregar nuevos productos. Valida las entradas y llama a la API para crear un producto. Los mensajes de éxito o error se muestran utilizando un sistema de notificaciones toast.

## Gestión de Estado y API

El proyecto utiliza **Zustand** para una gestión de estado global simplificada, ubicada en `src/store/product.js`.

### Endpoints de API

El store se comunica con el backend en `https://express-on-vercel-c2s.vercel.app/api/products`.

### Acciones del Store

- `fetchProducts()`: Petición GET para recuperar todos los productos.
- `createProduct(newProduct)`: Petición POST. Incluye validación para nombre, precio y URL de imagen.
- `deleteProduct(pid)`: Petición DELETE para eliminar un producto por ID.
- `updateProduct(pid, updatedProduct)`: Petición PUT para modificar detalles del producto.

**Manejo de Errores:** Todas las acciones devuelven un objeto `{ success: boolean, message: string }` que es utilizado por los componentes de la UI para mostrar retroalimentación apropiada (Toasts) al usuario.
