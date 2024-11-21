#### **Formato:**

- Archivo comprimido con el proyecto completo, incluyendo la carpeta src con el código de inicio y las actualizaciones, pero también los archivos necesarios para montar los contenedores; no solo debes incluir la carpeta src, sino la carpeta superior que contiene el proyecto entero.

#### **Descripción General:**

Tu tarea consiste en implementar un sistema de gestión para **items** y **enemigos** en el juego. Esto incluye las operaciones básicas de **Crear, Leer, Actualizar y Eliminar** (CRUD) para ambos tipos de entidades. El objetivo es proporcionar una interfaz en el backend que permita administrar tanto los ítems como los enemigos de manera similar a cómo se gestiona `Character`.

#### **Requisitos:**

##### **1. CRUD para Items**

1. **Crear un ítem**:
    
    - Diseña un formulario que permita al usuario introducir los datos del ítem:
        - `name` (nombre del ítem).
        - `description` (descripción del ítem).
        - `type` (`weapon`, `armor`, `potion`, `misc`).
        - `effect` (valor numérico que determine el impacto del ítem, por ejemplo, +5 fuerza).
        - `img` (nombre del archivo o URL de la imagen del ítem).
    - Al guardar, los datos deben almacenarse en la tabla `items` de la base de datos.
2. **Listar ítems existentes**:
    
    - Muestra una tabla que incluya los datos de todos los ítems:
        - `name`, `description`, `type`, `effect`, `img`.
        - Botones de acción para **editar** y **eliminar**.
3. **Actualizar un ítem**:
    
    - Crea un formulario para modificar los datos de un ítem existente.
    - Al guardar, actualiza los datos en la base de datos.
4. **Eliminar un ítem**:
    
    - Implementa la lógica para eliminar un ítem específico de la base de datos, asegurándote de que se eliminen también las relaciones existentes en tablas como `player_items` si es necesario.

---

##### **2. CRUD para Enemigos**

1. **Crear un enemigo**:
    
    - Diseña un formulario que permita introducir los datos del enemigo:
        
        - `name` (nombre del enemigo).
        - `description` (descripción del enemigo).
        - `isBoss` (un booleano que indique si es un jefe; puede implementarse como un checkbox).
        - `health` (puntos de vida).
        - `strength` (puntos de fuerza).
        - `defense` (puntos de defensa).
        - `img` (nombre del archivo o URL de la imagen del enemigo).
    - Al guardar, los datos deben almacenarse en la tabla `enemies` de la base de datos.
        
2. **Listar enemigos existentes**:
    
    - Muestra una tabla con todos los enemigos:
        - `name`, `description`, `isBoss`, `health`, `strength`, `defense`, `img`.
        - Botones de acción para **editar** y **eliminar**.
3. **Actualizar un enemigo**:
    
    - Crea un formulario para modificar los datos de un enemigo existente.
    - Al guardar, actualiza los datos en la base de datos.
4. **Eliminar un enemigo**:
    
    - Implementa la lógica para eliminar un enemigo de la base de datos.

---

#### **Requisitos Técnicos:**

1. **Modelos**:
    
    - Implementa clases `Item` y `Enemy` que incluyan métodos como `save`, `delete`, y opcionalmente métodos para recuperar datos (por ejemplo, `getAll` para listar todos los ítems o enemigos).
2. **Vistas**:
    
    - Crea las páginas necesarias para cada operación (crear, listar, actualizar, eliminar) dentro de un directorio `views/items` y `views/enemies`.
3. **Controladores**:
    
    - Diseña controladores o lógica centralizada para gestionar las operaciones de CRUD.
    - Por ejemplo:
        - `create_item.php`, `edit_item.php`, `delete_item.php` para ítems.
        - `create_enemy.php`, `edit_enemy.php`, `delete_enemy.php` para enemigos.
4. **Estilo y Usabilidad**:
    
    - Utiliza un diseño consistente con el CRUD de `Character` ya implementado.
    - Asegúrate de que las tablas y formularios sean claros y fáciles de usar.
