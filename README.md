# flutter-shop
## 1. Resumen Ejecutivo

- **Nombre del proyecto**: FlutterShop
- **Breve descripción**: Aplicación de e-commerce que permite visualizar, filtrar y agregar productos a un carrito de compras, con funcionalidad de guardado de favoritos y gestión de perfil de usuario.

## 2. Introducción

- **Contexto y problema**: El comercio electrónico ha crecido exponencialmente en los últimos años, pero muchas pequeñas empresas carecen de aplicaciones móviles accesibles y fáciles de usar. FlutterShop busca democratizar el acceso a tecnologías de e-commerce para pequeños y medianos negocios.
- **Justificación**: Una aplicación móvil dedicada mejora la experiencia de compra, aumenta el engagement y permite a los usuarios acceder a productos desde cualquier lugar, lo que potencialmente incrementa las ventas.
- **Público objetivo**: Pequeñas y medianas empresas que deseen digitalizar su catálogo de productos, así como consumidores que prefieren la comodidad de comprar desde sus dispositivos móviles.

## 3. Objetivos

### 📌 Objetivo General

Desarrollar una aplicación de e-commerce funcional y escalable que permita a los usuarios navegar por un catálogo de productos, gestionar un carrito de compras y guardar sus preferencias, excluyendo la funcionalidad de pago como alcance inicial.

### 📌 Objetivos Específicos

- Implementar autenticación segura con Firebase Authentication.
- Crear una interfaz intuitiva y atractiva con Material Design.
- Desarrollar un sistema de navegación eficiente entre las diferentes secciones de la app.
- Integrar Firebase Firestore como base de datos para almacenar información de productos y usuarios.
- Implementar funcionalidad de búsqueda y filtrado por categorías.
- Diseñar un sistema de carrito de compras con persistencia local.
- Crear una sección de perfil de usuario para gestionar información personal y productos favoritos.

## 4. Análisis de Requerimientos

### 1.1 Módulo de Autenticación

#### Descripción

Sistema completo para gestión de usuarios que permita registro, inicio de sesión y recuperación de credenciales.

#### Funcionalidades específicas

- **Registro de usuario**:
    - Formulario con validación para: nombre completo, email, contraseña (mínimo 6 caracteres con al menos una mayúscula y un número)
- **Inicio de sesión**:
    - Acceso con email/contraseña
    - Pantalla de carga durante la autenticación
- **Gestión de sesión**:
    - Detección automática de sesión activa al iniciar la app
    - Cierre de sesión con confirmación
    - Expiración de token con renovación automática

#### Criterios de aceptación
- El registro debe completarse en menos de 60 segundos
- Los errores de validación deben mostrarse en tiempo real

### 1.2 Módulo de Catálogo de Productos

#### Descripción

Sistema para mostrar, organizar y explorar los productos disponibles en la tienda.

#### Funcionalidades específicas

- **Visualización de productos**:
    
    - Vista en grid (2 columnas) con imagen, nombre, precio y rating
    - Vista en lista con información más detallada
    - Botón para cambiar entre vistas
    - Carga lazy con paginación (10 productos por carga)
    - Pull-to-refresh para actualizar el catálogo
- **Organización por categorías**:
    
    - Menú de categorías principales con iconos
    - Subcategorías desplegables
    - Contador de productos por categoría
    - Botón de "Ver todos" para categorías con muchos productos
- **Destacados y promociones**:
    
    - Banner rotativo en la parte superior
    - Sección "Lo más vendido" con ScrollView horizontal
    - Etiquetas visuales para productos en oferta o nuevos
    - Sección "Recomendado para ti" basada en historial

#### Criterios de aceptación

- Las imágenes deben cargarse con placeholders y caché
- El tiempo de carga inicial no debe superar 2 segundos
- La navegación entre categorías debe ser fluida

### 1.3 Módulo de Detalles de Producto

#### Descripción

Pantalla detallada con toda la información relevante de un producto seleccionado.

#### Funcionalidades específicas

- **Galería de imágenes**:
    
    - Carrusel de imágenes con indicador de posición
    - Zoom al hacer tap o pinch
    - Vista fullscreen de imágenes
    - Mínimo 3, máximo 10 imágenes por producto
