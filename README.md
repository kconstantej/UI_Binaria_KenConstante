Proyecto: Prevención de Pérdidas Cibernéticas – UiPath


Descripción:

Este proyecto automatiza el ejercicio "Cyber Loss Prevention" del portal Automation Anywhere Pathfinder, replicando el flujo de prevención de fraude con tarjetas de crédito.
La automatización accede a sitios simulados de la web oscura (Ryan’s Club), extrae listados de tarjetas comprometidas, valida la información en la base de datos de clientes de Eagle One Financial, genera un archivo CSV con las tarjetas identificadas y lo carga para validación final.

La solución está desarrollada sobre Robotic Enterprise Framework (REFramework) de UiPath para garantizar alta robustez, manejo de excepciones, logging detallado y reutilización de componentes.

Carpeta en Orchestrator:
Todos los Assets indicados se encuentran en la carpeta:
UI_Binaria_KenConstante

Requisitos previos:
Cuenta en Automation Anywhere A-People

Cuenta en Automation Anywhere Community Edition (A360)

SQLite Studio instalado

Instalar el odbc de Sqlite3

Acceso a Google Chrome para ejecutar la automatización.

UiPath Studio instalado (versión compatible con el proyecto).

Configurar para que la extensión de UiPath para Chrome funcione también en pestañas de incógnito. 

Configuración de Assets en Orchestrator
| Name                                | Description                                                  | Type       | Value                                                                                                         | Labels | Properties |
|-------------------------------------|--------------------------------------------------------------|------------|---------------------------------------------------------------------------------------------------------------|--------|------------|
| Cdr_AA                              | Credenciales de Automation Anywhere                          | Credential | [In credential store]                                                                                        | -      | -          |
| Cdr_RyansClub                       | Credenciales de Ryan's Club                                  | Credential | [In credential store]                                                                                        | -      | -          |
| CorreosCopiaError                   | Correo en copia para errores                                 | Text       | keencons1@gmail.com                                                                                           | -      | -          |
| CorreosError                        | Correo principal para notificaciones de error                | Text       | keencons@hotmail.com                                                                                          | -      | -          |
| Crd_PathDataBase                    | Credenciales para acceso a la base de datos SQLite           | Credential | [In credential store]                                                                                        | -      | -          |
| ExceptionMessage_ConsecutiveErrors  | Mensaje para límite de excepciones consecutivas              | Text       | Se alcanzó el número máximo de excepciones consecutivas del sistema.                                         | -      | -          |
| ExScreenshotsFolderPath             | Carpeta para guardar capturas de excepciones                 | Text       | Exceptions_Screenshots                                                                                        | -      | -          |
| logF_BusinessProcessName            | Nombre del proceso de negocio para logging                   | Text       | Prevención de pérdidas cibernéticas                                                                           | -      | -          |
| LogMessage_ApplicationException     | Mensaje para excepciones de sistema                          | Text       | Error de sistema                                                                                              | -      | -          |
| LogMessage_BusinessRuleException    | Mensaje para excepciones de regla de negocio                 | Text       | Error de regla de negocio:                                                                                    | -      | -          |
| LogMessage_GetTransactionData       | Mensaje al obtener datos de transacción                      | Text       | Procesando Transacción Número:                                                                                | -      | -          |
| LogMessage_GetTransactionDataError  | Mensaje de error al obtener datos                            | Text       | Error al obtener los datos de la transacción para el Número de Transacción:                                   | -      | -          |
| LogMessage_Success                  | Mensaje de transacción exitosa                               | Text       | Transacción exitosa                                                                                           | -      | -          |
| MaxConsecutiveSystemExceptions      | Límite de excepciones consecutivas                           | Text       | 3                                                                                                             | -      | -          |
| MaxRetryNumber                      | Límite de reintentos de transacción                          | Text       | 3                                                                                                             | -      | -          |
| NombreArchivoCsv                    | Nombre del archivo CSV final                                 | Text       | Resultado.csv                                                                                                 | -      | -          |
| NumeroCreditCardDump                | Número del volcado de tarjetas a procesar                    | Text       | 349473                                                                                                        | -      | -          |
| RetryNumberGetTransactionItem       | Reintentos para obtener ítem de transacción                  | Text       | 3                                                                                                             | -      | -          |
| RetryNumberSetTransactionStatus     | Reintentos para establecer estado de transacción             | Text       | 3                                                                                                             | -      | -          |
| UrlLoginAA                          | URL de login de Automation Anywhere                          | Text       | https://idp.automationanywhere.com/s/login/*                                                                 | -      | -          |
| UrlLoginPathfinder                  | URL de login para reto Ryan’s Club                           | Text       | https://pathfinder.automationanywhere.com/challenges/automationanywherelabs-ryansclublogin.html              | -      | -          |
| UrlPathFinder                       | URL principal del reto Cyber Loss Prevention                 | Text       | https://pathfinder.automationanywhere.com/challenges/automationanywherelabs-cyberlossprevention.html         | -      | -          |
| UrlRyansClub                        | URL de acceso al sitio Ryan’s Club                           | Text       | https://pathfinder.automationanywhere.com/challenges/automationanywherelabs-ryansclub_home.html              | -      | -          |


Estructura del REFramework
Robotic Enterprise Framework

Basado en Business Process Template

Implementa una State Machine para las fases del proceso

Incluye logging avanzado, manejo de excepciones y recuperación automática

Usa Assets en Orchestrator y/o Windows Credential Manager

Captura pantallas en caso de excepciones de sistema

Flujo de trabajo
1. INITIALIZE PROCESS
InitiAllSettings → Carga configuración desde Assets de Orchestrator

GetAppCredential → Obtiene credenciales desde Orchestrator o Credential Manager

InitiAllApplications → Abre y autentica en las aplicaciones requeridas

2. END PROCESS
CloseAllApplications → Cierra sesiones y aplicaciones abiertas durante el proceso

Flujo del proceso en este proyecto
Acceso a Pathfinder → Login con credenciales de Automation Anywhere.

Ingreso a Ryan’s Club → Obtención de listado de tarjetas (con datos parciales).

Cruce de datos con la base SQLite para encontrar coincidencias.

Generación del CSV con tarjetas comprometidas y datos del cliente.

Carga automática del CSV para validación.

Manejo de errores con logging y envío de correos automáticos.

Autor
Ken Constante
Consultor Soluciones RPA
keecons@hotmail.com

