# tarea1-naimireth-coder

📑 Guía de Arquitectura Web: Descifrando Django y los Fundamentos Backend:

1. 💾 ¿Qué es un CRUD y cuál es su propósito?
En el desarrollo de software, independientemente de la complejidad del sistema, casi toda la gestión de información se reduce a cuatro operaciones esenciales conocidas bajo el acrónimo CRUD:

➕ Create (Crear): Insertar nuevos registros o datos en el sistema.

🔍 Read (Leer): Consultar, buscar y visualizar la información almacenada.

📝 Update (Actualizar): Modificar o editar datos que ya existen.

🗑️ Delete (Borrar): Eliminar un registro de la base de datos de forma permanente o lógica.

Su propósito fundamental es proporcionar una interfaz o capa intermedia para que los usuarios finales interactúen con bases de datos de forma segura y visual, sin necesidad de conocer o ejecutar sentencias complejas de lenguaje de consultas (SQL).

📱 Ejemplo del mundo real: Gestión de Redes Sociales
Cualquier plataforma de interacción social (como la gestión de perfiles o publicaciones) opera bajo esta estructura:

Crear: Al subir una nueva fotografía al servidor.

Leer: Al navegar por la pantalla principal visualizando el contenido de otros usuarios.

Actualizar: Al modificar el pie de foto o la ubicación de una publicación existente para corregir un error.

Borrar: Al eliminar o archivar una publicación del perfil.

2. 📐 Patrones de Arquitectura: Diferencias Fundamentales entre MVC y MVT
Un patrón de arquitectura es una plantilla u organización estructural probada para el desarrollo de software. Su objetivo es separar las diferentes responsabilidades del código (datos, lógica de negocio e interfaz) para garantizar que el proyecto sea escalable, mantenible y modular.

🏛️ El patrón MVC (Modelo–Vista–Controlador)
Es el estándar tradicional de la industria. Divide el software en tres capas diferenciadas:

Modelo (Model): Gestiona los datos, define las reglas de negocio y se comunica directamente con la base de datos.

Vista (View): Representa la interfaz de usuario. Es la capa visual con la que interactúa el cliente (HTML, CSS, elementos gráficos).

Controlador (Controller): El intermediario central. Recibe las peticiones del usuario desde la Vista, solicita los datos pertinentes al Modelo y determina qué respuesta devolver.

🐍 El patrón MVT (Modelo–Vista–Template)
Es la variante utilizada por entornos de desarrollo como Django. Modifica sutilmente la asignación de roles del patrón tradicional:

Modelo (Model): Mantiene la misma función. Define las estructuras de datos y tablas.

Vista (View): Actúa de forma análoga al Controlador de MVC. Contiene la lógica de negocio; procesa las solicitudes, interactúa con el modelo y decide qué datos enviar a la salida.

Template (Plantilla): Es el equivalente a la Vista de MVC. Son archivos HTML dinámicos encargados exclusivamente del diseño y la presentación final de la información.


3. 🗺️ Estructura y Roles en un Proyecto Django
La organización interna de Django distribuye las tareas basándose en el flujo de peticiones web. Se puede entender mediante la analogía del servicio de un establecimiento:

🛰️ URLs (urls.py) — El Recepcionista: Recibe la petición de la dirección web (ej. /perfil/) introducida en el navegador, valida el destino y redirige el flujo hacia la función lógica correspondiente.

🍳 Vistas (views.py) — El Procesador Central: Recibe la orden de la URL, procesa los algoritmos o lógica del negocio, solicita datos específicos y construye la respuesta final.

📦 Modelos (models.py) — El Gestor de Datos: Estructura las tablas mediante clases de Python (ORM). Sabe exactamente qué campos (nombres, fechas, tipos de datos) existen y extrae la información requerida.

🍽️ Templates (templates/) — La Presentación: Estructuras HTML preparadas para recibir la información procesada por la vista y desplegarla visualmente ante el usuario.

⚡ Uso de etiquetas {% %} en plantillas
Los archivos HTML en Django utilizan un motor de renderizado dinámico. Los caracteres {% %} delimitan etiquetas de control o lógica de programación (ciclos for, condicionales if), permitiendo modificar el documento antes de ser enviado al navegador:

