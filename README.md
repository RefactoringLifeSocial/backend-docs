# Pet Adoption Platform - Database Schema

Este proyecto define la base de datos para una **plataforma social de adopción de mascotas**.  
El objetivo es que los usuarios puedan publicar mascotas que necesitan hogar, con fotos y detalles, y que otros usuarios puedan verlas y contactarse.

---

## 📌 Modelo de Datos

El modelo está diseñado bajo **mejores prácticas modernas**:
- Usuarios nunca se eliminan físicamente → se marcan con `is_active = false`.
- Roles, tipos y estados se manejan en tablas normalizadas.
- Relaciones claras con claves foráneas y restricciones de integridad.

---

## 📊 Entidades principales

### 1. Users
Representa a los usuarios de la plataforma.
- `id`: Identificador único.
- `name`: Nombre completo.
- `email`: Correo electrónico único.
- `phone`: Teléfono de contacto.
- `role_id`: Relación con `roles`.
- `created_at`: Fecha de creación.
- `is_active`: Booleano para soft delete.

### 2. Roles
Define los tipos de usuario en la plataforma.
Ejemplo:
- `ADMIN`
- `PUBLISHER` (puede publicar mascotas)
- `ADOPTER` (puede adoptar mascotas)

### 3. Pets
Información sobre la mascota.
- `name`, `breed`, `age`, `description`
- `type_id`: Relación con `pet_types` (Dog, Cat, Other)
- `status_id`: Relación con `pet_statuses` (Available, Adopted)

### 4. Posts
Publicaciones de adopción realizadas por usuarios.
- `title`, `description`
- `status_id`: Relación con `post_statuses` (Active, Closed)
- `user_id`: Relación con `users`
- `pet_id`: Relación con `pets`
- Cada post puede tener varias imágenes.

### 5. Images
Fotos asociadas a un post.
- `url`: Enlace a la imagen (almacenada en un servicio externo tipo S3/Cloudinary).
- `post_id`: Relación con `posts`.

### 6. Tablas de soporte
- `pet_types`: Dog, Cat, Other
- `pet_statuses`: Available, Adopted
- `post_statuses`: Active, Closed

---

## 🔗 Relaciones

- **Users 1—N Posts** → un usuario puede crear muchas publicaciones.
- **Posts 1—1 Pets** → cada publicación corresponde a una mascota.
- **Posts 1—N Images** → una publicación puede tener múltiples imágenes.
- **Pets 1—1 PetType** → cada mascota tiene un tipo.
- **Pets 1—1 PetStatus** → cada mascota tiene un estado (ej: disponible).
- **Posts 1—1 PostStatus** → cada post tiene un estado (ej: activo).

---

## 🔄 Flujo de uso (MVP)

1. Un usuario se registra vía Google Sign-In → se guarda en `users` con un `role` por defecto.
2. El usuario (si es `PUBLISHER`) crea una publicación:
   - Se crea un registro en `pets`.
   - Se crea un registro en `posts` asociado al usuario y a la mascota.
   - Se suben imágenes → registros en `images`.
3. Otros usuarios (rol `ADOPTER`) pueden navegar publicaciones activas.
4. Cuando una mascota es adoptada:
   - Se actualiza `pets.status_id = Adopted`.
   - Se actualiza `posts.status_id = Closed`.

---

## 🚀 Próximos pasos (más allá del MVP)

- Tabla `comments` para interacción social.
- Tabla `interests` para que un usuario exprese interés en adoptar.
- Manejo de auditoría (`updated_at`, `deleted_at`).
- Endpoints REST para la API (Spring Boot).

---

## 📂 Archivos en este repo

- `schema.sql` → DDL con la creación de tablas en PostgreSQL.
- `diagram.png` → Diagrama ER exportado de dbdiagram.io.
- `README.md` → Este archivo, guía para entender el modelo.

---

## 👨‍💻 Equipo

Este README está pensado para que **todos los niveles del equipo** (trainee, semi, senior) puedan entender:
- Qué tablas existen.
- Cómo se relacionan.
- Qué flujo sigue el sistema.

---
