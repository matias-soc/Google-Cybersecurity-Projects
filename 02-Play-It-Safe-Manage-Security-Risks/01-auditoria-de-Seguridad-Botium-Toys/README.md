# Auditoría de Seguridad: Botium Toys
> **Proyecto de Evaluación de Riesgos y Cumplimiento**

## Descripción del Proyecto
Este proyecto forma parte del certificado de **Google Cybersecurity**. El objetivo fue realizar una auditoría interna a la empresa "Botium Toys" para evaluar su postura de seguridad actual, identificar vulnerabilidades críticas y asegurar el cumplimiento de normativas internacionales (**PCI DSS, GDPR, NIST**).

## Alcance y Objetivos
* **Alcance:** Infraestructura IT, activos físicos, gestión de datos de clientes y sistemas heredados.
* **Objetivos:** Identificar brechas en los controles de seguridad y proponer un plan de mitigación de riesgos.

## Principales Hallazgos
* **Copias de seguridad:** No existen backups fuera del sitio (off-site).
* **Cifrado:** Datos sensibles (PII/SPII) y tarjetas de crédito almacenados en texto plano.
* **Accesos:** No se aplica el principio de "mínimo privilegio".
* 
## Recomendaciones
* **Estrategia de Backups:** Realización de backups físicos y digitales fuera del establecimiento para evitar riesgos de pérdida o robos.
* **Protección de Datos:** Aplicación inmediata de controles de seguridad y cifrado en el manejo de datos **PII y SPII** para blindar las bases de datos.

## 📂 Archivos en esta carpeta
* `botium-toys-report.pdf`: Informe completo de alcance y evaluación de riesgos.
* `Controls-and-compliance-checklist.pdf`: Lista de verificación detallada de controles.
