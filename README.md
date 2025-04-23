# Proyecto Gestor Hospitalario

📚 SGA - Sistema de Gestión Académica
Este proyecto es un sistema de gestión académica completo, compuesto por una API RESTful desarrollada en ASP.NET Core, conectada a una base de datos PostgreSQL en la nube (Railway), con una interfaz web básica (HTML + JS) para gestionar estudiantes, profesores, materias y semestres.


🧰 Tecnologías utilizadas
✔️ ASP.NET Core 8
✔️ Entity Framework Core
✔️ PostgreSQL (hosteado en Railway)
✔️ Swagger / OpenAPI
✔️ HTML5, CSS3, JavaScript
✔️ REST API + JSON
✔️ Arquitectura limpia (MVC simplificado)




📂 Estructura del Proyecto
Proyecto Gestor Hospitalario/
├── Acciones de GitHub/
├── Connected Services/
├── Dependencias/
├── Properties/
│   └── launchSettings.json
├── Context/
│   └── HospitalContext.cs
├── Controllers/
│   ├── ControlMedicoController.cs
│   ├── ConsultaMedicasController.cs
│   ├── EmpleadoController.cs
│   ├── EspecialidadController.cs
│   └── MedicosControllers.cs
├── DTos/
│   ├── ControlMedicoDTos.cs
│   ├── ConsultasMedicasDTos.cs
│   ├── EmpleadoDTos.cs
│   ├── EspecialidadDtos.cs
│   └── MedicosDTos.cs
├── Migrations/
│   ├── 20250423030645_Initial.cs
│   └── HospitalContextModelSnapshot.cs
├── Models/
│   ├── ControlMedico.cs
│   ├── ConsultaMedica.cs
│   ├── Empleado.cs
│   ├── Especialidad.cs
│   └── Medico.cs
├── appsettings.json
├── Gestor Hospitalario.http
├── Program.cs
└── WeatherForecast.cs


🗃️ Base de datos
Proveedor: PostgreSQL
Host: Railway (base en la nube)
Configuración: vía Program.cs directamente
🔒 Se recomienda moverla a appsettings.json con GetConnectionString("DefaultConnection").

options.UseNpgsql("Host=interchange.proxy.rlwy.net;Port=56434;Database=ferrocarril;Username=postgres;Password=...");

Tablas creadas:
Personas (con herencia entre Estudiante y Profesor)
Cursos (obsoleta, migrar a Materias)
EstudiantesCursos (obsoleta, usar Semestre + Materia)


⚙️ Endpoints REST (actuales)
Estudiantes
GET /api/Estudiantes → Obtener todos
POST /api/Estudiantes → Crear nuevo
PUT /api/Estudiantes/{cedula} → Editar existente
DELETE /api/Estudiantes/{cedula} → Eliminar
Profesores
GET /api/Profesor → Obtener todos
POST /api/Profesor → Crear nuevo
PUT /api/Profesor/{cedula} → Editar
DELETE /api/Profesor/{cedula} → Eliminar
Cursos (❌ obsoleto → migrar a materias/semestres)
GET /api/Cursos
POST /api/Cursos
...


🖥️ Interfaz web (wwwroot/index.html)
HTML con pestañas para cada sección:
Estudiantes
Profesores
Materias
Semestres
Conexión vía fetch al backend en script.js
Incluye validaciones de cédula, emails institucionales, etc.
Contiene buscador con ícono de lupa por cédula (modal emergente)


⚒️ Cómo ejecutar
🔌 Requisitos
.NET 8 SDK
PostgreSQL (local o Railway)
Visual Studio o VS Code
🚀 Pasos
git clone https://github.com/tu-usuario/SGA.Api.git
cd SGA.Api
dotnet restore
dotnet ef database update   # si necesitas migrar desde cero
dotnet run
Accede a:

Swagger: https://localhost:{puerto}/swagger
Interfaz Web: https://localhost:{puerto}/index.html


🚧 Estado del Proyecto
🔄 En transición de Cursos a un modelo con Materias + Semestres
🧩 Implementación de gestión por paralelo (A, B) y búsqueda avanzada por cédula
📦 Preparado para despliegue en Render + Railway (versión nube)

💡 Características destacadas
Herencia de modelos (Persona → Estudiante/Profesor)
Relaciones correctas EF Core (1:N y N:N)
Arquitectura limpia separada en: Modelos, Controladores, Contexto
Interfaz moderna integrada con JS puro

