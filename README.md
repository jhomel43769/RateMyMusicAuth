# 🔐 Rate My Music - Auth Service (Los Pies)

Bienvenido a la documentación de **RateMyMusicAuth**. Este microservicio es el pilar de la gestión de usuarios, desarrollado en **.NET 10**.

## 🚀 ¿Qué hace este servicio?

Este microservicio gestiona toda la lógica de autenticación y autorización:
- Registro de nuevos usuarios y creación de sus perfiles.
- Login de usuarios y validación de credenciales.
- Encriptación y verificación de contraseñas usando **BCrypt**.
- Emisión de **Tokens JWT (JSON Web Tokens)** para el acceso seguro a toda la plataforma.
- Interacción con la base de datos SQL Server mediante **Entity Framework Core**.

## 📁 Estructura del Proyecto

El proyecto sigue una arquitectura limpia (basada en responsabilidades):

- `Controllers/`: Define los endpoints de la API (ej. `AuthController` para login/registro).
- `Services/`: Contiene la lógica de negocio (generación de tokens, validación de contraseñas).
- `Interfaces/`: Define los contratos (interfaces) invertiendo dependencias para los *Services*.
- `Models/`: Entidades de dominio que se mapean a la Base de Datos (ej. `User`, `Profile`).
- `DTOs/`: Data Transfer Objects. Modelos que definen qué datos entran y salen de la API.
- `Data/`: Configuración del `DbContext` de Entity Framework Core.
- `Migrations/`: Archivos autogenerados para el control de versiones de la base de datos.
- `Program.cs`: Configuración de dependencias (Inyección de Dependencias), Swagger, Autenticación y middlewares.

## 🛠️ Requisitos Previos

- [.NET 10 SDK](https://dotnet.microsoft.com/)
- SQL Server (puedes usar LocalDB, SQL Server Express o Docker).

## 🏃‍♂️ Cómo levantar el proyecto localmente

1. **Clonar y restaurar paquetes:**
   ```bash
   dotnet restore
   ```

2. **Configurar la Base de Datos:**
   Asegúrate de tener un servidor SQL Server corriendo. Revisa el archivo `appsettings.Development.json` y verifica la cadena de conexión (`DefaultConnection`). Deberás actualizar el *Server* y *Database* si usas una configuración distinta.

3. **Ejecutar migraciones (Si es la primera vez):**
   ```bash
   dotnet ef database update
   ```
   *(Requiere tener la herramienta `dotnet-ef` instalada: `dotnet tool install --global dotnet-ef`)*

4. **Correr la aplicación:**
   ```bash
   dotnet run
   ```
   El servicio iniciará generalmente en un puerto local (ej. `http://localhost:5001`). Una vez corriendo, puedes acceder a **Swagger** en la ruta `/swagger` para probar los endpoints interactivamente.

---

## 🏗️ Topología del Ecosistema

Para entender cómo encaja esta pieza en el rompecabezas de 4 partes:

1. 👤 **La Cabeza:** [RateMyMusicPage](https://github.com/Jhomel-Dev/RateMyMusicPage) - Frontend UI.
2. 🚪 **El Cuello:** [RateMyMusicGateway](https://github.com/Jhomel-Dev/RateMyMusicGateway) - Enrutador.
3. 🦶 **Los Pies (Backend):**
   * 🔐 **[RateMyMusicAuth](https://github.com/Jhomel-Dev/RateMyMusicAuth)** (👉 **Estás aquí**)
   * ☁️ **[RateMyMusicMedia](https://github.com/Jhomel-Dev/RateMyMusicMedia)** - Subida de archivos.
