# 📚 Sistema de Préstamos - Java + Spring Boot

## 🚀 Descripción

Sistema de gestión de préstamos desarrollado con **Java + Spring Boot**, enfocado en aplicar conceptos de:

* Programación Orientada a Objetos
* Arquitectura en capas (Dominio, Datos, Servicio)
* Persistencia con JPA/Hibernate
* Reglas de negocio reales (préstamos, sanciones, validaciones)

---

## ⚙️ Instalación y Configuración

### 🔧 1. Creación del proyecto

Se utilizó **Spring Initializr** para generar la estructura base del proyecto.

* Tipo de proyecto: **Maven**
* Dependencias utilizadas:

  * MySQL
  * Spring Data JPA
  * Lombok

---

### 📦 2. Lombok

Se utiliza Lombok para reducir código repetitivo:

* `@Getter`
* `@Setter`
* `@ToString`
* Constructores automáticos

---

### 🛢️ 3. Configuración de Base de Datos

Configuraciones principales en `application.properties`:

```properties
spring.jpa.hibernate.ddl-auto=none
spring.jpa.show-sql=true
spring.main.web-application-type=none
```

#### Explicación:

* `ddl-auto=none` → No modifica la base de datos automáticamente
* `show-sql=true` → Muestra las queries generadas por Hibernate
* `web-application-type=none` → No levanta servidor web (modo consola)

---

### 🧹 4. Logs

Se utiliza configuración de **Logback** para limpiar la consola y evitar ruido innecesario.

---

## 🧠 Conceptos Clave Aprendidos

### 🔹 JPA vs MySQL

* En JPA se trabaja con **objetos**, no con claves directamente
* Se utilizan relaciones como:

```java
@ManyToOne
@JoinColumn(name="U_Legajo")
```

* Las relaciones se manejan entre objetos (POO), no entre IDs manuales

---

### 🔹 Entidades

* Se utiliza `@Entity` para mapear clases a tablas
* Se definen columnas con `@Column`
* Enums se manejan como String:

```java
@Enumerated(EnumType.STRING)
```

* Claves autogeneradas:

```java
@GeneratedValue(strategy = GenerationType.IDENTITY)
```

---

### 🔹 Validaciones

Se usan anotaciones como:

* `@NotNull`
* `@NotBlank`
* `@Email`

⚠️ Importante:

* `@NotBlank` → solo para String
* Para validar objetos se usa `@NotNull` + `@Valid`

---

### 🔹 Capa de Datos (Repository)

* Se utilizan interfaces que extienden:

```java
JpaRepository<Entidad, ID>
```

* Spring implementa automáticamente los métodos

Ejemplo:

```java
List<Recurso> findByNombreContaining(String descripcion);
```

---

### 🔹 Capa de Servicio

* Se usa `@Service`
* Se inyectan dependencias con `@Autowired`

```java
@Autowired
private IRecursoDatos recursoDatos;
```

📌 Concepto clave:

* `@Service` crea el objeto
* `@Autowired` lo inyecta

---

### 🔹 Transacciones

Para queries de modificación:

```java
@Modifying
@Transactional
```

📌 Necesario para:

* UPDATE
* DELETE

---

## ⚠️ Problemas y Correcciones Importantes

### 1. ❗ Unique en JPA

JPA no interpreta restricciones `UNIQUE` automáticamente → se deben validar manualmente o manejar excepciones.

---

### 2. ❗ Save en JPA

```java
save()
```

* Si el ID existe → UPDATE
* Si no existe → INSERT

---

### 3. ❗ Concurrencia (Try-Catch)

Dos usuarios pueden pasar validaciones al mismo tiempo →
la base de datos debe validar definitivamente.

---

### 4. ❗ Inyección de dependencias

Siempre usar:

```java
@Autowired
```

---

### 5. ❗ Transacciones

Operaciones de modificación requieren `@Transactional`

---

### 6. ❗ Naming (Snake Case)

Spring convierte:

```text
Java → camelCase
MySQL → snake_case
```

---

### 7. ❗ Validaciones incorrectas

```java
@NotBlank Recurso recurso ❌
```

✔️ Correcto:

```java
@NotNull Recurso recurso
```

---

### 8. ❗ Optimización

Evitar:

```java
findAll() + filtros en memoria ❌
```

Usar:

```java
findBy...() ✔️
```

---

## 🏗️ Arquitectura

El sistema está organizado en capas:

```
DOMINIO → Entidades y reglas
DATOS → Repositorios JPA
SERVICIO → Lógica de negocio
```

---

## 🔁 Flujo del Sistema

Ejemplo: Registrar préstamo

1. Validar usuario
2. Validar recurso
3. Validar restricciones
4. Crear préstamo
5. Guardar en BD
6. Cambiar estado del recurso

---

## 📌 Estado del Proyecto

✔️ Funcional
✔️ Con reglas de negocio
✔️ Arquitectura en capas

🚧 Pendiente (mejoras futuras):

* Manejo de excepciones más específico
* Optimización de queries
* Mejor desacoplamiento entre servicios
* Implementación web (API REST)

---

## 🧠 Conclusión

Este proyecto representa una base sólida para entender:

* Cómo funciona Spring Boot internamente
* Cómo se conecta Java con bases de datos
* Cómo diseñar lógica de negocio real

---

## 🔄 Próximos pasos

* Continuar con el curso de Java
* Volver a este proyecto para una versión 2
* Refactorizar a nivel profesional

---

## 👨‍💻 Autor

Proyecto desarrollado como práctica de aprendizaje en Ingeniería en Sistemas.

