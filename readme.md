# Pizzeria Management System

## Descripción

Sistema de gestión para pizzería que incluye manejo de productos, órdenes y autenticación de usuarios. Implementado con Clean Architecture en .NET 8 para el backend y Angular 18 para el frontend.

## Tecnologías Utilizadas

### Backend

- .NET 8
- Entity Framework Core
- SQL Server
- JWT Authentication
- Clean Architecture
- CQRS Pattern
- MediatR

### Frontend

- Angular 18
- Angular Material
- Standalone Components
- JWT Authentication
- Reactive Forms
- RxJS

## Estructura del Proyecto

### Backend (Clean Architecture)

```plaintext
*Capas de una Soluci�n
|------>Capa de InfraEstructura
|	|---->Data
|		|------------>Dependencias: Common
|	|---->Interface
|		|------------>Dependencias: Entity
|	|---->Repository
|		|------------>Dependencias: Common, Data de la capa de infraestructura, Interface de la capa de infraestructura
|
|------>Capa de Dominio
|	|---->Entity
|	|---->Interface
|		|------------>Dependencias: Entity
|	|---->Core
|		|------------>Dependencias: Entity,Interfaces De la Capa de Dominio, Interfaces de la capa de infraestructura
|
|----->Capa de Aplicaci�n
|	|---->DTO
|		|------------>Dependencias: Ninguna
|	|---->Interface
|		|------------>Dependencias: Aplicacion DTO y Transversal Common
|	|---->Command (Manejo de excepciones, Manejo de transacciones, transformaci�n de objetos )
|		|------------>Dependencias: Aplicacion DTO, Aplicacion Interfaces, Aplicacion Validator, Dominio Entity, Dominio Interfaces, Transversal Common, AutoMapper
|	|---->Query (Manejo de excepciones, Manejo de Consultas )
|		|------------>Dependencias: Aplicacion DTO, Aplicacion Interfaces, Aplicacion Validator, Dominio Entity, Dominio Interfaces, Transversal Common, AutoMapper
|	|---->Validator
|		|------------>Usa libreria FluentValidation (AspNetCore), FluenValidation.DependencyInjectionExtensions, Proyecto de DTO
|
|----->*Capa de Servicios
|	|---->WebApi
|		|------------>Dependencias: TODOS los proyectos para facilitar la inyecion de dependencias entre ellos, AutoMapper, AutoMapper.Microsoft.DependencyInjection, Microsoft.AspNetCore.Mvc.NewtonsoftJson
|
|----->*Capa Transversal
|	|---->Common
|		|------------>Dependencias: Usa libreria FluentValidation (AspNetCore)
|	|---->Mapper
|		|------------>Dependencias: Ninguna
|	|---->Logging (Proyecto encargado de la trazabilidad)
|		|------------>Dependencias: Transversal.Common
|----->Capa de Pruebas
|	|---->Aplication.Test (Recibe este nombre porque probar� cada m�todo de las clases implementadas en Aplicaci�n.Main)
|		|------------>Dependencias: Microsoft.Extension.Configuration.Abstractions, Microsoft.Estensions.DependencyInjection.Abstractions
```

### Frontend (Angular)

```
plaintext
src/
├── app/
│   ├── auth/
│   │   ├── login.component.ts
│   │   └── register.component.ts
│   ├── core/
│   │   ├── components/
│   │   ├── guards/
│   │   ├── interceptors/
│   │   ├── models/
│   │   └── services/
│   ├── features/
│   │   ├── products/
│   │   └── orders/
│   └── shared/
│       ├── components/
│       └── pipes/
├── assets/
└── environments/
```

## Características Principales

### Autenticación

- Login y Registro de usuarios
- JWT Token Authentication
- Manejo de roles (Admin, user_App, user_Dashboard_App)
- Protección de rutas
- Refresh Tokens

### Gestión de Productos

