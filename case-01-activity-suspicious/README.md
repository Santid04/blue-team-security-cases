# Mini caso SOC 1 – Análisis de evento de seguridad

## Descripción del caso

Este repositorio documenta escenarios prácticos de análisis de seguridad desde una perspectiva Blue Team / SOC.  
El objetivo es demostrar la lectura de logs, la correlación de eventos y la evaluación de impacto ante actividades sospechosas, utilizando entornos Linux y servicios reales.

---

## Identificación del ticket

**ID:** SOC-2026-001  
**Tipo:** Actividad sospechosa  
**Severidad:** Baja  
**Estado:** Cerrado  

---

## Resumen del evento

Se detectó actividad sospechosa proveniente de una dirección IP interna del laboratorio, consistente en solicitudes web a rutas comunes seguidas de intentos fallidos de autenticación SSH.  
La actividad fue mitigada automáticamente mediante mecanismos de seguridad configurados en el sistema, sin impacto operativo.

---

## Detalle técnico del evento

### Actividad web sospechosa

**Fuente:** Apache – `access.log`

**Eventos observados:**
```
GET /admin HTTP/1.1 404
GET /privado HTTP/1.1 401
GET /privado/index.html HTTP/1.1 403
```

### Análisis

- Solicitudes repetidas a rutas comunes.
- Combinación de códigos HTTP 401, 403 y 404.
- Patrón compatible con escaneo automatizado.
- No se registraron accesos exitosos a recursos sensibles.

---

### Intentos de acceso por SSH

**Fuente:** SSH – `auth.log`

**Eventos observados:**
- Intentos fallidos de autenticación contra el usuario root desde una misma dirección IP.

**Análisis:**
- El usuario root fue utilizado como objetivo, lo cual es típico en ataques automatizados.
- Los accesos fueron denegados por las políticas de hardening configuradas en el sistema.
- No se logró autenticación exitosa.

---

### Respuesta automática del sistema

**Fuente:** Fail2ban – `fail2ban.log`

**Eventos observados:**
- La dirección IP origen fue bloqueada automáticamente tras múltiples intentos fallidos.

**Análisis:**
- Fail2ban correlacionó los fallos de autenticación.
- Se ejecutó un bloqueo preventivo para evitar nuevos intentos.
- La respuesta fue automática y no requirió intervención manual.

---

## Impacto

- No se detectó acceso exitoso al sistema.
- No se observaron modificaciones de archivos.
- No hubo escalamiento de privilegios.
- Los servicios permanecieron operativos durante todo el evento.

**Impacto general:** Bajo

---

## Clasificación del evento

| Criterio     | Evaluación               |
|--------------|--------------------------|
| Tipo         | Escaneo y fuerza bruta   |
| Origen       | IP interna (laboratorio) |
| Severidad    | Baja                     |
| Estado       | Contenido                |
| Escalamiento | No requerido             |

---

## Acciones tomadas

- Bloqueo automático de la dirección IP mediante Fail2ban.
- Revisión manual de logs de Apache y SSH.
- Verificación de las configuraciones de firewall y servicios expuestos.

---

## Conclusión

El sistema respondió correctamente ante la actividad detectada.  
Las medidas de prevención, detección y respuesta funcionaron según lo esperado.  
No se identificaron impactos sobre la integridad, disponibilidad o confidencialidad del sistema.

**Estado final:** Ticket cerrado