- **Información del producto**:
    
    - Nombre, marca y categoría
    - Precio actual y precio anterior (si hay descuento)
    - Porcentaje de descuento calculado automáticamente
    - Disponibilidad (en stock, pocas unidades, agotado)
    - Sistema de valoración con estrellas y número de reseñas
- **Detalles técnicos**:
    
    - Pestañas o acordeón para: descripción, especificaciones, reseñas
    - Tabla de especificaciones técnicas
    - Lista de características principales con iconos
    - Sección de preguntas frecuentes (si aplica)
- **Acciones disponibles**:
    
    - Selector de cantidad (1-10)
    - Selector de variantes (color, talla, etc. si aplica)
    - Botón "Agregar al carrito" con animación de confirmación
    - Botón de "Favorito" (corazón) con estado toggle
    - Botón "Compartir" para enviar link del producto

#### Criterios de aceptación

- La galería debe soportar swipe y gestos táctiles
- Las variantes deben actualizar precio e imágenes si corresponde
- El botón de agregar al carrito debe mostrar feedback visual

### 1.4 Módulo de Carrito de Compras

#### Descripción

Sistema para gestionar los productos seleccionados para compra y simular proceso de checkout.

#### Funcionalidades específicas

- **Gestión de items**:
    
    - Lista de productos con imagen, nombre, precio y cantidad
    - Botones para incrementar/decrementar cantidad
    - Botón de eliminación con confirmación
    - Opción "Guardar para después"
    - Indicador de subtotal por producto
- **Resumen del carrito**:
    
    - Subtotal (suma de productos)
    - Impuestos (calculados automáticamente - 16%)
    - Gastos de envío (estimados)
    - Total final
    - Sección de cupón de descuento (UI solamente)
- **Persistencia**:
    
    - Guardado del carrito en Firebase para usuarios autenticados
    - Guardado temporal en local storage para sesión actual
    - Recuperación del carrito al iniciar sesión
    - Opción para guardar productos para más tarde
- **Simulación de checkout**:
    
    - Formulario de dirección de envío
    - Selección de método de envío
    - UI para selección de método de pago (sin funcionalidad real)
    - Botón de "Finalizar pedido" con mensaje de simulación

#### Criterios de aceptación

- El carrito debe actualizarse en tiempo real al modificar cantidades
- El carrito debe persistir al cerrar la app
- Los productos agotados deben marcarse visualmente

### 1.5 Módulo de Búsqueda y Filtrado

#### Descripción

Sistema completo para encontrar productos mediante búsqueda textual y diferentes filtros.

#### Funcionalidades específicas

- **Búsqueda textual**:
    
    - Barra de búsqueda persistente o accesible desde ícono
    - Sugerencias mientras se escribe
    - Historial de búsquedas recientes
    - Búsqueda por nombre, marca, descripción y SKU
    - Mensajes apropiados para resultados vacíos
- **Filtros avanzados**:
    
    - Por rango de precio (slider)
    - Por categoría y subcategoría (checkboxes)
    - Por valoración (estrellas mínimas)
    - Por disponibilidad (en stock/todos)
    - Por descuento (con descuento/todos)
- **Navegación de resultados**:
    
    - Paginación con carga lazy (10 resultados por página)
    - Posibilidad de cambiar entre vista grid y lista
    - Contador de resultados totales
    - Indicador visual de filtros activos con opción para eliminarlos

#### Criterios de aceptación

- La búsqueda debe ser tolerante a errores de tipeo
- Los filtros deben poder combinarse entre sí
- Los resultados deben actualizarse inmediatamente al cambiar filtros

### 1.6 Módulo de Perfil de Usuario

#### Descripción

Sistema para gestionar la información personal, preferencias y actividad del usuario.

#### Funcionalidades específicas

- **Gestión de datos personales**:
    
    - Visualización y edición de nombre, email y foto
    - Cambio de contraseña
    - Gestión de direcciones predeterminadas
- **Lista de favoritos**:
    
    - Grid con productos marcados como favoritos
    - Opción para eliminar individualmente
    - Botón para agregar directamente al carrito
    - Vaciar lista completa con confirmación

