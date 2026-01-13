# Mini caso SOC 2 – Incidente de seguridad con impacto

## Identificación del ticket

**ID:** SOC-2026-002  
**Tipo:** Incidente de seguridad  
**Severidad:** Media  
**Estado:** Cerrado  

---

## Resumen del evento

Se detectó un acceso exitoso al sistema a través del servicio SSH desde una dirección IP no habitual, utilizando credenciales válidas de un usuario del sistema. Posteriormente se observaron comandos ejecutados con privilegios elevados. El incidente fue contenido mediante acciones manuales y el acceso fue revocado.

---

## Detalle técnico del evento

### Acceso exitoso por SSH

**Fuente:** SSH – `auth.log`

**Eventos observados:**
- Inicio de sesión exitoso desde una dirección IP no habitual.
- Usuario válido del sistema utilizado para el acceso.

**Análisis:**
- El acceso no se realizó desde una IP conocida del laboratorio.
- No hubo intentos fallidos previos desde esa IP.
- El uso de credenciales válidas sugiere posible compromiso de credenciales.

---

### Uso de privilegios elevados

**Fuente:** SSH / sudo – `auth.log`

**Eventos observados:**
- Ejecución de comandos mediante `sudo` tras el inicio de sesión.

**Análisis:**
- El usuario autenticado pertenece al grupo sudoers.
- Se detectó elevación de privilegios poco tiempo después del login.
- No se puede confirmar intención maliciosa, pero el patrón es anómalo.

---

### Actividad posterior al acceso

**Fuente:** Sistema – `auth.log` y `syslog`

**Eventos observados:**
- Ejecución de comandos administrativos.
- Accesos a archivos del sistema.

**Análisis:**
- No se detectaron modificaciones persistentes.
- No se observaron nuevos usuarios creados.
- No se identificó instalación de software adicional.

---

## Impacto

- Se produjo acceso no autorizado al sistema.
- Existió potencial riesgo de compromiso del sistema.
- No se confirmaron cambios persistentes ni pérdida de información.

**Impacto general:** Medio

---

## Clasificación del evento

| Criterio     | Evaluación                     |
|--------------|--------------------------------|
| Tipo         | Acceso no autorizado           |
| Vector       | Credenciales comprometidas     |
| Origen       | IP externa                     |
| Severidad    | Media                          |
| Estado       | Contenido                      |
| Escalamiento | Requerido                      |

---

## Acciones tomadas

- Cierre inmediato de la sesión activa.
- Revocación de credenciales del usuario comprometido.
- Revisión de logs del sistema.
- Validación de integridad del sistema.
- Notificación y escalamiento al responsable del entorno.

---

## Recomendaciones

- Rotación periódica de credenciales.
- Revisión de privilegios de usuarios.
- Refuerzo de autenticación multifactor.
- Monitoreo continuo de accesos exitosos.
- Capacitación en buenas prácticas de seguridad.

---

## Conclusión

El incidente fue detectado a tiempo y contenido sin impacto crítico sobre el sistema. La rápida identificación del acceso anómalo permitió evitar modificaciones persistentes. Se recomienda reforzar las medidas de autenticación y monitoreo para prevenir incidentes similares.

**Estado final:** Ticket cerrado
