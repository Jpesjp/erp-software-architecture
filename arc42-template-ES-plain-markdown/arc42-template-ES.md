---
date: Enero 2026
title: Plantilla ![arc42](images/arc42-logo.png)
---

#

**Acerca de arc42**

arc42, La plantilla de documentación para arquitectura de sistemas y de
software.

Por Dr. Gernot Starke, Dr. Peter Hruschka y otros contribuyentes.

Revisión de la plantilla: 7.0 ES (basada en asciidoc), Enero 2017

© Reconocemos que este documento utiliza material de la plantilla de
arquitectura arc42, <https://www.arc42.org>. Creada por Dr. Peter
Hruschka y Dr. Gernot Starke.

# Introducción y Metas {#ection-introduction-and-goals}

Objetivo: Centralizar la gestión del talento humano y automatizar el cálculo de nómina mediante un sistema ERP basado en la nube.

## Vista de Requerimientos {#_vista_de_requerimientos}

Gestión de Empleados: Registro, actualización y consulta de información personal y laboral.  
Gestión de Nómina: Cálculo automático de salarios, deducciones y bonificaciones.  
Control de Asistencia: Registro de horas trabajadas y ausencias.  
Reportes: Generación de informes administrativos y financieros.

## Metas de Calidad {#_metas_de_calidad}

Rendimiento: Uso de FastAPI para garantizar tiempos de respuesta bajos.  
Integridad: Uso de MongoDB Atlas para asegurar consistencia de datos.  
Escalabilidad: Arquitectura desacoplada con SPA en React y API REST.  
Disponibilidad: Servicios desplegados en la nube con alta disponibilidad.

## Partes interesadas (Stakeholders) {#_partes_interesadas_stakeholders}

+-------------+---------------------------+-----------------------------------------------+
| Rol/Nombre  | Contacto                  | Expectativas                                  |
+=============+===========================+===============================================+
| Product     | PO del Proyecto           | Maximizar eficiencia en gestión de personal  |
| Owner       |                           |                                               |
+-------------+---------------------------+-----------------------------------------------+
| Equipo de   | Dev Team                  | Contar con requisitos claros y estables      |
| Desarrollo  |                           |                                               |
+-------------+---------------------------+-----------------------------------------------+
| Gerencia    | Dirección General         | Control total sobre nómina y costos laborales|
+-------------+---------------------------+-----------------------------------------------+
| RRHH        | Departamento RRHH         | Automatizar procesos operativos              |
+-------------+---------------------------+-----------------------------------------------+

# Restricciones de la Arquitectura {#section-architecture-constraints}

Tecnología: Backend compatible con Python 3.10+.  
Seguridad: Uso obligatorio de HTTPS/TLS y JWT.  
Persistencia: Bases de datos NoSQL en la nube.  
Infraestructura: Uso exclusivo de servicios cloud.

# Alcance y Contexto del Sistema {#section-context-and-scope}

El sistema ERP gestiona información de empleados y procesos de nómina, interactuando con usuarios internos y sistemas externos.

## Contexto de Negocio {#_contexto_de_negocio}

Entradas: Datos personales, registros de asistencia, salarios.  
Salidas: Comprobantes de nómina, reportes financieros, notificaciones.

**Diagrama: Contexto de Negocio**

Usuarios → ERP RRHH → Reportes / Sistemas Externos

**Interfases externas:** Sistema contable, correo institucional.

## Contexto Técnico {#_contexto_técnico}

Entradas: Formularios web, archivos CSV, peticiones API.  
Salidas: Respuestas JSON, archivos PDF, reportes.

Estrategia de solución:

Se implementa una arquitectura de microservicios en contenedores para aislar funcionalidades.

**Diagrama: Contexto Técnico**

Frontend → API → Base de Datos → Servicios ML

**Mapeo Entrada/Salida:**

Web → HTTPS → API → MongoDB → Reportes

# Estrategia de solución {#section-solution-strategy}

