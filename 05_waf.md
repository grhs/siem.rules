# Catálogo SOC GrayHats — Sección 5: WAF

---

## 5. WAF

Monitorización del tráfico web y API protegido por el WAF para detectar explotación de vulnerabilidades, bots, account takeover, abuso de APIs, exfiltración, scraping, fraude de aplicación, evasión del WAF y cambios peligrosos en la postura de protección.

---

### WAF-01 — Explotación de vulnerabilidades web

> ¿Alguien está explotando una vulnerabilidad web?

- SQL injection
- XSS
- RCE
- LFI/RFI
- Path traversal
- Command injection

#### Fichas detalladas — WAF-01 (Imperva App Protect — Portal web)

---

##### WAF.01.IMPERVA.WEB.001 — Ataque de inyección web detectado por Imperva

| Campo | Detalle |
|---|---|
| **Descripción** | Imperva Cloud WAF ha detectado un payload de ataque web en tráfico entrante hacia el portal: SQL injection, Cross-Site Scripting (XSS), Remote File Inclusion (RFI), Local File Inclusion (LFI) o Command Injection. El SOC debe determinar si el ataque ha sido bloqueado (`act = block`) o ha pasado en modo detección (`act = alert`). |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Logs CEF de Imperva Cloud WAF en formato `CEF:0\|Incapsula\|SIEMIntegration`. Campos clave: `waf.event` (tipo de ataque: SQLi, XSS, RFI…), `waf.eventcode`, `waf.act` (block/alert), `waf.src` (IP origen), `waf.request` (URL atacada), `waf.requestMethod`, `waf.country.code`, `waf.rulename`. |
| **Arquitectura de ingesta** | `Imperva Cloud WAF → (API pull CEF) → Agente Wazuh Ubuntu colector → fichero /var/log/incapsulaWAF.log → Manager Wazuh`. Requiere activar SIEM Logs en la consola Imperva (Account > SIEM Logs > WAF Log Setup), seleccionar Imperva API como connection mode y formato CEF. |
| **Lógica de detección** | Reglas custom sobre decoder `imperva-waf`. Event codes relevantes: SQLi → 1, XSS → 2, RFI → 10, LFI → 11, Command Injection → 14. Niveles orientativos: `act = alert` → nivel 7, `act = block` → nivel 9. |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1059 — Command and Scripting Interpreter (según técnica) |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere desplegar el agente colector Ubuntu, configurar el pull de logs vía API de Imperva y desplegar decoders y reglas custom en el manager. Documentación oficial disponible en wazuh.com/blog. |
| **Falsos positivos** | Bajos. Imperva aplica sus propias firmas antes de alertar. Posibles FP con pentests autorizados; coordinar ventanas de exclusión con el cliente. |
| **Prioridad de investigación** | Máxima cuando `waf.act = alert` (modo detección, el payload ha llegado al backend). Media cuando `waf.act = block`. |
| **Referencia** | [wazuh.com/blog/integrating-imperva-cloud-web-application-firewall-cwaf](https://wazuh.com/blog/integrating-imperva-cloud-web-application-firewall-cwaf/) |
| **Estado** | Pendiente de validación. |

---

##### WAF.01.IMPERVA.WEB.002 — DDoS / HTTP flood contra el portal detectado por Imperva

| Campo | Detalle |
|---|---|
| **Descripción** | Imperva Cloud WAF ha detectado un ataque de denegación de servicio contra el portal web. Al estar en la nube, Imperva absorbe el volumen antes de que llegue a la infraestructura del cliente, lo que lo diferencia de NET.01.PALO.TRAFFIC.002 (que detecta el DDoS cuando ya ha llegado al perímetro). |
| **Clasificación GrayHats** | 6.2 DDoS (Denegación distribuida de servicio) / 6.1 DoS (Denegación de servicio) |
| **Peligrosidad** | ALTO |
| **Telemetría** | Logs CEF de Imperva — `waf.event = DDoS`, `waf.eventcode = 8`. Campos clave: `waf.src`, `waf.country.code`, `waf.request`, `waf.http.code`, volumen de eventos en ventana de tiempo. |
| **Lógica de detección** | Regla custom: `waf.eventcode = 8` AND `waf.event = DDoS` → nivel 9, con `ignore = 60` para evitar tormenta de alertas durante el ataque. Regla de correlación adicional: N eventos DDoS en 60s desde distintas IPs → nivel 12 (ataque distribuido activo). |
| **MITRE ATT&CK** | T1498 — Network Denial of Service / T1499 — Endpoint Denial of Service |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo una vez desplegado el colector — la detección es un event code específico. El `ignore` en la regla es crítico para no saturar el manager durante ataques volumétricos. |
| **Falsos positivos** | Muy bajos. Imperva aplica umbrales antes de clasificar como DDoS. |
| **Relación con otros CU** | Complementa NET.01.PALO.TRAFFIC.002. Si ambas alertas disparan simultáneamente el ataque está superando la mitigación cloud y llegando al perímetro. |
| **Estado** | Pendiente de validación. |

---

##### WAF.01.IMPERVA.WEB.003 — Bloqueo por reputación de IP o geolocalización

| Campo | Detalle |
|---|---|
| **Descripción** | Imperva ha bloqueado tráfico entrante al portal por política de ACL: IP en lista negra, rango de IPs bloqueado, país bloqueado o URL bloqueada. Útil para detectar intentos de acceso desde orígenes con mala reputación o geografías no autorizadas por el cliente. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Logs CEF de Imperva — `waf.event = ACL (block country/IP/URL)`, `waf.eventcode = 3`. Campos clave: `waf.src`, `waf.country.code`, `waf.city.code`, `waf.request`, `waf.act`. |
| **Lógica de detección** | Regla custom: `waf.eventcode = 3` → nivel 4 (informativo por defecto). Regla de correlación: N bloqueos ACL desde la misma IP en 60s → nivel 8 (intento persistente desde IP bloqueada). Regla adicional: bloqueos desde país no esperado para ese sitio → nivel 6. |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1078 — Valid Accounts (según contexto) |
| **Severidad** | Baja / Media (según patrón de correlación) |
| **Esfuerzo** | Bajo — event code específico. El tuning de umbrales de correlación requiere conocer el baseline de tráfico legítimo por país para cada cliente. |
| **Falsos positivos** | Medios. Usuarios legítimos en viaje, IPs corporativas en rangos bloqueados, CDNs con IPs de reputación mixta. Proceso de excepción necesario. |
| **Estado** | Pendiente de validación. |

---

##### WAF.01.IMPERVA.WEB.004 — Campaña coordinada: múltiples técnicas desde misma fuente

| Campo | Detalle |
|---|---|
| **Descripción** | Una misma IP de origen genera alertas de distintos tipos de ataque en una ventana de tiempo corta: reconocimiento seguido de inyección, o combinación de SQLi + XSS + RFI. Patrón de atacante activo realizando una campaña manual o semi-automatizada contra el portal. Mayor confianza que alertas individuales. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 3.1 Escaneo de redes (scanning) / 10.1 APT |
| **Peligrosidad** | CRÍTICO |
| **Telemetría** | Correlación de múltiples eventos CEF de Imperva con distintos `waf.eventcode` y mismo `waf.src` en ventana temporal. |
| **Lógica de detección** | Regla custom de correlación: 3+ eventos con `waf.event` distintos desde el mismo `waf.src` en 300s → nivel 12. Requiere que las reglas individuales (WEB.001, WEB.003) estén activas como fuente de correlación. No existe event code específico en Imperva para este patrón; es detección de segundo nivel en Wazuh. |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1595 — Active Reconnaissance |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — requiere diseño de regla de correlación multi-evento con estado en Wazuh. Dependiente de que las reglas base (WEB.001, WEB.003) estén operativas y tuneadas. |
| **Falsos positivos** | Muy bajos. La combinación de múltiples técnicas desde una misma IP en ventana corta es altamente indicativa de actividad maliciosa. |
| **Estado** | Pendiente de validación. |

---

#### Fichas detalladas — WAF-01 (Imperva App Protect — API)

---

##### WAF.01.IMPERVA.API.001 — Violación de especificación de API detectada por Imperva

| Campo | Detalle |
|---|---|
| **Descripción** | Imperva ha detectado una petición a la API que viola su especificación OpenAPI/Swagger importada en la plataforma: parámetro no esperado, método HTTP no permitido, tipo de dato incorrecto, endpoint no definido. Indicador de enumeración de API, BOLA (Broken Object Level Authorization) o intento de acceder a endpoints no documentados. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Logs CEF de Imperva — campo `waf.rule.violation` extraído de `cs11` con valor `api_specification_violation_type`. Campos clave: `waf.src`, `waf.request` (endpoint atacado), `waf.requestMethod`, `waf.act`, `waf.rule.info`. |
| **Lógica de detección** | Regla custom: presencia de `waf.rule.violation` → nivel 7. Regla de correlación: N violaciones de especificación desde el mismo `waf.src` en 120s → nivel 10 (enumeración sistemática de API). |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1595.003 — Active Scanning: Wordlist Scanning |
| **Severidad** | Media / Alta (según patrón) |
| **Esfuerzo** | Medio — requiere que la especificación OpenAPI esté importada en Imperva para el sitio API. Sin especificación importada esta ficha no aplica. |
| **Falsos positivos** | Medios. Clientes de API con versiones desactualizadas, desarrolladores en pruebas. Coordinación con el equipo de desarrollo para mantener la especificación actualizada en Imperva. |
| **Requisito previo** | Especificación OpenAPI/Swagger importada y activa en el sitio API de Imperva. |
| **Estado** | Pendiente de validación. |

---

##### WAF.01.IMPERVA.API.002 — Abuso de tasa de API / scraping detectado por Imperva

| Campo | Detalle |
|---|---|
| **Descripción** | Una IP o cliente está realizando un número excesivo de peticiones a la API en un intervalo corto, superando los límites de tasa configurados en Imperva. Patrón típico de scraping automatizado, credential stuffing contra endpoints de autenticación, o abuso de endpoints de consulta de datos. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 6.6 Agotamiento de recursos |
| **Peligrosidad** | MUY ALTO |
| **Telemetría** | Logs CEF de Imperva — `waf.event` relacionado con rate limiting o bot detection. Campos clave: `waf.src`, `waf.request` (endpoint abusado), `waf.requestMethod`, `waf.act`, `waf.requestClientApplication` (User-Agent), `waf.clappsig` (firma de cliente). |
| **Lógica de detección** | Regla custom sobre event codes de rate limiting y bot detection de Imperva. Nivel orientativo: detección individual → 6, bloqueo por rate limit → 8. Regla de correlación: mismo `waf.src` supera umbral de eventos en 60s → nivel 10. |
| **MITRE ATT&CK** | T1110.004 — Credential Stuffing / T1595 — Active Reconnaissance (según endpoint) |
| **Severidad** | Media / Alta (según endpoint abusado) |
| **Esfuerzo** | Medio — requiere configurar las políticas de rate limiting y bot detection en el sitio API de Imperva. Sin políticas activas, Imperva no genera eventos de este tipo. |
| **Falsos positivos** | Medios. Integraciones legítimas con picos de tráfico, clientes con reintentos agresivos. Whitelist de rangos IP de integradores conocidos. |
| **Nota operativa** | Prestar especial atención cuando el endpoint abusado es `/auth`, `/login`, `/token` o similar — patrón de credential stuffing contra la API con mayor probabilidad de impacto. |
| **Estado** | Pendiente de validación. |

---

### WAF-02 — Ataques contra APIs

> ¿Están abusando de las APIs expuestas?

- BOLA/IDOR
- Enumeración de objetos
- Manipulación de tokens
- Shadow APIs

---

### WAF-03 — Bot malicioso

> ¿El tráfico automatizado está abusando de la aplicación?

- Scrapers y scanners
- Headless browsers
- Bots distribuidos con rotación de IP

---

### WAF-04 — Account Takeover

> ¿Alguien está tomando control de cuentas?

- Credential stuffing
- Password spraying
- Brute force contra login
- Actividad anómala post-login

---

### WAF-05 — Fraude transaccional

> ¿Se usan los flujos web de forma fraudulenta?

- Spam en formularios
- Creación masiva de cuentas
- Fraude en checkout

---

### WAF-06 — Rate abuse / DDoS de aplicación

> ¿Se abusa hasta degradar la disponibilidad?

- Peticiones excesivas por IP/usuario
- Slow DDoS
- Abuso de endpoints pesados

---

### WAF-07 — Reconocimiento web

> ¿Alguien está explorando la aplicación?

- Escaneo de directorios
- Búsqueda de paneles admin
- Incremento de 404/403

---

### WAF-08 — Acceso a rutas sensibles

> ¿Se intenta acceder a recursos sensibles?

- Acceso a `/admin`, `.env`, `.git`
- Endpoints internos publicados
- Consolas de administración

---

### WAF-09 — Abuso de sesión

> ¿Una sesión web está siendo manipulada?

- Robo de cookies
- JWT manipulados
- Session fixation
- Escalada funcional

---

### WAF-10 — Exfiltración web

> ¿Se extraen datos vía funcionalidades legítimas?

- Descargas masivas
- Scraping
- Abuso de exportaciones CSV/Excel

---

### WAF-11 — Manipulación de lógica de negocio

> ¿Se abusa de la lógica de la aplicación?

- Cambio de precios
- Acceso a IDs de otros usuarios
- Bypass de flujo

---

### WAF-12 — Upload malicioso

> ¿Se sube contenido malicioso?

- Web shells
- Doble extensión
- MIME type inconsistente

---

### WAF-13 — Inyección HTTP

> ¿Las peticiones contienen payloads ofensivos?

- SQLi/XSS en parámetros
- XXE
- Cabeceras manipuladas
- Payloads ofuscados

---

### WAF-14 — Evasión WAF

> ¿Alguien intenta esquivar las reglas?

- Encoding múltiple
- Verb tampering
- Payloads polimórficos

---

### WAF-15 — Ataques a CMS/frameworks

> ¿Se atacan tecnologías concretas?

- WordPress y plugins
- Laravel `.env`
- Log4Shell-like payloads
- Apache Struts RCE

---

### WAF-16 — Supply chain web

> ¿Hay abuso de dependencias externas?

- Scripts externos anómalos
- Magecart / skimming web

---

### WAF-17 — Georreputación

> ¿El origen del tráfico aumenta el riesgo?

- Países no esperados
- IPs de mala reputación
- Nodos TOR
- Data centers vs residenciales

---

### WAF-18 — Campañas coordinadas

> ¿Se está ante una campaña organizada?

- Mismo payload contra muchas URLs
- Ataques distribuidos
- Escaneo lento distribuido

---

### WAF-19 — Configuración WAF

> ¿Se ha debilitado la protección WAF?

- Reglas desactivadas
- Bypass rules nuevas
- Cambios en rate limits

---

### WAF-20 — Bypass WAF / origen expuesto

> ¿Alguien ataca directamente el backend?

- Tráfico directo al origen
- IP de origen descubierta
- Dominios alternativos no protegidos

---


---