- CRUD completo de productos
- Categorización
- Control de disponibilidad
- Precios y descripciones

### Gestión de Órdenes

- Creación de órdenes
- Múltiples items por orden
- Cálculo automático de totales
- Estados de orden:
  - Pending
  - InProgress
  - Ready
  - Delivered
  - Cancelled
- Historial de órdenes
- Detalles de orden

## Instalación y Configuración

### Requisitos Previos

- .NET 8 SDK
- Node.js (versión 18 o superior)
- SQL Server
- Angular CLI

### Backend Setup

1. Clonar el repositorio
2. Navegar al directorio del MicroServicePizzeria

```bash
cd MicroServicePizzeria
```

3. Restaurar paquetes NuGet

```bash
dotnet restore
```

4. Actualizar la cadena de conexión en `appsettings.json`
5. Ejecutar migraciones

```bash
dotnet ef database update --project ..\4_Infrastructure\Infrastructure.MSPizzeria.Data\ --startup-project .\Service.MSPizzeria.WebApi --context ApplicationDBContext
```

6. Ejecutar el proyecto

```bash
dotnet run
```

### Frontend Setup

1. Navegar al directorio del WebPizzeria

```bash
cd WebPizzeria
```

2. Instalar dependencias

```bash
npm install
```

3. Actualizar la URL del API en `environment.ts`
4. Ejecutar el proyecto

```bash
ng serve
```

## Uso

### Acceso al Sistema

1. Abrir el navegador en `http://localhost:4200`
2. Iniciar sesión con las credenciales (o restraste desde el endpoint, ya que no pudie integrarlo con el frontend):
   - Email: elfens95.ealc@gmail.com
   - Password: Pablito_95

### Flujo Principal

1. **Login**

   - Ingresar credenciales
   - Sistema válida y genera token
   - Redirección al dashboard

2. **Gestión de Productos**

   - Ver lista de productos
   - Crear nuevos productos
   - Actualizar existentes

3. **Gestión de Órdenes**
   - Crear nueva orden
   - Seleccionar productos
   - Especificar cantidades
   - Añadir notas
   - Procesar orden
   - Actualizar estado
   - Ver detalles

## API Endpoints

### Autenticación

```
POST /api/v1/User/login
POST /api/v1/User/register
```

### Productos

```
GET    /api/v1/product
GET    /api/v1/product/{id}
POST   /api/v1/product
PUT    /api/v1/product/{id}
```

### Órdenes

```
GET    /api/v1/order
GET    /api/v1/order/{id}
POST   /api/v1/order
PUT    /api/v1/order/{id}
```

## Consideraciones de Seguridad

- Validación de tokens JWT
- Encriptación de contraseñas
- Roles y permisos
- Cross-Origin Resource Sharing (CORS)
- Validación de entradas
- Manejo seguro de datos sensibles

## Buenas Prácticas Implementadas

- Clean Architecture
- SOLID Principles
- CQRS Pattern
- Repository Pattern
- Dependency Injection
- Error Handling
- Logging
- Data Validation
- Code First Approach
- Responsive Design
- Lazy Loading
- Component-Based Architecture

## Contribución

1. Fork el proyecto
2. Crear rama para feature (`git checkout -b feature/AmazingFeature`)
3. Commit cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abrir Pull Request

## Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE.md](LICENSE.md) para detalles

## Contacto

[Efrel López] - [efli95.ealc@gmail.com]

Project Link: [https://github.com/efrel/Pizzeria](https://github.com/efrel/Pizzeria)

## Agradecimientos

- [Angular Material](https://material.angular.io/)
- [JWT.io](https://jwt.io/)
- [Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

```

Este README proporciona:
1. Visión general del proyecto
2. Instrucciones de instalación
3. Estructura del proyecto
4. Características principales
5. Guía de uso
6. Endpoints de API
7. Consideraciones de seguridad
8. Buenas prácticas
9. Guía de contribución

```