Se adopta una arquitectura basada en microservicios, CI/CD automatizado y procesamiento de datos con enfoque MLOps.

# Vista de Bloques {#section-building-block-view}

## Sistema General de Caja Blanca {#_sistema_general_de_caja_blanca}

***Diagrama General***

Frontend → API Gateway → Servicios → Base de Datos

Motivación

:   Separar responsabilidades para facilitar mantenimiento.

Bloques de construcción contenidos

:   Frontend, Backend, ETL, ML, Base de Datos.

Interfases importantes

:   REST API, Conectores de datos.

### API RRHH {#_caja_negra_1}

Gestión de empleados.

Interfase: REST / JSON

Performance: < 300 ms

Ubicación: /backend/api

Requerimientos: HU-01, HU-02

Riesgos: Sobrecarga en horas pico.

### Servicio Nómina {#_caja_negra_2}

Cálculo de pagos.

### Módulo ETL {#_caja_negra_n}

Procesamiento de datos.

### API REST {#_interfase_1}

Comunicación cliente-servidor.

### Conector MongoDB {#_interfase_m}

Acceso a datos.

## Nivel 2 {#_nivel_2}

### Caja Blanca Backend

Controladores, servicios, repositorios.

### Caja Blanca Data Layer

Persistencia y cache.

## Nivel 3 {#_nivel_3}

### Caja Blanca API Empleados

Validación y lógica de negocio.

### Caja Blanca Nómina

Cálculo de deducciones.

### Caja Blanca ETL

Limpieza y transformación.

# Vista de Ejecución {#section-runtime-view}

## Registro de Empleado {#_escenario_de_ejecución_1}

- Usuario envía formulario.
- API valida datos.
- Se guarda en MongoDB.
- Se retorna confirmación.

## Cálculo de Nómina {#_escenario_de_ejecución_2}

- Sistema procesa datos.
- Calcula pagos.
- Genera reporte.

# Vista de Despliegue {#section-deployment-view}

## Nivel de infraestructura 1 {#_nivel_de_infraestructura_1}

***Diagrama General***

Navegador → Cloud API → DB Cloud

Motivación

:   Garantizar acceso remoto.

Características de Calidad

:   Alta disponibilidad y escalabilidad.

Mapeo

:   Servicios → Contenedores → Nube.

## Nivel de Infraestructura 2 {#_nivel_de_infraestructura_2}

### GitHub Codespaces

Desarrollo remoto.

### Google Colab

Procesamiento ETL.

### Databricks

Big Data.

# Conceptos Transversales (Cross-cutting) {#section-concepts}

## Seguridad

Autenticación JWT y roles.

## Logging

Registro centralizado.

## CI/CD

Automatización con GitHub Actions.

## MLOps

Entrenamiento reproducible.

# Decisiones de Diseño {#section-design-decisions}

Uso de FastAPI por rendimiento.  
Uso de MongoDB por flexibilidad.  
Uso de contenedores por portabilidad.

# Requerimientos de Calidad {#section-quality-scenarios}

## Árbol de Calidad

Disponibilidad → Rendimiento → Seguridad → Escalabilidad

## Escenarios de calidad

- Respuesta < 2s con 500 usuarios.
- Recuperación ante fallos en < 5 min.
- Acceso seguro 24/7.

# Riesgos y deuda técnica {#section-technical-risks}

Dependencia de servicios gratuitos.  
Escalabilidad limitada en versión community.  
Falta de pruebas automatizadas completas.

# Glosario {#section-glossary}

+----------------------+-----------------------------------------------+
| Término              | Definición                                    |
+======================+===============================================+
| API                  | Interfaz de programación de aplicaciones     |
+----------------------+-----------------------------------------------+
| ETL                  | Extracción, Transformación y Carga            |
+----------------------+-----------------------------------------------+
| MLOps                | Operaciones de Machine Learning               |
+----------------------+-----------------------------------------------+
| CI/CD                | Integración y Despliegue Continuo             |
+----------------------+-----------------------------------------------+
