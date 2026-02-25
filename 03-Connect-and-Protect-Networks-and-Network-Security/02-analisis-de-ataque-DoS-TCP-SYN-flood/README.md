
# Análisis de Incidente de Red: Ataque TCP SYN Flood (DoS)

## Descripción del Proyecto

Este proyecto consiste en el análisis de una interrupción del servicio web detectada en los puertos 80 y 443. El objetivo fue identificar el vector de ataque mediante la inspección de solicitudes de red y proponer medidas de mitigación para restaurar la continuidad del negocio.

## Alcance y Hallazgos Clave

* **Servicio Afectado:** Servidor Web (Puertos 80 HTTP y 443 HTTPS).
* **Herramientas Utilizadas:** Análisis de registros de tráfico (Logs / Wireshark).
* **Hallazgos Técnicos:**
    * **Protocolo TCP:** Se detectó un volumen masivo de paquetes con la **flag SYN** procedentes de una dirección IP desconocida.
    * **Handshake Incompleto:** El atacante inicia el enlace de tres vías pero nunca envía el paquete final (ACK).
    * **Estado del Servidor:** El servidor agotó su memoria disponible al intentar mantener miles de conexiones entreabiertas (half-open connections).

## Análisis del Incidente (Resumen Ejecutivo)

El incidente se manifestó como un error de tiempo de espera de conexión para los usuarios legítimos. Tras analizar los registros, se confirmó que el servidor estaba siendo blanco de un ataque de **TCP SYN Flood**, lo que impedía que el "handshake" de tres vías se completara correctamente, saturando los recursos del sistema.

## Causa Probable

Mi análisis indica que el problema se debe a un ataque de **Denegación de Servicio (DoS)**. Un actor malintencionado inundó el servidor con solicitudes SYN. Debido a la naturaleza del protocolo TCP, el servidor reserva recursos para cada solicitud; al no recibir el acuse de recibo final, la tabla de conexiones pendientes se llena, provocando la caída del servicio.

## Impacto y Continuidad del Negocio

Este evento afectó directamente la disponibilidad del sitio web, impidiendo que los clientes realizaran operaciones normales. La saturación de memoria en los servidores puso en riesgo la estabilidad de la infraestructura, resaltando la necesidad de implementar mecanismos de defensa ante ataques de inundación.

## Pasos Sugeridos para la Resolución

Como analista inicial, se escalan las siguientes recomendaciones al equipo de ingeniería:

1. **Mitigación Inmediata (ACL):** Configurar el firewall para bloquear la dirección IP del atacante mediante una lista de control de acceso. Esto detiene el golpe inmediato mientras se aplica una solución de fondo.
2. **Implementación de SYN Cookies:** Habilitar esta técnica a nivel de sistema operativo para que el servidor no reserve memoria hasta que el apretón de manos sea legítimo.
3. **Monitoreo de Conexiones:** Establecer umbrales de alerta para detectar picos anómalos de paquetes SYN en periodos cortos de tiempo.

## 📂 Archivos en esta carpeta

* **analisis_incidente_DoS.pdf:** Documento detallado con el desglose técnico del ataque y el protocolo TCP.
* **como_leer_log_TCP_wireshark.pdf:** Guía práctica sobre la identificación de flags TCP en capturas de tráfico.
* **wireshark_TCP_log.pdf:** Evidencia visual de los registros analizados durante el incidente.
