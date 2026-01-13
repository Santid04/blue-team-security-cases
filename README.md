# Blue Team – Security Analysis Cases

## Descripción

Este repositorio documenta casos prácticos de análisis de seguridad desde una perspectiva Blue Team / SOC.  
Los escenarios están basados en entornos Linux reales y simulan actividades sospechosas e incidentes de seguridad, incluyendo detección, análisis, respuesta y documentación del evento.

El objetivo del repositorio es demostrar criterio analítico, lectura de logs y capacidad de evaluación de impacto, más allá del uso de herramientas específicas.

---

## Contenido del repositorio

### Caso 1 – Actividad sospechosa contenida
- Escaneo web mediante solicitudes a rutas comunes.
- Intentos fallidos de autenticación SSH.
- Bloqueo automático mediante Fail2ban.
- Sin impacto sobre el sistema.

📁 [Ver caso](./case-01-activity-suspicious/)
---

### Caso 2 – Incidente de seguridad con impacto
- Acceso exitoso al sistema mediante credenciales válidas.
- Uso de privilegios elevados.
- Evaluación de impacto y escalamiento.
- Revocación de accesos y contención del incidente.

📁 [Ver caso](./case-02-security-incident/)

---

## Alcance

Los casos documentados no representan incidentes reales en producción, sino escenarios controlados utilizados con fines educativos y de práctica en ciberseguridad defensiva.

---

## Enfoque

- Blue Team
- SOC Tier 1 / Junior
- Análisis de logs
- Correlación de eventos
- Evaluación de impacto
- Documentación técnica
