# Análisis de Incidente de Red: Diagnóstico DNS e ICMP

## Descripción del Proyecto
Este proyecto consiste en el análisis de una interrupción del servicio en el dominio `www.yummyrecipesforme.com`. El objetivo fue realizar un triaje inicial mediante la inspección de registros de tráfico para identificar la causa raíz de la denegación de servicio reportada por los usuarios.

## Alcance y Hallazgos Clave
* **Servicio Afectado:** DNS (Puerto 53 UDP).
* **Herramientas Utilizadas:** Análisis de logs mediante `tcpdump`.
* **Hallazgos Técnicos:**
    * **Protocolo UDP:** Se detectaron consultas con la **flag A?** (solicitud de registro de dirección) que no recibieron respuesta del servidor, indicando un fallo en el mapeo del dominio a la dirección IP.
    * **Protocolo ICMP:** El análisis reveló mensajes de error **"Port Unreachable"** (Puerto inalcanzable) dirigidos al puerto 53.
    * **Estado del Puerto:** El puerto 53 no estaba escuchando consultas en el momento del incidente.

## Análisis del Incidente (Resumen Ejecutivo)
El incidente ocurrió a las **13:24:32.192571**. El equipo de TI detectó la anomalía tras recibir múltiples reportes de clientes que no podían acceder al dominio. Tras analizar los logs, se confirmó que el tráfico DNS estaba siendo rechazado explícitamente, impidiendo la resolución de nombres para los usuarios finales.

## Causa Probable
Mi análisis como principiante indica que el problema apunta a un **ataque de Denegación de Servicio (DoS)**. Un actor malicioso realizó un ataque enviando repetidamente información al servidor DNS. En consecuencia, el firewall bloqueó la conexión por actividad sospechosa y, debido a esta configuración de seguridad, se encuentra bloqueando actualmente todas las consultas al puerto 53, incluyendo las legítimas.

## Impacto y Continuidad del Negocio
Este incidente generó una pérdida total de disponibilidad del servicio para los clientes. El bloqueo del firewall, aunque preventivo, resultó en un falso positivo que afectó la continuidad del negocio al impedir el acceso al dominio principal, lo que resalta la importancia de ajustar los umbrales de detección de intrusos.

## Pasos Sugeridos para la Resolución
Como analista inicial, se escalan las siguientes recomendaciones al equipo de ingeniería:
1. **Revisión del Firewall:** Analizar las reglas de bloqueo automático y transicionar hacia un filtrado por IP de origen sospechosa.
2. **Monitoreo de Logs:** Verificar si tras el ajuste persisten registros de dudosa procedencia.
3. **Prueba de Servicio:** Asegurar que el puerto 53 vuelva a estar operativo y escuchando consultas para restaurar la normalidad.

## 📂 Archivos en esta carpeta
* **analisis_incidente_DNS.pdf:** Documento detallado con el desglose técnico de los protocolos.
* **capturas/**: Carpeta que contiene las capturas de pantalla de los logs de `tcpdump` analizados.