5. **Validación de Datos**:
    
    - Valida los datos enviados por los formularios antes de guardarlos en la base de datos:
        - Campos obligatorios.
        - Longitudes máximas.
        - Valores numéricos válidos para campos como `health`, `strength`, `defense`, y `effect`.

---

#### **SQL para las nuevas tablas:**

```sql
CREATE TABLE items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL, -- Nombre del ítem
    description TEXT, -- Descripción del ítem
    type ENUM('weapon', 'armor', 'potion', 'misc') NOT NULL, -- Tipo de ítem
    effect INT NOT NULL DEFAULT 0, -- Valor numérico que indica el impacto del ítem
    img VARCHAR(255) -- Ruta o URL de la imagen asociada al ítem
);
```

```sql
CREATE TABLE enemies (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL, -- Nombre del enemigo
    description TEXT NOT NULL, -- Descripción del enemigo
    isBoss BOOLEAN NOT NULL DEFAULT FALSE, -- Indica si el enemigo es un jefe
    health INT NOT NULL, -- Puntos de vida del enemigo
    strength INT NOT NULL, -- Fuerza del enemigo
    defense INT NOT NULL, -- Defensa del enemigo
    img VARCHAR(255) -- Ruta o URL de la imagen asociada al enemigo
);
```

---

#### Estructura del proyecto
```
dwes-t3-rpg/
├── docker/
│   ├── apache/
│   │   └── Dockerfile
├── mysql_data/
├── src/
│   ├── assets/                # Recursos como imágenes, CSS o JS
│   │   ├── css/
│   │   │   └── styles.css
│   │   ├── js/
│   │   │   └── scripts.js
│   │   ├── img/
│   │   │   ├── characters/
│   │   │   ├── enemies/
│   │   │   ├── items/
│   │   │   └── rooms/
│   │   └── README.md          # Documentación para los assets
│   ├── config/
│   │   └── db.php             # Configuración de la base de datos
│   ├── model/
│   │   ├── Character.php      # Modelo para personajes
│   │   ├── Item.php           # Modelo para ítems
│   │   ├── Enemy.php          # Modelo para enemigos
│   │   └── save_character.php # Lógica para guardar personajes (deprecado si ya es manejado desde el modelo)
│   └── views/
│       ├── partials/          # Fragmentos reutilizables
│       │   └── _menu.php      # Menú de navegación
│       ├── characters/        # CRUD de personajes
│       │   ├── create_character.php
│       │   ├── edit_character.php
│       │   ├── delete_character.php
│       │   ├── list_characters.php
│       ├── items/             # CRUD de ítems
│       │   ├── create_item.php
│       │   ├── edit_item.php
│       │   ├── delete_item.php
│       │   ├── list_items.php
│       ├── enemies/           # CRUD de enemigos
│       │   ├── create_enemy.php
│       │   ├── edit_enemy.php
│       │   ├── delete_enemy.php
│       │   ├── list_enemies.php
│       ├── index.php          # Página inicial o dashboard
│       └── README.md          # Documentación para las vistas
├── .gitignore                 # Configuración para Git
├── docker-compose.yml         # Configuración de Docker
├── README.md                  # Documentación general del proyecto

```

---

#### **Objetivo Final:**

Una vez completada la tarea, deberás ser capaz de:

- Crear, listar, actualizar y eliminar tanto ítems como enemigos desde el sistema.
- Visualizar y administrar los datos de ítems y enemigos de manera eficiente y organizada.

---

#### **Evaluación:**

1. La implementación deberá cumplir con los requisitos funcionales y técnicos descritos.
2. Se valorará el uso de buenas prácticas en:
    - Organización del código.
    - Modularidad (uso adecuado de modelos y vistas).
3. La interfaz debe ser clara, intuitiva y consistente con el resto de la aplicación.

Funcionalidad del CRUD de `Enemy`
- Listado
- Creación
- Modificación
- Borrado
Funcionalidad del CRUD de `Item`
- Listado
- Creación
- Modificación
- Borrado





