# Análisis de Incidente de Red: Ataque de Fuerza Bruta (FBA)

## Descripción del Proyecto
[cite_start]Este proyecto consiste en la investigación y documentación de un incidente de seguridad que afectó al sitio web `yummyrecipesforme.com`[cite: 42]. [cite_start]El objetivo fue identificar el vector de ataque utilizado por un ex-empleado para comprometer el servidor web, inyectar código malicioso y redirigir el tráfico legítimo hacia un dominio fraudulento[cite: 42].

## Alcance y Hallazgos Clave
* [cite_start]**Servicio Afectado:** Panel de administración del Host Web y Servidor HTTP (Puerto 80)[cite: 35, 42].
* [cite_start]**Herramientas Utilizadas:** Análisis de registros de tráfico (`tcpdump`) y entorno de pruebas seguro (*sandbox*)[cite: 43, 44].
* **Hallazgos Técnicos:**
    * [cite_start]**Modelo TCP/IP:** El incidente involucró protocolos en las cuatro capas, destacando **HTTP** en la capa de aplicación y **TCP** en la de transporte[cite: 35, 36].
    * [cite_start]**Vector de Entrada:** Un ataque de **fuerza bruta** exitoso contra la cuenta administrativa tras el uso de credenciales comprometidas[cite: 42].
    * [cite_start]**Redirección de Red:** Se detectó un cambio de IP hacia la dirección `192.0.2.172` vinculada al dominio malicioso `greatrecipesforme.com`[cite: 50, 51].



## Análisis del Incidente (Resumen Ejecutivo)
[cite_start]El incidente se descubrió cuando el dueño del sitio notó que no podía acceder a su cuenta debido a un cambio de contraseña no autorizado[cite: 41]. [cite_start]El análisis forense reveló que, tras obtener acceso al panel de administración, el atacante inyectó una función de **JavaScript** para forzar la descarga de malware[cite: 42]. [cite_start]Los registros muestran que a las **14:20:32**, el tráfico del navegador fue redirigido mediante una nueva resolución de DNS hacia un servidor externo malicioso[cite: 49, 50].

## Causa Probable
[cite_start]La vulnerabilidad principal fue la capacidad del atacante para realizar un ataque de **fuerza bruta** debido a una gestión de contraseñas débil[cite: 42]. [cite_start]Al utilizar el protocolo **HTTP (Puerto 80)**, los datos viajaban sin cifrado, facilitando el compromiso inicial y la ejecución del archivo malicioso[cite: 35, 47, 48].



## Impacto y Continuidad del Negocio
[cite_start]Este evento provocó la infección de los equipos de los usuarios finales con malware que ralentizaba su funcionamiento[cite: 42]. [cite_start]La pérdida del control administrativo y la suplantación de identidad del sitio mediante la redirección a `greatrecipesforme.com` representaron un riesgo crítico para la reputación de la organización[cite: 42, 51].

## Pasos Sugeridos para la Resolución
Como analista de ciberseguridad, se escalan las siguientes recomendaciones:
1. [cite_start]**Autenticación de Múltiples Factores (MFA/2FA):** Implementar sistemas de códigos únicos para evitar que una contraseña comprometida permita el acceso al sistema[cite: 57].
2. [cite_start]**Principio de Mínimo Privilegio (PoLP):** Asignar permisos estrictamente por puesto y revisar regularmente los accesos concedidos a los empleados[cite: 58].
3. [cite_start]**Hardening de Contraseñas:** Exigir cambios regulares y prohibir el uso de contraseñas anteriores o débiles[cite: 56].
4. [cite_start]**Cifrado de Comunicaciones:** Migrar al protocolo **HTTPS (Puerto 443)** para proteger la integridad de los datos y evitar ataques de sniffing[cite: 59].

## 📂 Archivos en esta carpeta
* [cite_start]**analisis_incidente_FBA.pdf:** Informe detallado con el mapeo del modelo TCP/IP y análisis cronológico de los logs[cite: 31].
* **actividad_analisis_de_ataque.pdf:** Documento de la actividad a realizar.
* **tcpdump_traffic_FBA.pdf:** Los logs posteriormente analizados, la evidencia del ataque de fuerza bruta.



[Image of Multi-factor authentication process]
