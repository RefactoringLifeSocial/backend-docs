# 📖 Git Workflow Guidelines

Este documento define cómo vamos a trabajar en equipo con **Git** y **GitHub** para el proyecto **RefactoringLifeSocial**.  
El objetivo es mantener un flujo claro, limpio y fácil de seguir, especialmente para quienes nunca trabajaron con un flujo colaborativo.

---

## 🔀 Flujo de ramas (Git Flow simplificado)

### `main`
- **Rama protegida**  
- Contiene siempre el código **estable** y listo para producción.

### `develop`
- **Rama de integración**  
- Aquí se combinan las *features* antes de llegar a `main`.

### `feature/*`
- Para **nuevas funcionalidades**.  
- Ejemplos:  
  - `feature/login-google`  
  - `feature/adoption-request`

### `bugfix/*`
- Para **correcciones en desarrollo** *(no se usan por ahora, se evaluarán más adelante)*.  
- Ejemplo:  
  - `bugfix/fix-null-pointer`

### `hotfix/*`
- Para **arreglos urgentes en producción** *(no se usan por ahora, se evaluarán más adelante)*.  
- Ejemplo:  
  - `hotfix/fix-prod-db-connection`


## 📌 Diagrama de flujo

```lua
main   <--- hotfix
 |
develop <--- feature / bugfix
```

<br>

## 📝 Nomenclatura de ramas

- **feature/** → nuevas funcionalidades  
- **bugfix/** → correcciones en código no productivo *(no se usan por ahora, se evaluarán más adelante)*  
- **hotfix/** → correcciones en producción *(no se usan por ahora, se evaluarán más adelante)*  
- **release/** → versiones listas para despliegue *(opcional si el proyecto crece mucho)*  

### Ejemplos de nombres:
- `feature/add-pet-endpoint`  
- `bugfix/fix-email-validation`  
- `hotfix/rollback-adoption-status`
  

---

<br>

## 💬 Convenciones de commits

Usamos un formato **tipo [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/)** para que los mensajes sean claros:

```text
<tipo>(<scope>): <descripción>
```

### 🔑 Tipos más usados

| Tipo        | Descripción                                           | Ejemplo                                         |
|-------------|-------------------------------------------------------|-------------------------------------------------|
| **feat**    | Nueva funcionalidad                                   | `feat(auth): add Google login flow`             |
| **fix**     | Corrección de bug                                     | `fix(pets): correct age validation`             |
| **docs**    | Cambios en documentación                              | `docs(db): update ER diagram`                   |
| **style**   | Cambios de formato (espacios, indentación, etc.)      | `style(ui): adjust button spacing`              |
| **refactor**| Refactor de código sin cambio funcional               | `refactor(posts): simplify status handling`     |
| **test**    | Agregados o cambios en tests                          | `test(user): add unit tests for validation`     |
| **chore**   | Tareas de soporte (config, build, etc.)               | `chore(ci): update GitHub Actions workflow`     |

---

### 📌 Verbos recomendados dentro de la descripción

- **add** → cuando se agrega algo nuevo  
  - `feat(user): add profile picture upload`  
- **update** → cuando se modifica o mejora algo existente  
  - `docs(api): update endpoints list`  
- **remove**/**delete** → cuando se elimina algo  
  - `chore(deps): remove unused library`  
- **fix** → cuando se corrige un error puntual  
  - `fix(order): fix null pointer on checkout`  


### 📌 Ejemplos

```text
feat(auth): add Google login flow
fix(pets): correct age validation
docs(db): update ER diagram
refactor(posts): simplify status handling
```

## 🔐 Pull Requests (PRs)

- Todo cambio debe hacerse vía **Pull Request** hacia `develop`.  
- Las ramas `main` y `develop` estarán **protegidas**.  
- Ningún dev puede pushear directo a esas ramas.  

---

### ✅ Reglas de PR

1. **Título claro** que describa el cambio.  
   - Ejemplo: `feat(pets): add adoption interest endpoint`  
2. Cada PR debe tener al menos **2 revisiones aprobadas** antes de hacer *merge*.  
3. Debe pasar el **pipeline de CI/CD** (si existe).  
4. **Commits pequeños y claros** → evitar un único commit gigante tipo `"fix all"`.  
5. Relacionar el PR con el **issue correspondiente**  
   - Ejemplo: `Closes #12`  

<br>

## 👥 Roles en las revisiones

- **Jr:** puede abrir PR, pero necesita feedback de Semi/Senior.  
- **Semi:** revisa PR de Jr y crea PR propios, requiere aprobación de Senior.  
- **Senior:** revisa PR de Semi y mergea cuando haya consenso.  
- **Admin:** protege ramas, configura permisos y resuelve bloqueos.  

<br>

## ✅ Checklist antes de abrir un PR

- [ ] Código compilado y probado localmente  
- [ ] Tests ejecutados (si aplica)  
- [ ] Commits limpios y con mensajes claros  
- [ ] Documentación actualizada (`README`, diagramas, etc.)  

<br>

## 📂 Alcance

Este documento aplica para **todos los repositorios de la organización**.  