#### Criterios de aceptación

- Los cambios en el perfil deben guardarse en Firebase
- Los favoritos deben almacenarse en Firebase para acceso desde cualquier dispositivo
- El historial debe almacenarse en Firebase con la cuenta del usuario

## 2. Requerimientos No Funcionales 

### 2.1 Performance

- **Tiempo de inicio**: La app debe iniciar en menos de 3 segundos en dispositivos de gama media
- **Tiempo de carga de catálogo**: Menos de 2 segundos para la primera carga, menos de 1 segundo para cargas subsiguientes
- **Scroll fluido**: Mínimo 60 FPS en scroll de listas y grids
- **Consumo de memoria**: Menos de 150MB en uso normal
- **Rendimiento de Firebase**: Menos de 1.5 segundos para operaciones de lectura/escritura


### 2.2 Usabilidad

- **Diseño responsive**: Adaptación a pantallas de celulares
- **Navegación intuitiva**: Máximo 3 taps para llegar a cualquier función
- **Feedback visual**: Para todas las acciones del usuario
- **Mensajes de error**: Claros, específicos y con sugerencias de solución

### 2.3 Compatibilidad

- **Android**: Versión mínima 6.0 (API 23), objetivo 13.0 (API 33)
- **Tamaños de pantalla**: Optimización para smartphones (4-6.7").


### 2.5 Escalabilidad

- **Arquitectura modular**: Separación clara de componentes para facilitar expansión
- **Escalabilidad de Firebase**: Uso de índices y consultas optimizadas
- **Actualización de contenido**: Mecanismo para actualizar catálogo sin actualizar app
- **Manejo de errores**: Sistema robusto para detectar y manejar fallos de conectividad o servidor

## 5. Arquitectura del Sistema

- **Patrón de arquitectura**: MVVM (Model-View-ViewModel) facilitado por GetX
    
- **Estructura de carpetas**:
    
    - `/lib`
        - `/models` - Clases de datos
        - `/views` - Pantallas UI
        - `/controllers` - Lógica de negocio con GetX
        - `/services` - Conexión a Firebase y APIs
        - `/utils` - Helpers y utilidades
        - `/widgets` - Componentes reutilizables
    - `/assets` - Imágenes y recursos
- **Flujo de datos**: Unidireccional desde la UI a los controllers y viceversa, utilizando observables de GetX
    

## 6. Desarrollo y Funcionalidades

### Pantallas principales:

#### Pantalla de Bienvenida y Autenticación

- Onboarding con introducción a la app
- Formulario de login con email/contraseña
- Opción de registro para nuevos usuarios

#### Pantalla de Inicio (Home)

- Banners promocionales (Carousel)
- Categorías destacadas (ScrollView horizontal)
- Productos populares
- Búsqueda rápida
- Bottom Navigation Bar para navegación principal

#### Catálogo y Búsqueda

- GridView con productos paginados
- Barra de búsqueda con sugerencias
- Filtros por categoría, precio y valoración
- Ordenamiento por relevancia, precio y novedades
- Indicador de disponibilidad de productos

#### Detalles de Producto

- Galería de imágenes con zoom
- Información detallada del producto
- Valoraciones y opiniones
- Productos relacionados
- Botones para agregar al carrito o a favoritos

#### Carrito de Compras

- Lista de productos seleccionados
- Ajuste de cantidades
- Cálculo de subtotales
- Opción para guardar para después
- Simulación de checkout (sin procesamiento de pago)

#### Perfil de Usuario

- Información personal editable
- Productos favoritos
- Historial de productos vistos
- Opción de cierre de sesión

## 7. Metodología de Trabajo

- **Enfoque ágil**: Scrum adaptado con sprints de una semana
- **Herramientas de gestión**: Github projects para seguimiento de tareas
- **Control de versiones**:
    - GitHub con pull requests y code reviews
    - Convenciones de commit siguiendo Conventional Commits
- **Reuniones**:
    - Daily standup de 15 minutos
    - Sprint planning al inicio de cada semana
    - Retrospectiva al finalizar cada sprint