HTML
{% if usuario.is_authenticated %}
  <p>Sesión activa: {{ usuario.nombre }}</p>
{% else %}
  <p>Por favor, inicie sesión para acceder al contenido.</p>
{% endif %}
4. 🔄 El Flujo de Datos: Del Formulario a la Persistencia
El ciclo de vida de la información desde una interfaz de usuario hasta el almacenamiento persistente sigue un camino estructurado:

[ Formulario Web ] ──( Petición POST )──> [ URLs ] ──> [ Vista ] ──> [ Validación (Form) ] ──> [ Modelo ] ──> [ Base de Datos ]
🛫 Envío: El usuario completa un formulario web y presiona un botón de acción, disparando una petición HTTP (frecuentemente mediante el método POST).

🔀 Enrutado: El servidor recibe la petición y el archivo urls.py determina qué Vista debe manejar la transacción.

🛡️ Validación: La Vista recibe los parámetros de entrada y comprueba su integridad (tipos de datos correctos, campos obligatorios completos).

💾 Almacenamiento: Una vez validados, la Vista invoca los métodos de guardado (.save()). El Modelo traduce el objeto de Python a comandos nativos SQL e inserta los registros en la base de datos.

🛬 Confirmación: Tras la inserción exitosa, el servidor emite una directiva de redirección hacia una página de confirmación o éxito.

🧰 5. Caja de Herramientas y Comandos Esenciales
Django opera bajo una filosofía de desarrollo ágil, ofreciendo herramientas automatizadas desde la interfaz de comandos (Terminal):

⚙️ startapp: Genera la estructura modular para un subcomponente específico del proyecto, manteniendo el aislamiento del código.

🌐 runserver: Inicia un servidor web local de desarrollo (por defecto en http://localhost:8000/) para visualizar los cambios en tiempo real.

📸 makemigrations: Examina los archivos models.py y detecta modificaciones estructurales, generando un archivo histórico de instrucciones (plano de migración).

🏗️ migrate: Lee las instrucciones de las migraciones pendientes y aplica los cambios físicos directamente en el esquema de la base de datos.

📋 ModelForm: Clase especializada que vincula un modelo de datos con una interfaz de formulario, generando automáticamente el mapeo de campos HTML necesarios.

👁️ 6. El Panel de Administración de Django
Una de las ventajas competitivas de Django es su entorno administrativo integrado. Proporciona una interfaz gráfica web segura y preconstruida para realizar operaciones CRUD completas sobre los modelos definidos, sin necesidad de escribir código adicional de frontend.

Para su habilitación se requiere:

Generar una cuenta administrativa desde la terminal: python manage.py createsuperuser.

Registrar las entidades correspondientes dentro del archivo de configuración admin.py.

El acceso mediante la ruta /admin permite supervisar el estado de los datos almacenados, realizar pruebas de inserción rápidas y validar la persistencia de los registros del sistema.

🔌 7. Arquitectura REST y Django Rest Framework (DRF)
El diseño clásico de Django (MVT) se basa en un servidor monolítico que entrega páginas web estructuradas en HTML directo al cliente. No obstante, las arquitecturas desacopladas modernas requieren esquemas orientados a servicios.

La arquitectura REST (Representational State Transfer) establece que el backend no debe preocuparse por la representación visual, sino únicamente por la transferencia de datos puros, estandarizados bajo formatos ligeros como JSON. Esto permite que un único backend sirva simultáneamente a aplicaciones móviles, interfaces SPA (React, Vue, Angular) o servicios externos de procesamiento.

🧠 ¿Qué es Django Rest Framework (DRF)?
Es una extensión especializada que dota a Django de las herramientas necesarias para la construcción de APIs RESTful:

Serializadores (Serializers): Clases encargadas de traducir los tipos de datos complejos de los modelos de Python a formato JSON (salida) y de validar y transformar los datos JSON entrantes a objetos de base de datos (entrada).

Vistas de API (API Views): Controladores optimizados para responder flujos de datos estructurados gestionando métodos HTTP estándar de manera nativa.