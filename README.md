# Proyecto Gestor Hospitalario

## 📚 SGA - Sistema de Centros Medicos
Este proyecto es un sistema de gestión académica completo, compuesto por una API RESTful desarrollada en ASP.NET Core, conectada a una base de datos MySQL en maquinas virtuales con Ubuntu server 24, con una interfaz web básica (HTML + JS) para gestionar en los centro Medicos los Empleados, Medicos, consultas medicas y especialidades.

## 🏥 Sistema de Gestión Hospitalaria Distribuido
## 🧰 Tecnologías Utilizadas
Componente	Tecnología
Backend	ASP.NET Core 7, Entity Framework Core, Swagger/OpenAPI
Base de Datos	MySQL 8.0 (Configuración distribuida Maestro-Esclavo)
Frontend	HTML5, CSS3, JavaScript (Vanilla)
Infraestructura	3 VMs Ubuntu Server 24.04 (VirtualBox)
Seguridad	CORS Policies, Validaciones en capa de controlador
DevOps	Configuración manual de replicación MySQL

```
Gestor_Hospitalario/
├── 📁 Context/
│   └── HospitalContext.cs           # Configuración EF Core y DbSets
├── 📁 Controllers/
│   ├── CentrosMedicosController.cs  # 350+ líneas (CRUD completo)
│   ├── ConsultaMedicaController.cs  # Con validación de horarios
│   ├── EmpleadoController.cs        # Gestión de personal administrativo
│   ├── EspecialidadesController.cs  # Simple CRUD
│   └── MedicoController.cs          # Relación con especialidades
├── 📁 DTos/
│   ├── CentroMedico/                # Separación por entidad
│   │   ├── CreateDTO.cs             # Validaciones Required
│   │   ├── ReadDTO.cs               # Proyecciones seguras
│   │   └── UpdateDTO.cs             # 
│   ├── ConsultaMedica/              # DTOs para consultas
│   └── ...                          # Similar estructura para otras entidades
├── 📁 Models/
│   ├── CentroMedico.cs              # Modelo principal
│   ├── ConsultaMedica.cs            # Con relaciones
│   ├── Empleado.cs                  # 
│   ├── Especialidad.cs              # 
│   └── Medico.cs                    # Relación N:1 con Especialidad
├── 📁 Migrations/                    # Historial de migraciones EF
├── 📁 wwwroot/
│   ├── 📁 css/                       # Styles.css + Normalize
│   ├── 📁 js/                        # 5 archivos modularizados
│   │   ├── main.js                  # Lógica principal
│   │   └── entidades/               # JS por módulo
│   └── index.html                   # Interfaz única con tabs
├── appsettings.json                 # Cadenas de conexión
├── Program.cs                       # Configuración CORS y Swagger
└── Infraestructura.md               # Guía de configuración VMs
```

## 🔄 Diagrama de Flujo - Creación de Consulta Médica
sequenceDiagram
    Frontend->>+Backend: POST /api/ConsultaMedica/Crear (DTO)
    Backend->>+Validación: Verificar solapamiento horario
    Validación-->>-Backend: OK/Error
    Backend->>+MySQL Master: INSERT consulta
    MySQL Master->>MySQL Slave: Replicación (binlog)
    MySQL Slave-->>-Backend: ACK
    Backend-->>-Frontend: 201 Created (ReadDTO)


## 📊 Estructura de la API REST
```csharp
{
  "CentrosMedicos": {
    "Endpoints": {
      "GET Listar": "/api/CentrosMedicos/Listar",
      "POST Crear": {
        "Body": {
          "Nombre": "string (required)",
          "Direccion": "string (required)",
          "Telefono": "string (required)",
          "Email": "string (required)"
        },
        "Validaciones": [
          "Nombre único por dirección",
          "Formato email válido"
        ]
      }
    },
    "EjemploResponse": {
      "CentroID": 1,
      "Nombre": "Hospital Central",
      "Direccion": "Av. Principal 123",
      "Telefono": "022345678",
      "Email": "contacto@hospitalcentral.com"
    }
  }
}
```

![230b2cab-0151-4b75-ab19-1a81f86331e4](https://github.com/user-attachments/assets/943226fd-1d5a-4941-b355-5b293f667799)


