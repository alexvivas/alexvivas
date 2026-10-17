# CheckPOS — Sistema de punto de venta SaaS

**Proyecto colaborativo · En desarrollo (MVP)**  
**Sector:** comercio minorista en Perú (bodegas y minimarkets).

[Repositorio original](https://github.com/AriasYarangaIam/CheckPOS) · [Arquitectura](https://github.com/AriasYarangaIam/CheckPOS/blob/main/ARCHITECTURE.md) · [Plan de desarrollo](https://github.com/AriasYarangaIam/CheckPOS/blob/main/SPRINTS.md)

## Visión del proyecto

CheckPOS busca simplificar el registro de ventas y la operación diaria de pequeños comercios, especialmente donde la conectividad puede ser inestable. El producto plantea una experiencia **mobile-first** con soporte **offline-first**, control de inventario, ventas a crédito («fiados»), cierre de caja y sincronización posterior.

> **Estado real:** el producto todavía no ofrece todo ese flujo de principio a fin. La versión revisada incorpora cimientos de identidad, base de datos y una interfaz inicial de acceso. Las operaciones comerciales siguen en desarrollo. Esta ficha distingue diseño e implementación.

## Arquitectura y tecnologías

| Componente | Tecnología verificada | Propósito |
| --- | --- | --- |
| Frontend | React, TypeScript, Vite, Tailwind CSS | Interfaz web responsive |
| Almacenamiento del cliente | Dexie / IndexedDB | Modelo local de catálogo, carrito, eventos y sesión de dispositivo |
| Backend | Go, API REST, pgx | Servicios HTTP e identidad |
| Datos | PostgreSQL, SQL, Goose | Persistencia relacional y migraciones |
| Seguridad multi-tenant | PostgreSQL RLS, roles de conexión, JWT | Aislamiento por comercio y autenticación |
| Entorno | Docker Compose | PostgreSQL local para desarrollo |
| Calidad | Tests Go y Vitest presentes en el repositorio | Cobertura de componentes y contratos; ejecución no verificada en esta revisión |

**Aclaración de stack:** esta implementación **no es** el prototipo separado con Next.js, Zustand y Supabase. En CheckPOS se eligió React con Vite y una API propia en Go. Redis y almacenamiento de objetos aparecen en el diseño arquitectónico, pero no están integrados como servicios operativos en el repositorio revisado.

## Implementado en el código revisado

- **Base de datos y aislamiento:** migraciones SQL de un modelo relacional de 14 tablas, políticas *Row Level Security* para tablas por comercio y separación de roles de acceso.
- **Backend inicial:** endpoints de salud y disponibilidad, inicio de sesión con JWT y vinculación de dispositivos para habilitar una ventana de uso offline.
- **Acceso del empleado:** pantalla de PIN de cuatro dígitos, teclado numérico, gestión de sesión local y estados de rechazo/desbloqueo en el cliente.
- **Persistencia local:** esquema IndexedDB/Dexie para catálogo local, carrito, eventos pendientes y estado de sesión.
- **Pruebas y documentación:** archivos de pruebas unitarias, integración y contratos técnicos, además de especificaciones de arquitectura y planificación por sprints.

La presencia de código y pruebas **no equivale** a una certificación de funcionamiento extremo a extremo: no se ejecutaron las suites ni se desplegó una demo durante esta revisión.

## En desarrollo o planificado

| Módulo | Situación observada |
| --- | --- |
| Catálogo comercial | Esquema y contrato definidos; CRUD de producto pendiente en el backend funcional |
| Venta de mostrador | Arquitectura y modelo definidos; flujo completo de venta todavía pendiente |
| Fiados y movimientos | Tablas y reglas documentadas; operaciones de negocio pendientes |
| Cierre de caja | Modelo relacional y criterios descritos; proceso completo pendiente |
| Sincronización de ventas offline | Estructura local y contrato de idempotencia documentados; motor completo y endpoints de venta pendientes |
| Escaneo de productos y operación comercial | Flujos objetivo definidos; no verificados como funcionalidades completas |

## Decisiones de ingeniería relevantes

1. **Separación de comercios:** el diseño extrae el identificador de tienda del token verificado, y la base utiliza políticas RLS para restringir el acceso entre tenants.
2. **Dinero sin redondeos flotantes:** el contrato contempla importes monetarios en centavos enteros.
3. **Operación offline:** la aplicación guarda información y estado local en IndexedDB; la conciliación de eventos de venta es parte del roadmap.
4. **Evolución incremental:** la arquitectura se documenta por módulos y se trabaja en sprints, con pruebas de contratos en el repositorio.

## Participación y atribución

Proyecto de equipo alojado en **[AriasYarangaIam/CheckPOS](https://github.com/AriasYarangaIam/CheckPOS)**. Mi cuenta de GitHub, **[alexvivas](https://github.com/alexvivas)**, aparece con acceso de colaborador al repositorio.

**Contribución individual:** pendiente de detallar con cambios, tareas o Pull Requests verificables. Las características anteriores describen el **trabajo del equipo**; no se atribuyen íntegramente a una sola persona.

## Referencias técnicas

- [Código y README del equipo](https://github.com/AriasYarangaIam/CheckPOS)
- [Contrato de arquitectura](https://github.com/AriasYarangaIam/CheckPOS/blob/main/ARCHITECTURE.md)
- [Contratos de base de datos](https://github.com/AriasYarangaIam/CheckPOS/blob/main/docs/DATABASE.md)
- [Plan de backend](https://github.com/AriasYarangaIam/CheckPOS/blob/main/docs/BACKEND.md)
- [Plan de frontend](https://github.com/AriasYarangaIam/CheckPOS/blob/main/docs/FRONTEND.md)
- [Sprints y criterios de aceptación](https://github.com/AriasYarangaIam/CheckPOS/blob/main/SPRINTS.md)

---

*Última revisión de esta ficha: 17 de octubre de 2026. El repositorio está en desarrollo activo; su estado puede cambiar tras nuevos commits.*
