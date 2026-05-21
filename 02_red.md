# Catálogo SOC GrayHats — Sección 2: Red

---

## 2. Red

Detecciones basadas en el análisis del tráfico de red para identificar actividad maliciosa o anómala en las comunicaciones entre equipos, usuarios, sedes, servicios e Internet. Fuentes principales: logs de firewall, IDS/IPS, proxy, DNS, VPN, NetFlow, Wazuh.

---

### NET-01 — Intrusión perimetral

> ¿Alguien está intentando entrar desde fuera?

- Intentos de explotación contra servicios expuestos
- Ataques contra VPN, portales web
- Intentos contra RDP, SSH, FTP, SMB o servicios publicados
- Ataques de fuerza bruta desde Internet
- Explotación de CVE conocidas
- Tráfico detectado por IDS/IPS

#### Fichas detalladas — NET-01 (Palo Alto)

---

##### NET.01.PALO.THREAT.001 — Explotación de vulnerabilidad detectada por Palo Alto IPS

| Campo | Detalle |
|---|---|
| **Descripción** | El módulo Threat Prevention de Palo Alto ha detectado un intento de explotación de una vulnerabilidad conocida contra un servicio expuesto. El IPS ha inspeccionado el payload y lo ha clasificado como `vulnerability` o `exploit`. El SOC debe determinar si el ataque ha tenido éxito (acción `allow`) o ha sido bloqueado (`reset-both`, `drop`). |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `vulnerability`. Campos clave: `threat_name`, `threat_id`, `severity` (low/medium/high/critical), `action`, `src_ip`, `dst_ip`, `dst_port`, `application`. Llega al manager por syslog directo del firewall. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` en `0700-paloalto_rules.xml`. Niveles orientativos por severidad del threat: informational → 3, low → 5, medium → 7, high → 10, critical → 12. Requiere filtrar por subtipo `vulnerability` para este caso de uso concreto. |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application |
| **Severidad** | Alta / Crítica (según severidad del threat en PAN-OS) |
| **Esfuerzo** | Bajo — built-in. Requiere configurar el Syslog Profile en PAN-OS para enviar Threat logs al manager y validar que el decoder `paloalto` los parsea correctamente. |
| **Falsos positivos** | Bajos. El IPS de PA aplica firmas específicas; posibles FP con escáneres de vulnerabilidades autorizados (mitigación: whitelist por IP de origen). |
| **Prioridad de investigación** | Máxima cuando `action = allow` — el exploit puede haber llegado al destino. Media cuando `action = reset-both` o `drop` — bloqueado pero requiere seguimiento si hay repetición. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.THREAT.002 — Brute force desde Internet detectado por Palo Alto

| Campo | Detalle |
|---|---|
| **Descripción** | Palo Alto ha detectado múltiples intentos de autenticación fallidos contra un servicio expuesto desde una misma IP de origen. El IPS clasifica el patrón como `brute-force` dentro del Threat log. Complementa los casos de brute force de endpoints (EP-02) añadiendo visibilidad perimetral antes de que el intento llegue al sistema destino. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `brute-force` o `flood`. Campos clave: `threat_name`, `src_ip`, `dst_ip`, `dst_port`, `application`, `action`, `repeat_count`. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto`. Niveles orientativos: medium → 7, high → 10. Para correlación avanzada: regla custom que agrupe múltiples eventos `THREAT/brute-force` desde la misma `src_ip` en ventana de tiempo (similar al patrón EP.02.WIN.AUTH.001). |
| **MITRE ATT&CK** | T1110 — Brute Force |
| **Severidad** | Media-Alta |
| **Esfuerzo** | Bajo — built-in para detección individual. Medio si se quiere correlación de volumetría por IP origen. |
| **Falsos positivos** | Bajos. Escáneres autorizados pueden generar fallos legítimos; whitelist por IP de origen. |
| **Relación con otros CU** | Si el brute force supera el perímetro, la detección continúa en EP.02.WIN.AUTH.001 (brute force remoto en el endpoint destino). Ambas alertas deben correlarse en la investigación. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.TRAFFIC.001 — Port scanning / reconocimiento perimetral

| Campo | Detalle |
|---|---|
| **Descripción** | Una IP externa está realizando reconocimiento activo contra el perímetro: múltiples conexiones rechazadas hacia distintos puertos o hosts en un intervalo corto. Patrón típico de pre-ataque para identificar servicios expuestos. El Traffic log registra las sesiones denegadas por política. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | BAJO |
| **Telemetría** | Traffic log de PAN-OS — tipo `TRAFFIC`, acción `deny` o `drop`, `session_end_reason` = `policy-deny`. Campos clave: `src_ip`, `dst_ip`, `dst_port`, `protocol`, `application` = `not-applicable`, `bytes` muy bajos (SYN sin respuesta). |
| **Lógica de detección** | No existe regla built-in específica para port scanning en el ruleset Palo Alto de Wazuh. Requiere regla custom de correlación: N eventos `TRAFFIC/deny` desde la misma `src_ip` hacia distintos `dst_port` en ventana de tiempo (ej. 20 puertos en 60s). Alternativamente, activar la firma de reconocimiento en el perfil de Threat Prevention del firewall (genera Threat log, cubierto por THREAT.001). |
| **MITRE ATT&CK** | T1046 — Network Service Discovery |
| **Severidad** | Media |
| **Esfuerzo** | Medio — requiere regla custom de correlación en Wazuh o activación de la firma de reconocimiento en PA. El Traffic log tiene volumen alto; la regla debe ser eficiente. |
| **Falsos positivos** | Medios. Escáneres de seguridad autorizados (Nessus, Qualys) generan el mismo patrón; whitelist imprescindible. |
| **Nota de volumen** | El Traffic log de PA puede ser muy voluminoso. Se recomienda filtrar en el Syslog Profile de PAN-OS para enviar solo sesiones `deny`/`drop` y reducir el ruido. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.WF.001 — Payload malicioso en tráfico entrante (WildFire)

| Campo | Detalle |
|---|---|
| **Descripción** | WildFire ha analizado un fichero o payload que viajaba en tráfico entrante y lo ha clasificado como malicioso o grayware. Indica un intento de introducir código malicioso desde Internet a través de una aplicación o protocolo permitido por política (HTTP, HTTPS, SMTP, FTP, SMB). El veredicto puede ser inmediato (firma conocida) o diferido (análisis en sandbox cloud). |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | WildFire log de PAN-OS — tipo `WILDFIRE`. Campos clave: `verdict` (malicious, grayware, phishing), `filename`, `filetype`, `src_ip`, `dst_ip`, `application`, `action`. El log llega a Wazuh con el veredicto final tras el análisis. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` para WildFire. Niveles orientativos: grayware → 6, phishing → 8, malicious → 12. Filtrar por `verdict = malicious` para alertas de alta prioridad. |
| **MITRE ATT&CK** | T1566 — Phishing / T1190 — Exploit Public-Facing Application (según vector) |
| **Severidad** | Alta / Crítica (según veredicto) |
| **Esfuerzo** | Bajo — built-in. Requiere licencia WildFire activa en PAN-OS y configuración del perfil WildFire en las políticas de seguridad del firewall. |
| **Falsos positivos** | Muy bajos para veredicto `malicious`. Posibles FP con `grayware` (software legítimo de administración remota, packers, etc.); revisar caso a caso. |
| **Latencia** | El análisis en sandbox puede tardar entre 5 y 15 minutos. El veredicto `malicious` inmediato indica firma conocida en la base de datos WildFire. |
| **Estado** | Pendiente de validación. |

---

#### Fichas detalladas — NET-01 (GlobalProtect VPN)

---

##### NET.01.PALO.GP.001 — Brute force contra portal/gateway GlobalProtect

| Campo | Detalle |
|---|---|
| **Descripción** | Múltiples intentos de autenticación fallidos contra el portal o gateway de GlobalProtect desde la misma IP de origen. Patrón de fuerza bruta o password spraying contra la VPN corporativa. A diferencia de NET.01.PALO.THREAT.002, este caso se detecta desde los logs de autenticación de GlobalProtect, no desde el IPS, lo que aporta contexto de usuario (qué cuenta se está atacando). |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | MEDIO |
| **Telemetría** | System log de PAN-OS — tipo `SYSTEM`, subtipo `globalprotect`. Eventos de autenticación fallida: `globalprotectgateway-auth-fail` y `globalprotectportal-auth-fail`. Campos clave: `src_ip`, `user`, `description` (motivo del fallo), `gateway` o `portal`. |
| **Ingesta en Wazuh** | Añadir el tipo `SYSTEM` al Syslog Profile de PAN-OS (si no está ya habilitado). El decoder `paloalto` de Wazuh parsea los System logs. Puede requerir decoder custom para extraer los campos específicos de GlobalProtect del campo `description`. |
| **Lógica de detección** | Regla custom de correlación: 5+ eventos `auth-fail` desde la misma `src_ip` en 120s → brute force por IP. Regla adicional: 5+ eventos `auth-fail` contra el mismo `user` desde distintas IPs en 300s → password spraying por cuenta. |
| **MITRE ATT&CK** | T1110 — Brute Force / T1110.003 — Password Spraying |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere habilitar System log en el Syslog Profile de PA y desarrollar reglas custom de correlación en Wazuh. |
| **Falsos positivos** | Bajos. Usuarios con contraseña caducada pueden generar 2-3 fallos legítimos; el umbral de 5 los absorbe. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.GP.002 — Conexión VPN desde ubicación anómala

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario se conecta a GlobalProtect desde un país o IP no habitual para esa cuenta. Indicador de compromiso de credenciales o uso no autorizado de la VPN. En clientes con MFA (Entra ID) el riesgo es menor pero no descartable (MFA bypass, adversary-in-the-middle). En clientes sin MFA, una conexión exitosa desde ubicación anómala es señal de alerta máxima. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | System log de PAN-OS — tipo `SYSTEM`, subtipo `globalprotect`. Evento de conexión exitosa: `globalprotectgateway-connected`. Campos clave: `user`, `src_ip`, `location` (país/región reportado por PA), `gateway`, timestamp. |
| **Lógica de detección** | Requiere regla custom con CDB list (lista de países/rangos IP permitidos por cliente). Dispara cuando `location` no está en la whitelist del cliente o cuando la `src_ip` pertenece a un rango de reputación baja (hosting, TOR, VPN comercial). Para impossible travel: correlación de dos eventos `connected` del mismo `user` con `src_ip` de países distintos en menos de N horas. |
| **MITRE ATT&CK** | T1078 — Valid Accounts / T1133 — External Remote Services |
| **Severidad** | Alta (sin MFA) / Media (con MFA de Entra ID) |
| **Esfuerzo** | Alto — requiere CDB list de países permitidos por cliente (distinta por cliente), integración de geolocalización IP en Wazuh y reglas custom de correlación. El impossible travel requiere además retención de estado entre eventos. |
| **Falsos positivos** | Medios. Usuarios en viaje legítimo, conexiones desde oficinas remotas no registradas. Proceso de excepción necesario. |
| **Variante sin MFA** | Conexión exitosa desde país anómalo → alerta inmediata nivel 12. Escalar a incidente y forzar reset de contraseña hasta confirmar legitimidad. |
| **Variante con MFA (Entra ID)** | Conexión exitosa desde país anómalo → alerta nivel 8. Correlacionar con Risky sign-ins de Entra ID si se tiene integración M365. El MFA reduce el riesgo pero no lo elimina (técnicas AiTM como Evilginx). |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.GP.003 — Cuenta VPN bloqueada por intentos fallidos

| Campo | Detalle |
|---|---|
| **Descripción** | GlobalProtect ha bloqueado una cuenta de usuario tras superar el umbral de intentos de autenticación fallidos. Consecuencia directa de un ataque de brute force consumado contra esa cuenta en la VPN. Complementa GP.001 (que detecta el patrón de intentos) con la confirmación del bloqueo. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | MEDIO |
| **Telemetría** | System log de PAN-OS — tipo `SYSTEM`, subtipo `globalprotect`. Evento de bloqueo: `globalprotectgateway-auth-fail` con descripción indicando lockout, o correlación con el log de autenticación del backend (AD/LDAP Event ID 4740 si el lockout ocurre en el directorio). |
| **Lógica de detección** | Dos vías paralelas: (1) Regla custom sobre System log de PA detectando el mensaje de lockout en el campo `description`. (2) Correlación con EP.02.WIN.AUTH.003 (4740 en el DC) cuando el lockout se propaga al directorio. La combinación de ambas señales en la misma ventana temporal es indicador de alta confianza. |
| **MITRE ATT&CK** | T1110 — Brute Force (resultado) |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — la vía (1) requiere decoder custom para el campo `description` de GP. La vía (2) ya está cubierta por EP.02.WIN.AUTH.003 si los DCs tienen agente Wazuh. |
| **Falsos positivos** | Muy bajos. Cualquier lockout de cuenta VPN merece investigación. |
| **Nota operativa** | En clientes sin MFA, un lockout de VPN seguido de un reset de contraseña rápido (EP.04.WIN.IDM.004) en el mismo usuario es patrón de alta sospecha de compromiso. |
| **Estado** | Pendiente de validación. |

---

#### Fichas detalladas — NET-01 (Portales web con Palo Alto)

---

##### NET.01.PALO.THREAT.003 — Ataque web conocido detectado por IPS (Palo Alto)

| Campo | Detalle |
|---|---|
| **Descripción** | El IPS de Palo Alto ha detectado un payload de ataque web conocido en tráfico HTTPS entrante hacia un portal o API expuesta: SQLi, XSS, RCE, path traversal, command injection, LFI/RFI u otras técnicas catalogadas en las firmas de Threat Prevention. El SOC debe determinar si el ataque ha llegado al backend (`action = allow`) o ha sido bloqueado. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `vulnerability` o `spyware`, categoría web-related. Campos clave: `threat_name`, `threat_id`, `severity`, `action`, `src_ip`, `dst_ip`, `dst_port` (443/80), `application` (ssl, web-browsing), `url`. |
| **Requisito previo** | SSL/TLS Decryption activo en la política de Palo Alto para el tráfico entrante hacia la aplicación. Sin decryption, el IPS no puede inspeccionar el payload HTTPS y esta ficha no aplica. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` en `0700-paloalto_rules.xml`. Niveles orientativos: medium → 7, high → 10, critical → 12. Para alertas accionables: filtrar por `dst_ip` correspondiente a la IP del portal web y subtipo `vulnerability`. Regla custom de correlación para detectar múltiples técnicas distintas desde la misma `src_ip` en ventana corta (patrón de escaneo activo con explotación). |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1059 — Command and Scripting Interpreter (según técnica) |
| **Severidad** | Alta / Crítica (según severidad del threat y acción) |
| **Esfuerzo** | Bajo para detección individual — built-in. Medio para correlación de campañas (múltiples técnicas desde misma fuente). |
| **Falsos positivos** | Bajos. Posibles FP con escáneres de vulnerabilidades autorizados (Nessus, Burp Suite en pruebas de pentesting); whitelist por IP de origen. Coordinar con el cliente los periodos de pentesting. |
| **Prioridad de investigación** | Máxima cuando `action = allow` — el payload ha llegado al backend. Revisar logs de aplicación para confirmar si ha tenido efecto. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.THREAT.004 — Reconocimiento y escaneo de aplicación web

| Campo | Detalle |
|---|---|
| **Descripción** | Una IP externa está realizando reconocimiento activo sobre el portal web: directory busting, fingerprinting de tecnologías, búsqueda de rutas sensibles (`/admin`, `/.env`, `/.git`, `/wp-admin`), o enumeración de endpoints de API. Palo Alto detecta el patrón desde el Threat log (firmas de reconocimiento) o desde el Traffic log (volumen de sesiones cortas hacia distintas rutas). Precursor habitual de NET.01.PALO.THREAT.003. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | BAJO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `vulnerability` con firmas de reconocimiento web (ej. `Web Crawlers`, `HTTP Directory Traversal Scan`). Complementariamente, Traffic log con múltiples sesiones HTTPS cortas hacia la misma `dst_ip` desde la misma `src_ip` con `bytes` bajos (respuestas 404). |
| **Requisito previo** | SSL/TLS Decryption activo para inspección del payload. Sin decryption, solo es visible el patrón de conexiones TCP (volumen y duración), no las rutas solicitadas. |
| **Lógica de detección** | Vía Threat log: reglas built-in para firmas de escaneo web. Vía Traffic log: regla custom — N sesiones HTTPS desde la misma `src_ip` hacia la misma `dst_ip` en menos de 60s con `bytes` por debajo de umbral (indicativo de respuestas de error). Umbral orientativo: 30 sesiones en 60s. |
| **MITRE ATT&CK** | T1595.003 — Active Scanning: Wordlist Scanning / T1590 — Gather Victim Network Information |
| **Severidad** | Media |
| **Esfuerzo** | Medio — la detección vía Threat log es built-in; la vía Traffic log requiere regla custom de correlación con umbral ajustado al baseline de cada aplicación. |
| **Falsos positivos** | Medios. Bots legítimos (Googlebot, monitores de disponibilidad), pentests autorizados. Whitelist de rangos de crawlers conocidos y periodos de pentesting. |
| **Relación con otros CU** | Si tras el reconocimiento se detecta NET.01.PALO.THREAT.003 desde la misma IP, la correlación de ambas alertas eleva la confianza a campaña activa. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.PALO.TRAFFIC.002 — Volumen anómalo de peticiones HTTP/S (DoS de aplicación)

| Campo | Detalle |
|---|---|
| **Descripción** | Una o varias IPs externas generan un volumen anómalo de peticiones HTTP/S contra el portal web, degradando o interrumpiendo su disponibilidad. A diferencia de un DDoS volumétrico de red (NET-10), este caso se focaliza en el agotamiento de recursos de la aplicación (HTTP flood, Slowloris, abuso de endpoints pesados). Palo Alto lo detecta desde el Traffic log y/o desde las firmas de DoS de Threat Prevention. |
| **Clasificación GrayHats** | 6.1 DoS (Denegación de servicio) / 6.2 DDoS (Denegación distribuida de servicio) |
| **Peligrosidad** | ALTO |
| **Telemetría** | Traffic log de PAN-OS — tipo `TRAFFIC`, `dst_ip` del portal, `dst_port` 443/80, volumen de sesiones por unidad de tiempo. Complementariamente Threat log subtipo `flood` si el perfil de protección DoS está activo en PA. Campos clave: `src_ip`, `bytes_sent`, `bytes_received`, `elapsed`, `packets`. |
| **Requisito previo** | Para detección vía Threat log: activar perfil de protección DoS/Zone en la política de Palo Alto. Para detección vía Traffic log: regla custom de correlación en Wazuh sobre volumen de sesiones. SSL Decryption recomendado pero no estrictamente necesario para este caso (el patrón es volumétrico, no depende del payload). |
| **Lógica de detección** | Vía Threat log: regla built-in para subtipo `flood` del grupo `paloalto`. Vía Traffic log: regla custom — N sesiones desde la misma `src_ip` hacia `dst_ip` del portal en ventana de 30s supera umbral definido por baseline del cliente. Para DoS distribuido: N sesiones desde IPs distintas hacia el mismo destino supera umbral global. |
| **MITRE ATT&CK** | T1499 — Endpoint Denial of Service / T1499.002 — Service Exhaustion Flood |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — la vía Threat log requiere activar el perfil DoS en PA. La vía Traffic log requiere establecer un baseline de tráfico normal por aplicación y ajustar umbrales. |
| **Falsos positivos** | Medios. Picos de tráfico legítimos (campañas de marketing, lanzamientos de producto). El baseline por aplicación es esencial para reducirlos. |
| **Nota operativa** | Si el volumen proviene de muchas IPs distintas con ASNs de hosting o CDN (patrón DDoS), escalar a proveedor de conectividad o servicio anti-DDoS. Palo Alto solo puede mitigar a nivel de política local. |
| **Estado** | Pendiente de validación. |

---

#### Fichas detalladas — NET-01 (Servicios expuestos a Internet sin firewall)

---

##### NET.01.WIN.RDP.001 — Brute force contra RDP expuesto a Internet

| Campo | Detalle |
|---|---|
| **Descripción** | Múltiples intentos de autenticación fallidos contra el servicio RDP (puerto 3389) de un sistema Windows expuesto directamente a Internet sin firewall perimetral. Uno de los vectores de ataque más frecuentes en la actualidad. Sin protección perimetral, el sistema está recibiendo el tráfico malicioso directamente. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 9.3 Servicios con acceso potencial no deseado |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Canal Security — Event ID 4625 (An account failed to log on) con LogonType 3 o 10 y `ipAddress` externa. Event ID 4624 (LogonType 10) para detectar conexiones RDP exitosas desde IPs externas sospechosas. |
| **Lógica de detección** | Regla built-in 60122 (fallo individual, nivel 5) + 60204 (correlación 8 fallos en 240s, nivel 10). Regla custom adicional recomendada: login RDP exitoso (4624 LogonType 10) desde IP pública → nivel 8 (acceso remoto externo consumado). |
| **MITRE ATT&CK** | T1110 — Brute Force / T1133 — External Remote Services |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in para brute force. Medio para detección de login exitoso externo (regla custom). |
| **Falsos positivos** | Bajos. RDP desde Internet es anómalo en entornos corporativos gestionados. |
| **Recomendación de hardening** | Exponer RDP directamente a Internet es una práctica de alto riesgo. Recomendación inmediata al cliente: restringir el acceso a través de GlobalProtect VPN o al menos limitarlo por IP de origen en el host (Windows Firewall). Considerar NLA (Network Level Authentication) obligatorio. |
| **Relación con otros CU** | Si el brute force tiene éxito, correlacionar con EP.08.WIN.AUTH.004 (login interactivo privilegiado) y EP.03.WIN.PERS.* (persistencia post-compromiso). |
| **Estado** | Pendiente de validación. |

---

##### NET.01.LNX.SSH.001 — Brute force contra SSH expuesto a Internet

| Campo | Detalle |
|---|---|
| **Descripción** | Múltiples intentos de autenticación fallidos contra el servicio SSH (puerto 22) de un sistema Linux expuesto directamente a Internet. SSH expuesto a Internet recibe ataques de fuerza bruta automatizados de forma prácticamente continua desde bots y scanners globales. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 9.3 Servicios con acceso potencial no deseado |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Fichero `/var/log/auth.log` (Debian/Ubuntu) o `/var/log/secure` (RHEL/CentOS). Mensajes del tipo `Failed password for`, `Invalid user`, `Connection closed by authenticating user`. El agente Wazuh monitoriza estos ficheros con `<localfile>`. |
| **Lógica de detección** | Reglas built-in del grupo `syslog,sshd`: 5710 (Invalid user, nivel 5), 5712 (Too many auth failures, nivel 8), 5720 (Multiple auth failures, nivel 10). Regla custom recomendada: login SSH exitoso desde IP pública con usuario no habitual → nivel 10. |
| **MITRE ATT&CK** | T1110 — Brute Force / T1133 — External Remote Services |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. Requiere que el agente tenga configurado el `localfile` apuntando al log de autenticación correcto según la distro. |
| **Falsos positivos** | Muy bajos para correlación de múltiples fallos. El volumen de alertas individuales (5710) puede ser alto en sistemas muy expuestos; filtrar por umbral de correlación. |
| **Recomendación de hardening** | Deshabilitar autenticación por contraseña (solo clave pública). Cambiar el puerto por defecto. Implementar fail2ban. Restringir el acceso vía GlobalProtect VPN. |
| **Relación con otros CU** | Login SSH exitoso desde IP externa desconocida → escalar a incidente. Correlacionar con creación de usuarios, modificación de `authorized_keys` o instalación de servicios (persistencia en Linux, pendiente de Fase 2). |
| **Estado** | Pendiente de validación. |

---

##### NET.01.WIN.SMB.001 — Intentos de acceso SMB expuesto a Internet

| Campo | Detalle |
|---|---|
| **Descripción** | Intentos de autenticación o acceso a recursos compartidos SMB (puertos 445/139) desde IPs externas en un sistema Windows expuesto a Internet. SMB expuesto a Internet es un vector de ataque crítico asociado a ransomware (WannaCry, NotPetya) y movimiento lateral. Su exposición directa es una vulnerabilidad grave. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 9.3 Servicios con acceso potencial no deseado |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Canal Security — Event ID 4625 (fallo de autenticación con LogonType 3, red), Event ID 5140 (acceso a recurso compartido de red), Event ID 5145 (acceso a fichero/carpeta compartida con detalle). |
| **Lógica de detección** | Regla built-in 60122 + 60204 (brute force, igual que RDP). Regla custom adicional: Event ID 5140 con `IpAddress` externa → nivel 10 (acceso a share desde Internet). Regla de alta prioridad: cualquier conexión SMB exitosa desde IP pública → nivel 12. |
| **MITRE ATT&CK** | T1110 — Brute Force / T1021.002 — SMB/Windows Admin Shares / T1190 — Exploit Public-Facing Application |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo para brute force (built-in). Medio para detección de acceso a shares desde Internet (regla custom). |
| **Falsos positivos** | Prácticamente nulos. SMB desde Internet nunca es tráfico legítimo en entornos corporativos. |
| **Recomendación de hardening** | Bloquear puertos 445 y 139 a Internet de forma inmediata es una acción prioritaria. No existe justificación operativa para tener SMB expuesto a Internet. Escalar al cliente como riesgo crítico. |
| **Relación con otros CU** | Correlacionar con NET.01.WIN.RDP.001 — un atacante que prueba SMB y RDP simultáneamente está realizando reconocimiento activo del sistema. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.WIN.FTP.001 — Brute force contra FTP expuesto a Internet (IIS)

| Campo | Detalle |
|---|---|
| **Descripción** | Múltiples intentos de autenticación fallidos contra el servicio FTP de IIS expuesto a Internet. FTP transmite credenciales en texto claro y es un servicio obsoleto con múltiples vulnerabilidades conocidas. Su exposición directa a Internet es un riesgo alto. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 9.3 Servicios con acceso potencial no deseado |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Log de IIS FTP en `%SystemDrive%\inetpub\logs\LogFiles\FTPSVC*`. Campos clave: `cs-username`, `c-ip`, `sc-status` (530 = autenticación fallida, 230 = login exitoso), `cs-method`. Monitorizado por el agente Wazuh via `<localfile>` con `log_format iis`. |
| **Lógica de detección** | Reglas built-in del grupo `ms-ftp` en Wazuh: 11804 (fallo de autenticación FTP, nivel 5), 11805 (múltiples fallos, nivel 10). Regla custom: login FTP exitoso (`sc-status = 230`) desde IP externa → nivel 10. |
| **MITRE ATT&CK** | T1110 — Brute Force / T1133 — External Remote Services |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. Requiere configurar el `localfile` apuntando al directorio de logs de IIS FTP. |
| **Falsos positivos** | Bajos para correlación de múltiples fallos. Evaluar si el FTP tiene uso legítimo: si no, recomendación de desactivación inmediata. |
| **Recomendación de hardening** | Reemplazar FTP por SFTP o FTPS. Si el servicio no tiene uso activo, desactivarlo. Si debe mantenerse, restringir acceso por IP de origen. Nunca exponer FTP sin cifrado a Internet. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.WIN.DOTNET.001 — Intentos de explotación de .NET Remoting expuesto a Internet

| Campo | Detalle |
|---|---|
| **Descripción** | El endpoint TCP de .NET Remoting está expuesto directamente a Internet. .NET Remoting es una tecnología legacy (deprecada desde .NET Framework 4.0) con vulnerabilidades de deserialización graves y conocidas (CVE-2014-1806, CVE-2017-8759 entre otras). Su exposición a Internet es un riesgo crítico: cualquier atacante que encuentre el puerto abierto puede intentar deserialización maliciosa sin necesidad de credenciales. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 9.5 Sistema vulnerable |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Tres fuentes combinadas: (1) Event log de Aplicación de Windows — errores de deserialización o excepciones no controladas del proceso que aloja el endpoint Remoting. (2) FIM (EP.09.WIN.FIM.001) — cambios en los binarios o configuración del servicio. (3) Event ID 4625/4624 si el endpoint tiene autenticación Windows. Opcionalmente: logs del proceso de la aplicación si escribe en fichero monitorizado por Wazuh. |
| **Lógica de detección** | No existe regla built-in específica para .NET Remoting. Requiere: (1) Regla custom sobre el Event log de Aplicación filtrando excepciones de deserialización (`System.Runtime.Serialization`, `BinaryFormatter`). (2) Regla custom sobre FIM para detectar modificación de ficheros del servicio (indicador de compromiso post-explotación). (3) Correlación: excepción de deserialización + modificación de fichero en ventana corta → nivel 12 (posible explotación exitosa). |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1059.005 — Visual Basic / T1203 — Exploitation for Client Execution |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — requiere conocer la aplicación concreta, identificar los logs que genera y desarrollar reglas custom específicas. La cobertura es limitada sin instrumentación adicional de la aplicación. |
| **Falsos positivos** | Bajos para correlación deserialización + FIM. Las excepciones individuales pueden ser operativas (FP medios). |
| **Recomendación de hardening** | Migrar a WCF o gRPC de forma urgente. Mientras no sea posible: restringir el acceso al endpoint por IP de origen (whitelist estricta), no exponer a Internet bajo ningún concepto, deshabilitar `BinaryFormatter` si la versión de .NET lo permite, aplicar `SerializationBinder` personalizado. Escalar al cliente como riesgo crítico inmediato. |
| **Nota operativa** | La presencia de .NET Remoting expuesto a Internet debe tratarse como un hallazgo de seguridad independiente y comunicarse al cliente con urgencia, independientemente de si hay alertas activas. |
| **Estado** | Pendiente de validación. |

---

#### Fichas detalladas — NET-01 (Ataques de fuerza bruta desde Internet)

---

##### NET.01.WIN.PANEL.001 — Brute force contra panel de administración web expuesto

| Campo | Detalle |
|---|---|
| **Descripción** | Múltiples intentos de autenticación fallidos contra un panel de administración web expuesto a Internet (cPanel, Plesk, phpMyAdmin u otros). Estos paneles ofrecen control total sobre el hosting, bases de datos o el servidor web, por lo que su compromiso tiene impacto crítico. La detección se realiza desde los logs de acceso del servidor web subyacente. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 9.3 Servicios con acceso potencial no deseado |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Logs de acceso Apache (`/var/log/apache2/access.log`) o Nginx (`/var/log/nginx/access.log`). Indicadores de brute force: múltiples peticiones POST hacia rutas de login del panel (`/login`, `/cpanel`, `/plesk`, `/phpmyadmin/index.php`) con código de respuesta HTTP 401, 403 o 200 (login exitoso tras fallos). Campos clave: `client_ip`, `request_uri`, `status_code`, `timestamp`. |
| **Ingesta en Wazuh** | `<localfile>` en el agente con `log_format apache` o `log_format nginx` apuntando al access.log correspondiente. |
| **Lógica de detección** | Reglas built-in de Wazuh para Apache/Nginx: 30105 (múltiples códigos 401 desde misma IP, nivel 10), 31151 (Nginx auth failures). Reglas custom recomendadas por panel: (1) N peticiones POST a `/cpanel` o `/login` con status 401/403 desde misma IP en 60s → nivel 10. (2) Petición POST a ruta de login con status 200 precedida de fallos → nivel 12 (login exitoso tras brute force). Adaptar las rutas según el panel del cliente. |
| **MITRE ATT&CK** | T1110 — Brute Force / T1190 — Exploit Public-Facing Application |
| **Severidad** | Alta / Crítica (login exitoso) |
| **Esfuerzo** | Medio — las reglas built-in cubren el patrón genérico; las rutas específicas de cada panel requieren reglas custom por cliente. La heterogeneidad de paneles (cPanel vs Plesk vs phpMyAdmin) implica múltiples variantes de rutas. |
| **Falsos positivos** | Bajos para correlación de múltiples fallos. El login exitoso tras fallos es prácticamente siempre sospechoso. |
| **Recomendación de hardening** | Restringir el acceso al panel por IP de origen (whitelist). Habilitar 2FA en el panel si lo soporta. Cambiar el puerto o la URL por defecto. Nunca exponer phpMyAdmin directamente a Internet — considerar acceso solo desde localhost con túnel SSH. |
| **Nota operativa** | phpMyAdmin expuesto a Internet sin autenticación adicional es un hallazgo crítico independiente — comunicar al cliente de forma inmediata. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.API.001 — Credential stuffing / brute force contra API sin WAF

| Campo | Detalle |
|---|---|
| **Descripción** | Una IP o conjunto de IPs realizan múltiples intentos de autenticación fallidos contra endpoints de autenticación de una API expuesta a Internet sin WAF delante (endpoints tipo `/auth`, `/login`, `/token`, `/oauth/token`, `/api/v*/auth`). Patrón de credential stuffing (uso de credenciales robadas) o brute force automatizado. Sin WAF, la única fuente de detección es el log de acceso del servidor web. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 8.4 Phishing |
| **Peligrosidad** | ALTO |
| **Telemetría** | Logs de acceso Apache o Nginx del servidor que aloja la API. Indicadores: múltiples peticiones POST al endpoint de autenticación con status 401 o 403 desde la misma IP o rango de IPs. Para credential stuffing distribuido: múltiples IPs distintas con bajo volumen individual pero alto volumen agregado hacia el mismo endpoint. Campos clave: `client_ip`, `request_uri`, `status_code`, `request_method`, `response_body_size`. |
| **Ingesta en Wazuh** | `<localfile>` con `log_format apache` o `log_format nginx`. Recomendado activar el log de errores además del access log para capturar contexto adicional. |
| **Lógica de detección** | Regla custom — N peticiones POST al endpoint `/auth` (o equivalente) con status 401/403 desde la misma `client_ip` en 60s → nivel 10 (brute force por IP). Regla adicional para credential stuffing distribuido: N peticiones POST al mismo endpoint desde IPs distintas en 300s superando umbral agregado → nivel 10. Regla crítica: petición POST al endpoint de autenticación con status 200 precedida de 3+ fallos desde la misma IP en 300s → nivel 12 (credencial válida encontrada). |
| **MITRE ATT&CK** | T1110.004 — Credential Stuffing / T1110.001 — Password Guessing / T1133 — External Remote Services |
| **Severidad** | Alta / Crítica (credencial válida encontrada) |
| **Esfuerzo** | Medio — requiere identificar los endpoints de autenticación de cada API cliente y crear reglas custom con las rutas específicas. La detección de credential stuffing distribuido requiere correlación multi-IP con estado en Wazuh. |
| **Falsos positivos** | Medios para detección por IP individual (clientes con reintentos agresivos, integraciones con errores). Muy bajos para la regla de credencial válida tras fallos. |
| **Recomendación de hardening** | Implementar rate limiting en el servidor web o en la propia API. Añadir CAPTCHA o MFA en el endpoint de autenticación. Desplegar Imperva WAF (WAF.01.IMPERVA.API.*) para cobertura completa. Implementar detección de credential stuffing en la capa de aplicación. |
| **Nota operativa** | Si el endpoint `/token` usa OAuth 2.0 con `grant_type=password`, es especialmente vulnerable a credential stuffing ya que devuelve tokens de larga duración. Priorizar la protección de estos endpoints. |
| **Estado** | Pendiente de validación. |

---

##### NET.01.XSVC.001 — Correlación transversal: mismo atacante contra múltiples servicios

| Campo | Detalle |
|---|---|
| **Descripción** | Una misma IP de origen genera intentos de autenticación fallidos o ataques contra múltiples servicios distintos en un mismo cliente en una ventana de tiempo: RDP + SSH + panel web + API + VPN. Patrón de reconocimiento activo y ataque multi-vector. La correlación transversal eleva significativamente la confianza respecto a alertas individuales y permite identificar campañas organizadas contra un cliente concreto. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales / 4.1 Explotación de vulnerabilidades conocidas / 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Correlación de alertas ya generadas por: NET.01.WIN.RDP.001, NET.01.LNX.SSH.001, NET.01.WIN.SMB.001, NET.01.WIN.FTP.001, NET.01.PALO.GP.001, NET.01.WIN.PANEL.001, NET.01.API.001, NET.01.PALO.THREAT.002. Todas comparten el campo `src_ip` / `client_ip` / `waf.src` como elemento correlador. |
| **Lógica de detección** | Regla custom de correlación de segundo nivel en Wazuh: 2+ alertas de distintos grupos (`paloalto`, `sshd`, `ms-ftp`, `imperva-waf`, `apache`, `windows_security`) con el mismo `src_ip` en ventana de 600s → nivel 12 (campaña multi-servicio activa). Requiere normalización del campo IP de origen entre los distintos decoders — considerar usar un campo normalizado común en los decoders custom. |
| **MITRE ATT&CK** | T1110 — Brute Force / T1595 — Active Reconnaissance / T1190 — Exploit Public-Facing Application |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — es una detección de tercer nivel que depende de que todas las reglas base estén operativas y de que los campos IP estén normalizados entre fuentes heterogéneas. La normalización de `src_ip` entre Wazuh, Palo Alto, Imperva y logs Apache/Nginx es el principal reto técnico. |
| **Falsos positivos** | Muy bajos. La coincidencia de IP atacante en múltiples servicios simultáneamente es altamente indicativa de actividad maliciosa organizada. Posible FP con escáneres de seguridad autorizados — whitelist de IPs de pentesting. |
| **Nota operativa** | Cuando dispara esta regla, notificar al cliente de forma inmediata y considerar el bloqueo proactivo de la IP en todos los servicios. Documentar la IP en la CDB list de IPs maliciosas del cliente para enriquecer futuras correlaciones. |
| **Prerequisito** | Normalización del campo IP de origen entre todos los decoders implicados. Recomendado como tarea de arquitectura antes de activar esta regla. |
| **Estado** | Pendiente de validación. |

---

### NET-02 — Comunicaciones con infraestructura maliciosa

> ¿Algún activo interno se está comunicando con infraestructura maliciosa o sospechosa?

- Conexiones a IPs o dominios maliciosos
- Comunicación con C2
- Tráfico hacia botnets
- Conexiones a nodos TOR o proxies anónimos
- Tráfico hacia dominios recientemente creados

#### Fichas detalladas — NET-02 (Conexiones a IPs o dominios maliciosos)

---

##### NET.02.PALO.001 — Conexión a IP o dominio malicioso detectada por Palo Alto

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno ha iniciado o recibido una conexión hacia/desde una IP o dominio clasificado como malicioso por las fuentes de inteligencia integradas en Palo Alto: PAN-DB (base de datos de URLs y dominios), DNS Security (resoluciones DNS hacia dominios maliciosos, C2, DGA, phishing) o las firmas de spyware del módulo Threat Prevention (comunicaciones C2 conocidas). Indicador de posible compromiso del activo interno. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Tres fuentes complementarias: (1) Threat log — tipo `THREAT`, subtipo `spyware`, categorías `command-and-control`, `malware`, `phishing`. Campos clave: `threat_name`, `src_ip` (activo interno), `dst_ip`, `dst_fqdn`, `action`, `app`. (2) Threat log — subtipo `dns` cuando DNS Security bloquea o detecta una resolución maliciosa. Campos clave: `dns_query`, `dns_category`, `action`. (3) URL Filtering log — tipo `THREAT`, subtipo `url`, categorías `malware`, `command-and-control`, `phishing`. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` para subtipos `spyware` y `url`. Niveles orientativos por severidad: medium → 7, high → 10, critical → 12. Reglas custom recomendadas: (1) `THREAT/spyware` con categoría `command-and-control` desde IP interna → nivel 12 (indicador de compromiso activo). (2) `THREAT/dns` con `dns_category = malware` o `c2` → nivel 10. (3) Correlación: mismo `src_ip` interno con múltiples conexiones a distintas IPs maliciosas en 300s → nivel 12 (activo comprometido con C2 activo). |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1071.004 — DNS / T1048 — Exfiltration Over Alternative Protocol / T1041 — Exfiltration Over C2 Channel |
| **Severidad** | Alta / Crítica |
| **Esfuerzo** | Bajo — la detección individual es built-in una vez configurados los perfiles de Threat Prevention, DNS Security y URL Filtering en las políticas de PA. La correlación multi-conexión requiere regla custom. |
| **Falsos positivos** | Bajos para categorías `command-and-control` y `malware`. Medios para `phishing` (usuarios que hacen clic en enlaces en correos). PAN-DB puede tener falsos positivos en dominios recién categorizados — proceso de excepción necesario. |
| **Prioridad de investigación** | Máxima cuando `action = allow` — la conexión se ha establecido. El activo interno debe aislarse y analizarse. Media cuando `action = block` o `reset-both` — Palo Alto ha bloqueado la comunicación pero el activo puede estar comprometido. |
| **Relación con otros CU** | Correlacionar con EP-03 (persistencia) y EP-10 (evasión defensiva) en el endpoint origen — si hay C2 activo, el atacante probablemente ya ha establecido persistencia. |
| **Estado** | Pendiente de validación. |

---

##### NET.02.NOWAF.001 — Conexión a IP o dominio malicioso sin firewall (solo Wazuh)

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno sin firewall perimetral ni protección DNS se comunica con una IP o dominio malicioso. Sin Palo Alto ni DNS Security, la detección depende exclusivamente de la telemetría disponible en el propio endpoint vía agente Wazuh: logs de conexiones de red del sistema operativo, resoluciones DNS locales o logs de aplicación. La cobertura es significativamente más limitada que con Palo Alto. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Varias fuentes posibles según el sistema: (1) **Windows — Sysmon (Fase 2)**: Event ID 3 (Network connection) y Event ID 22 (DNS query). Requiere Sysmon desplegado — no disponible en Fase 1. (2) **Windows — Fase 1**: sin telemetría de red nativa; cobertura muy limitada. (3) **Linux**: `/var/log/syslog` o logs de aplicación si el proceso registra conexiones salientes. (4) **Wazuh CDB list**: comparación de IPs de destino contra lista de IPs maliciosas conocidas — requiere construir y mantener la lista. |
| **Lógica de detección** | **Sin feeds de TI en Wazuh (situación actual):** cobertura prácticamente nula en Fase 1 Windows. En Linux, detección oportunista desde logs de aplicación si existen. **Con feeds de TI integrados (situación objetivo):** CDB list de IPs/dominios maliciosos actualizada periódicamente (feeds OSINT: AbuseIPDB, Feodo Tracker, URLhaus, MISP) + regla custom que compara el campo de IP de destino en cualquier log contra la CDB list → nivel 10 cuando hay match. Regla adicional: resolución DNS de dominio malicioso en log de sistema → nivel 10. |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1071.004 — DNS / T1041 — Exfiltration Over C2 Channel |
| **Severidad** | Crítica (cuando se detecta) |
| **Esfuerzo** | Alto — en Fase 1 Windows la cobertura es prácticamente nula sin Sysmon ni feeds de TI. Construir capacidad de detección real requiere: (1) Desplegar Sysmon (Fase 2). (2) Integrar feeds de TI en Wazuh como CDB lists con actualización automática. (3) Desarrollar reglas custom de correlación IP/dominio. |
| **Falsos positivos** | Dependen de la calidad del feed de TI utilizado. Feeds OSINT públicos tienen tasa de FP más alta que PAN-DB — proceso de validación y excepción necesario. |
| **Brecha de cobertura** | Esta ficha documenta una brecha de seguridad real: sistemas sin firewall perimetral ni DNS Security tienen visibilidad mínima de comunicaciones con infraestructura maliciosa. Se recomienda priorizar para estos clientes: (1) Despliegue de Sysmon (Fase 2). (2) Integración de feeds OSINT en Wazuh. (3) A medio plazo, despliegue de DNS resolver con filtrado (ej. Quad9, Cloudflare Gateway). |
| **Recomendación de hardening** | Desplegar un resolver DNS con filtrado de dominios maliciosos (Cloudflare Gateway, Quad9, Cisco Umbrella) como medida inmediata de bajo coste que no requiere cambios en la arquitectura de red. Esto aporta cobertura de dominios maliciosos sin necesidad de Palo Alto ni Sysmon. |
| **Estado** | Pendiente de validación. Cobertura real en Fase 1: muy baja. Cobertura objetivo con Sysmon + feeds TI: media. |

---

#### Fichas detalladas — NET-02 (Comunicación con C2)

---

##### NET.02.PALO.C2.001 — C2 conocido detectado por firmas Palo Alto

| Campo | Detalle |
|---|---|
| **Descripción** | Palo Alto ha identificado comunicación saliente desde un activo interno hacia infraestructura de Command & Control conocida mediante las firmas de spyware/C2 del módulo Threat Prevention. La firma identifica el protocolo o patrón de comunicación específico del framework C2 (Cobalt Strike, Metasploit, njRAT, AsyncRAT, etc.). Indicador de compromiso activo — el endpoint está bajo control de un atacante. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `spyware`, categoría `command-and-control`. Campos clave: `threat_name` (nombre del framework C2), `src_ip` (activo comprometido), `dst_ip`, `dst_port`, `application`, `action`, `severity`. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` para subtipo `spyware/command-and-control`. Niveles orientativos: high → 10, critical → 12. Regla custom recomendada: `action = allow` con categoría `command-and-control` → nivel 12 + alerta inmediata (la sesión C2 está activa). Correlación: mismo `src_ip` con múltiples eventos C2 en 300s → nivel 12 (beaconing activo). |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1095 — Non-Application Layer Protocol / T1571 — Non-Standard Port |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — built-in una vez activado el perfil de Threat Prevention con categoría C2 habilitada. |
| **Falsos positivos** | Muy bajos. Las firmas de C2 son altamente específicas. Posibles FP con software legítimo de administración remota (TeamViewer, AnyDesk) si no están en whitelist. |
| **Prioridad de investigación** | Máxima siempre. Aislar el endpoint de forma inmediata si `action = allow`. Si `action = block`, el endpoint sigue comprometido aunque la sesión C2 esté cortada — investigar persistencia. |
| **Relación con otros CU** | Correlacionar con EP.03.WIN.PERS.* (persistencia) y EP.10.WIN.AV.001 (Defender manipulado) en el endpoint origen. Un C2 activo implica que el atacante ya ha establecido acceso. |
| **Estado** | Pendiente de validación. |

---

##### NET.02.PALO.C2.002 — C2 sobre HTTPS detectado con SSL Decryption (Palo Alto)

| Campo | Detalle |
|---|---|
| **Descripción** | Con SSL Decryption activo en el tráfico saliente, Palo Alto puede inspeccionar el payload de conexiones HTTPS y detectar tráfico C2 que usa HTTPS como canal de evasión — técnica habitual en frameworks modernos (Cobalt Strike HTTPS listener, Sliver, Havoc). Sin decryption esta ficha no aplica y el C2 sobre HTTPS es invisible al firewall. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `spyware` o `vulnerability`, categoría `command-and-control`, sobre tráfico `application = ssl` o `application = web-browsing` con decryption activo. Complementariamente URL Filtering log con categoría `command-and-control` o `malware` sobre HTTPS. Campos clave: `src_ip`, `dst_ip`, `dst_fqdn`, `url`, `threat_name`, `action`. |
| **Lógica de detección** | Mismas reglas built-in que NET.02.PALO.C2.001 pero sobre tráfico HTTPS decifrado. Regla custom adicional: destino HTTPS con JA3/JA4 hash conocido de framework C2 (Cobalt Strike default JA3: `72a7c9febc3d4bfedd63f4be90e94898`) → nivel 12. Requiere activar el log de JA3 en el perfil de decryption. |
| **MITRE ATT&CK** | T1071.001 — Web Protocols / T1573 — Encrypted Channel / T1573.001 — Symmetric Cryptography |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — la detección es built-in pero requiere SSL Decryption activo en tráfico saliente, lo que implica desplegar certificados en los endpoints y gestionar excepciones (banca, healthcare). Solo aplica en clientes con decryption configurado. |
| **Falsos positivos** | Bajos con firmas de C2. Medios con detección por JA3 (algunos clientes legítimos comparten JA3 con herramientas C2). |
| **Prerequisito** | SSL/TLS Decryption activo en política de tráfico saliente en Palo Alto. Sin este requisito, esta ficha no aporta cobertura adicional sobre NET.02.PALO.C2.001. |
| **Nota operativa** | En clientes sin SSL Decryption saliente, documentar como brecha de cobertura explícita — el C2 sobre HTTPS es prácticamente indetectable a nivel de red sin esta capacidad. |
| **Estado** | Pendiente de validación. Aplica solo en clientes con SSL Decryption saliente activo. |

---

##### NET.02.PALO.C2.003 — Consulta DNS a dominio C2 o DGA detectada por DNS Security

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno ha realizado una consulta DNS hacia un dominio clasificado como C2, malware o generado algorítmicamente (DGA) por el motor de DNS Security de Palo Alto. El canal DNS es frecuentemente usado por malware para resolver el dominio del servidor C2 antes de establecer la conexión, y también como canal de comunicación encubierto (DNS tunneling). La detección a nivel DNS es anterior a la conexión y complementa NET.02.PALO.C2.001. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `dns`, generado por DNS Security. Campos clave: `dns_query` (dominio consultado), `dns_category` (malware, c2, phishing, DGA), `src_ip` (activo que resuelve), `action` (sinkhole, block, alert), `threat_name`. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` para subtipo `dns`. Niveles orientativos: `dns_category = command-and-control` → nivel 10-12, `dns_category = malware` → nivel 8-10, `dns_category = dga` → nivel 8. Regla custom: misma `src_ip` resolviendo múltiples dominios de categoría C2/DGA en 300s → nivel 12 (patrón de beaconing DNS o DGA activo). |
| **MITRE ATT&CK** | T1071.004 — DNS / T1568.002 — Domain Generation Algorithms / T1090 — Proxy |
| **Severidad** | Alta / Crítica |
| **Esfuerzo** | Bajo — built-in con DNS Security activo. Requiere configurar la acción DNS Security en modo `sinkhole` o `block` (no solo `alert`) para mayor efectividad. |
| **Falsos positivos** | Bajos para categorías C2 y DGA. Medios para dominios recién registrados que no son maliciosos. DNS Security puede generar FP en dominios legítimos recién creados — proceso de excepción necesario. |
| **Ventaja sobre NET.02.PALO.C2.001** | Detecta la intención de conectar con C2 antes de que se establezca la sesión TCP, incluso si el firewall bloquea después la conexión. Útil para detectar malware que aún no ha conseguido comunicarse con su C2. |
| **Relación con otros CU** | Si hay consulta DNS a C2 (esta ficha) pero no hay Threat log de sesión C2 (NET.02.PALO.C2.001), el firewall está cortando la conexión pero el endpoint sigue comprometido. Ambas señales juntas confirman compromiso activo. |
| **Estado** | Pendiente de validación. |

---

##### NET.02.EP.C2.001 — Proceso sospechoso con conexión C2 detectado por Sysmon

| Campo | Detalle |
|---|---|
| **Descripción** | Sysmon ha registrado una conexión de red saliente desde un proceso sospechoso en el endpoint hacia una IP o dominio externo. A diferencia de las fichas de red (que ven el tráfico pero no el proceso), Sysmon correlaciona directamente proceso → conexión → destino, lo que permite identificar qué binario está generando el tráfico C2. Especialmente útil para detectar C2 sobre puertos legítimos (443, 80, 53) desde procesos anómalos (Word, Excel, PowerShell, cmd). |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 3 (Network connection) — campos clave: `Image` (proceso que inicia la conexión), `DestinationIp`, `DestinationPort`, `DestinationHostname`, `Protocol`, `Initiated` = true. Sysmon Event ID 22 (DNS query) — campos clave: `Image`, `QueryName`, `QueryResults`. Ambos llegan al manager Wazuh vía el canal `Microsoft-Windows-Sysmon/Operational`. |
| **Ingesta en Wazuh** | Canal `Microsoft-Windows-Sysmon/Operational` en `agent.conf`. Requiere Sysmon desplegado con configuración que incluya reglas de red (SwiftOnSecurity o equivalente). El ruleset comunitario socfortress/Wazuh-Rules incluye reglas para Sysmon Event ID 3 y 22. |
| **Lógica de detección** | Reglas custom de correlación de alto valor: (1) Event ID 3 con `Image` = proceso Office (winword.exe, excel.exe, powerpnt.exe) y `DestinationPort` = 443/80 → nivel 12 (Office estableciendo conexión saliente — phishing con macro activo). (2) Event ID 3 con `Image` = intérprete (powershell.exe, cmd.exe, wscript.exe, mshta.exe) y destino IP pública → nivel 12. (3) Event ID 22 con `QueryName` de alta entropía (DGA) desde cualquier proceso → nivel 10. (4) Correlación Event ID 22 (DNS query) + Event ID 3 (conexión) al mismo destino desde mismo proceso en 5s → nivel 12 (resolución + conexión C2 confirmada). |
| **MITRE ATT&CK** | T1071.001 — Web Protocols / T1071.004 — DNS / T1059 — Command and Scripting Interpreter / T1566.001 — Spearphishing Attachment |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — requiere Sysmon desplegado (Fase 2), configuración adecuada del ruleset Sysmon, y reglas custom de correlación proceso-conexión. El volumen de Event ID 3 puede ser alto; el filtrado por procesos de interés es esencial para evitar ruido. |
| **Falsos positivos** | Medios para reglas individuales (muchos procesos legítimos hacen conexiones salientes). Muy bajos para las correlaciones específicas (Office → conexión saliente, intérprete → IP pública). |
| **Prerequisito** | Sysmon desplegado en Fase 2. No disponible en Fase 1. |
| **Ventaja sobre fichas de red** | Es la única ficha que identifica el proceso responsable del C2, no solo el flujo de red. Esencial para la investigación forense — permite saber exactamente qué binario fue comprometido. |
| **Relación con otros CU** | Correlacionar con EP.03.WIN.PERS.* — si hay C2 activo desde un proceso hay que buscar el mecanismo de persistencia que lo relanza. También correlacionar con NET.02.PALO.C2.003 (DNS query) para confirmar el dominio C2 desde la capa de red. |
| **Estado** | Pendiente de validación. Aplica solo en endpoints con Sysmon desplegado (Fase 2). |

---

#### Fichas detalladas — NET-02 (Tráfico hacia botnets)

---

##### NET.02.PALO.BOT.001 — Comunicación con infraestructura de botnet (Palo Alto)

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno se está comunicando con infraestructura conocida de una botnet — servidores C2 de redes de bots como Emotet, QakBot, TrickBot, Mirai o similares. Palo Alto lo detecta mediante firmas específicas de botnet en el módulo Threat Prevention o por categorización de la IP/dominio destino como botnet en PAN-DB. Indicador de compromiso activo: el endpoint puede estar siendo usado para spam, DDoS distribuido, minería o movimiento lateral. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Threat log de PAN-OS — tipo `THREAT`, subtipo `spyware`, categoría `botnet`. Complementariamente URL Filtering log con categoría `malware` o `botnet` si el C2 usa HTTP/S. DNS Security log con `dns_category = malware` para resoluciones DNS de dominios de botnet. Campos clave: `threat_name`, `src_ip` (bot comprometido), `dst_ip`, `action`. |
| **Lógica de detección** | Reglas built-in del grupo `paloalto` para subtipo `spyware/botnet`. Niveles orientativos: high → 10, critical → 12. Regla custom: `action = allow` con categoría `botnet` → nivel 12 (comunicación activa con C2 de botnet). Correlación: múltiples eventos de botnet desde el mismo `src_ip` en 300s → nivel 12 + alerta de aislamiento inmediato. |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1583.005 — Botnet / T1584.005 — Botnet |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — built-in con Threat Prevention activo. Las firmas de botnet son parte del perfil de seguridad estándar de PA. |
| **Falsos positivos** | Muy bajos. Las firmas de botnet son altamente específicas. |
| **Nota operativa** | A diferencia del C2 genérico, un endpoint en botnet puede estar generando tráfico malicioso hacia terceros (spam, DDoS) además de recibir comandos. Investigar también el tráfico saliente del endpoint hacia otros destinos. |
| **Relación con otros CU** | Correlacionar con NET.02.PALO.C2.001 — botnets y C2 comparten infraestructura. Si dispara esta ficha y la de C2 simultáneamente desde el mismo endpoint, la confianza de compromiso es máxima. |
| **Estado** | Pendiente de validación. |

---

##### NET.02.NOWAF.BOT.001 — Comunicación con botnet sin firewall (solo Wazuh)

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo sin Palo Alto se comunica con infraestructura de botnet. Sin firewall con Threat Prevention, la detección depende de feeds de TI en Wazuh (CDB lists de IPs/dominios de botnets conocidas) o de telemetría de endpoint con Sysmon. La cobertura es significativamente más limitada. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | (1) Wazuh CDB list con IPs/dominios de botnets conocidas (Feodo Tracker, Abuse.ch, Botvrij) comparada contra logs de red o Sysmon Event ID 3. (2) Sysmon Event ID 3 (Fase 2) — conexión desde proceso sospechoso a IP de botnet conocida. (3) Logs de aplicación si el sistema registra conexiones salientes. |
| **Lógica de detección** | Con feeds de TI: regla custom — match de IP destino contra CDB list de botnets → nivel 12. Con Sysmon: correlación proceso + IP de botnet → nivel 12. Sin ninguno de los dos: cobertura nula en Fase 1. |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1583.005 — Botnet |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — requiere integrar feeds específicos de botnet (Feodo Tracker, Abuse.ch) como CDB lists en Wazuh con actualización automática. |
| **Falsos positivos** | Dependen de la calidad del feed. Feodo Tracker y Abuse.ch tienen buena reputación y tasa de FP baja. |
| **Brecha de cobertura** | Sin feeds de TI ni Sysmon, la detección de botnets en sistemas sin PA es prácticamente imposible en Fase 1. Prioridad de implementación: alta. |
| **Estado** | Pendiente de validación. Cobertura real en Fase 1: nula. Cobertura objetivo con feeds TI + Sysmon: media-alta. |

---

#### Fichas detalladas — NET-02 (Conexiones a nodos TOR o proxies anónimos)

---

##### NET.02.PALO.TOR.001 — Conexión a nodos TOR o proxies anónimos

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno está conectándose a la red TOR o usando servicios de proxy anónimo para ocultar su tráfico. Desde el punto de vista del SOC hay dos escenarios: (1) usuario intentando evadir controles de navegación (política); (2) malware usando TOR como canal C2 para dificultar el rastreo del servidor de mando. Ambos requieren investigación — el segundo es indicador de compromiso avanzado. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 8.1 Uso no autorizado de recursos |
| **Peligrosidad** | ALTO |
| **Telemetría** | URL Filtering log de PAN-OS — categoría `proxy-avoidance-and-anonymizers`. Traffic log — conexiones TCP al puerto 9001 o 9030 (puertos estándar de TOR) o a IPs conocidas de nodos TOR (PAN-DB mantiene la lista actualizada). DNS Security log — consultas a dominios `.onion` o a puentes TOR conocidos. Campos clave: `src_ip`, `dst_ip`, `dst_port`, `application`, `url`, `action`. |
| **Lógica de detección** | Regla built-in: URL Filtering con categoría `proxy-avoidance-and-anonymizers` → nivel 6-8 según política del cliente. Regla custom de alta prioridad: conexión TCP a puerto 9001/9030 desde endpoint corporativo → nivel 10 (uso directo de cliente TOR). Regla crítica: proceso del sistema (svchost, lsass, powershell) conectando a nodo TOR → nivel 12 (malware usando TOR como C2). |
| **MITRE ATT&CK** | T1090.003 — Proxy: Multi-hop Proxy / T1090 — Proxy / T1071 — Application Layer Protocol |
| **Severidad** | Media (usuario evadiendo controles) / Crítica (malware con C2 sobre TOR) |
| **Esfuerzo** | Bajo — PAN-DB tiene categoría `proxy-avoidance-and-anonymizers` y lista de nodos TOR actualizada. La diferenciación usuario vs malware requiere correlación con el proceso origen (Sysmon Fase 2). |
| **Falsos positivos** | Bajos. El uso de TOR en entornos corporativos es prácticamente siempre anómalo. Posibles FP en organizaciones con casos de uso legítimo (investigación OSINT, periodismo). |
| **Diferenciación usuario vs malware** | Sin Sysmon: imposible distinguir si es el usuario o un proceso malicioso. Con Sysmon Event ID 3: si el proceso origen es un navegador (chrome.exe, firefox.exe) → probable usuario. Si es un proceso de sistema o no esperado → probable malware. |
| **Recomendación de hardening** | Bloquear en PA la categoría `proxy-avoidance-and-anonymizers` y los puertos 9001/9030 salientes. En clientes que necesiten TOR para investigación, crear una excepción por usuario/IP de origen. |
| **Estado** | Pendiente de validación. |

---

#### Fichas detalladas — NET-02 (Tráfico hacia dominios recientemente creados)

---

##### NET.02.PALO.NRD.001 — Tráfico hacia dominios recientemente registrados

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno está accediendo o resolviendo dominios registrados hace menos de 30 días (Newly Registered Domains / NRD). Técnica habitual de atacantes para evadir listas negras: registran dominios nuevos poco antes del ataque, antes de que los feeds de TI los clasifiquen. Especialmente relevante para campañas de phishing, distribución de malware y C2 de primera fase. No todo dominio nuevo es malicioso, pero el patrón en contexto corporativo merece revisión. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 2.2 Servidor C&C (Mando y Control) |
| **Peligrosidad** | ALTO |
| **Telemetría** | DNS Security log de PAN-OS — `dns_category = newly-registered-domain` o `dns_category = recent-domains`. URL Filtering log — categoría `newly-registered-domain` cuando el acceso es HTTP/S. Campos clave: `dns_query` (dominio NRD), `src_ip`, `action`, `dns_category`. |
| **Lógica de detección** | Regla custom: `dns_category = newly-registered-domain` → nivel 6 (informativo, requiere revisión). Regla de correlación: NRD + categoría adicional sospechosa (malware, phishing, C2) en el mismo dominio → nivel 10. Regla crítica: mismo `src_ip` resolviendo 3+ dominios NRD distintos en 300s → nivel 10 (patrón de DGA o campaña activa). Correlación con Threat log: si un NRD genera también un evento de Threat Prevention → nivel 12. |
| **MITRE ATT&CK** | T1583.001 — Acquire Infrastructure: Domains / T1566 — Phishing / T1071.004 — DNS |
| **Severidad** | Media / Alta (según correlación) |
| **Esfuerzo** | Bajo — DNS Security categoriza NRDs automáticamente. El tuning de umbrales para reducir FP es el esfuerzo principal. |
| **Falsos positivos** | Medios. Muchos dominios nuevos son legítimos (nuevos servicios SaaS, sitios de proveedores recién creados). La correlación con otras categorías sospechosas es esencial para reducir FP. Proceso de excepción necesario para dominios NRD de proveedores conocidos del cliente. |
| **Nota operativa** | Esta ficha es especialmente útil como señal temprana de campaña: si varios endpoints del mismo cliente resuelven el mismo NRD en un periodo corto, es indicador de campaña de phishing activa contra ese cliente. Correlacionar con M365-04 (phishing por correo) si está disponible. |
| **Estado** | Pendiente de validación. |

---

### NET-03 — Command & Control y beaconing

> ¿Existe comunicación persistente compatible con control remoto?

- Conexiones periódicas a un mismo destino
- Patrones tipo beacon
- DNS beaconing
- Túneles HTTP/S o DNS
- JA3/JA4 sospechoso

#### Fichas detalladas — NET-03 (Command & Control y beaconing)

---

##### NET.03.PALO.BEACON.001 — Beaconing periódico hacia mismo destino externo (Palo Alto Traffic log)

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno establece conexiones periódicas y regulares hacia el mismo destino externo en intervalos constantes o casi constantes. Patrón característico de malware que hace check-in con su servidor C2 para recibir comandos — el intervalo de beaconing suele estar hardcodeado en el implante (cada 60s, cada 5min, cada 1h). A diferencia de NET-02, este caso no requiere que el destino esté en ninguna lista negra: es el patrón temporal lo que es anómalo. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Traffic log de PAN-OS — tipo `TRAFFIC`, sesiones completadas hacia el mismo `dst_ip` o `dst_fqdn` desde el mismo `src_ip`. Campos clave: `src_ip`, `dst_ip`, `dst_port`, `application`, `bytes`, `elapsed`, `session_end_reason`, timestamps de sesión. |
| **Lógica de detección** | Regla custom de correlación en Wazuh: 6+ sesiones desde el mismo `src_ip` hacia el mismo `dst_ip:dst_port` en ventana de 60 minutos con `bytes` por sesión similares → nivel 8. Para beaconing de baja frecuencia: ampliar ventana a 24h. La regularidad del intervalo es el indicador clave: tráfico legítimo tiene varianza alta; beaconing tiene varianza muy baja. |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1571 — Non-Standard Port / T1090 — Proxy |
| **Severidad** | Alta |
| **Esfuerzo** | Alto — la detección estadística de beaconing en Wazuh requiere reglas custom con correlación temporal avanzada. Sin NetFlow, solo se puede aproximar por frecuencia y volumen uniforme. |
| **Falsos positivos** | Medios. Muchas aplicaciones legítimas hacen check-ins periódicos (antivirus, agentes de gestión, telemetría, NTP). Whitelist de aplicaciones y destinos conocidos esencial antes de activar. |
| **Limitación** | Sin NetFlow, Wazuh solo ve las sesiones registradas en el Traffic log de PA. Para beaconing de baja frecuencia (cada 4-8h) ampliar la ventana de correlación a 24h. |
| **Estado** | Pendiente de validación. |

---

##### NET.03.PALO.BEACON.002 — C2 sobre HTTP/S con patrón de beaconing (Palo Alto)

| Campo | Detalle |
|---|---|
| **Descripción** | Palo Alto detecta tráfico HTTP/S saliente con características propias de beaconing C2: User-Agent anómalo o hardcodeado, URI con estructura fija, respuestas de tamaño uniforme, intervalos regulares. Muchos frameworks C2 modernos (Cobalt Strike, Sliver, Mythic) usan HTTP/S con perfiles de mimetismo para parecerse a tráfico legítimo, pero mantienen patrones detectables en el User-Agent o en la estructura de la URI. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | URL Filtering log de PAN-OS con SSL Decryption activo — campos `url`, `user_agent`, `http_method`, `response_content_type`, `bytes_sent`, `bytes_received`. Threat log subtipo `spyware` con categoría `command-and-control` sobre tráfico web. Campos clave: `src_ip`, `dst_fqdn`, `url`, `user_agent`, `action`. |
| **Lógica de detección** | Regla custom: User-Agent vacío o con valor por defecto de framework C2 conocido (ej. Cobalt Strike default: `Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0)`) → nivel 10. Regla de correlación: mismo `src_ip` + mismo `dst_fqdn` + mismo `user_agent` + `bytes` uniformes en múltiples sesiones → nivel 10. Regla crítica: patrón anterior + destino NRD o sin categoría en PAN-DB → nivel 12. |
| **MITRE ATT&CK** | T1071.001 — Web Protocols / T1001.003 — Protocol Impersonation / T1568 — Dynamic Resolution |
| **Severidad** | Alta / Crítica |
| **Esfuerzo** | Alto — requiere SSL Decryption activo para ver User-Agent y URL en HTTPS. Sin decryption solo es visible el patrón de conexiones TCP. |
| **Prerequisito** | SSL Decryption activo en tráfico saliente. |
| **Falsos positivos** | Medios. La combinación User-Agent + uniformidad de bytes + periodicidad reduce los FP significativamente. |
| **Estado** | Pendiente de validación. Cobertura completa solo con SSL Decryption saliente activo. |

---

##### NET.03.PALO.DNS.001 — DNS beaconing y tunneling

| Campo | Detalle |
|---|---|
| **Descripción** | Un activo interno usa el protocolo DNS como canal de comunicación encubierto con un servidor C2: el malware codifica datos en las consultas DNS (subdominios de alta entropía o longitud inusual) y recibe respuestas en los registros TXT, CNAME o A. El DNS tunneling permite exfiltrar datos y recibir comandos incluso en redes donde todo el tráfico TCP/UDP está bloqueado excepto DNS. Complementa NET.02.PALO.C2.003 añadiendo detección por comportamiento del protocolo. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | DNS Security log de PAN-OS — subtipo `dns`, campos `dns_query`, `dns_type` (A, TXT, CNAME, MX), `dns_response`, `src_ip`. Complementariamente Threat log con firmas de DNS tunneling (iodine, dnscat2, dns2tcp). |
| **Lógica de detección** | Regla custom — alta entropía en `dns_query` (subdominio > 40 caracteres o con caracteres base64/hex) → nivel 8. Correlación: mismo `src_ip` con N consultas DNS al mismo dominio padre en 60s con subdominios distintos de alta entropía → nivel 10. Built-in: firma de herramienta de tunneling conocida → nivel 12. Adicional: volumen anómalo de consultas DNS tipo TXT desde un único `src_ip` → nivel 8. |
| **MITRE ATT&CK** | T1071.004 — DNS / T1048.003 — Exfiltration Over Unencrypted Non-C2 Protocol / T1132 — Data Encoding |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — DNS Security detecta herramientas conocidas de tunneling de forma built-in. La detección por entropía de subdominios requiere reglas custom. |
| **Falsos positivos** | Medios. CDNs y servicios legítimos (Akamai, Fastly) usan subdominios largos de alta entropía. Whitelist de dominios conocidos esencial. |
| **Diferencia con NET.02.PALO.C2.003** | NET.02.PALO.C2.003 detecta dominios C2 conocidos por PAN-DB. Esta ficha detecta el comportamiento de tunneling/beaconing DNS independientemente de si el dominio está en alguna lista negra — cubre C2 sobre dominios nuevos o desconocidos. |
| **Estado** | Pendiente de validación. |

---

##### NET.03.EP.BEACON.001 — Beaconing detectado a nivel de proceso (Sysmon)

| Campo | Detalle |
|---|---|
| **Descripción** | Sysmon detecta que un proceso específico en el endpoint establece conexiones periódicas y regulares hacia el mismo destino externo. A diferencia de NET.03.PALO.BEACON.001 (que ve el tráfico de red sin saber el proceso), esta ficha correlaciona el proceso responsable con el patrón de beaconing, lo que es fundamental para la investigación forense y para distinguir beaconing malicioso de check-ins legítimos de aplicaciones. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 3 (Network connection) — campos `Image` (proceso), `DestinationIp`, `DestinationPort`, `DestinationHostname`, timestamp. La correlación temporal de múltiples Event ID 3 del mismo proceso hacia el mismo destino revela el patrón de beaconing. |
| **Lógica de detección** | Regla custom de correlación: mismo `Image` + mismo `DestinationIp:DestinationPort` con 5+ eventos Event ID 3 en 30 minutos → nivel 8. Reglas de alta confianza: (1) Proceso Office (winword.exe, excel.exe) con Event ID 3 periódico hacia IP externa → nivel 12. (2) Proceso sin firma digital con beaconing periódico → nivel 12. (3) Proceso en ruta anómala (`%TEMP%`, `%APPDATA%`) con conexiones periódicas → nivel 12. |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1059 — Command and Scripting Interpreter / T1053 — Scheduled Task/Job |
| **Severidad** | Alta / Crítica (según proceso implicado) |
| **Esfuerzo** | Alto — requiere Sysmon (Fase 2) y gestión del volumen de Event ID 3. Whitelist de procesos legítimos con check-ins periódicos conocidos imprescindible. |
| **Prerequisito** | Sysmon desplegado en Fase 2. No disponible en Fase 1. |
| **Falsos positivos** | Medios para la regla genérica. Muy bajos para reglas de proceso específico (Office con beaconing, proceso sin firma, ruta anómala). |
| **Ventaja sobre NET.03.PALO.BEACON.001** | Identifica el proceso responsable del beaconing, lo que permite distinguir malware de aplicaciones legítimas y acelera la investigación forense. La combinación de ambas fichas da la mayor confianza. |
| **Estado** | Pendiente de validación. Aplica solo en endpoints con Sysmon desplegado (Fase 2). |

---

### NET-04 — Reconocimiento y escaneo interno

> ¿Algún activo está explorando la red interna?

- Port scanning y host discovery
- Escaneo SMB, RDP, SSH, WinRM
- Conexiones a muchos destinos internos o puertos
- Uso de herramientas como Nmap, Masscan

---

### NET-05 — Movimiento lateral

> ¿Un atacante está moviéndose desde un sistema comprometido?

- Conexiones SMB/RDP/WinRM laterales
- Uso de PsExec observado por red
- Acceso a shares administrativos
- Saltos entre VLANs o segmentos no habituales

---

### NET-06 — Exfiltración de datos

> ¿Se están sacando datos de la organización?

- Subida anómala de volumen
- Transferencia a servicios cloud no autorizados
- Uso de FTP, SFTP, SCP, rclone
- Tráfico saliente fuera de horario

---

### NET-07 — Uso anómalo de protocolos y servicios

> ¿Se están usando protocolos de forma insegura?

- DNS directo a resolvers externos
- Tráfico SMB hacia Internet
- Túneles SSH no autorizados
- Uso de puertos no estándar

---

### NET-08 — DNS sospechoso

> ¿El comportamiento DNS indica malware, evasión o túnel?

- Dominios DGA
- DNS tunneling
- Dominios alta entropía
- DoH/DoT no autorizado
- Typosquatting

---

### NET-09 — Accesos remotos y VPN anómalos

> ¿El acceso remoto está siendo abusado?

- Accesos VPN desde países no habituales
- Password spraying contra VPN
- Conexiones simultáneas imposibles
- Sesiones muy largas o recurrentes

---

### NET-10 — Denegación de servicio

> ¿Hay un ataque que afecte a la disponibilidad?

- Picos anómalos de tráfico
- SYN/UDP/ICMP flood
- Saturación de firewall o VPN
- Comportamiento compatible con DDoS

---

### NET-11 — Violación de segmentación

> ¿La segmentación está siendo violada?

- Comunicación entre VLANs no permitida
- Tráfico desde IoT hacia sistemas críticos
- Cambios no autorizados en reglas de firewall

---

### NET-12 — Dispositivos no autorizados

> ¿Hay activos no autorizados dentro de la red?

- Nuevos dispositivos con MAC desconocida
- Rogue access points
- Servidores DHCP no autorizados

---

### NET-13 — WiFi y acceso físico a red

> ¿El acceso inalámbrico está siendo abusado?

- Rogue AP y evil twin
- Deauth attacks
- Salto de red guest a red corporativa

---

### NET-14 — Abuso de aplicaciones y navegación

> ¿Los usuarios usan Internet de forma insegura?

- Navegación a sitios de phishing
- Shadow IT
- Descarga de ejecutables sospechosos

---

### NET-15 — Anomalías de comportamiento de red

> ¿La red muestra comportamientos fuera de patrón?

- Cambio radical de patrón de tráfico
- Tráfico fuera de horario
- Aparición de nuevos protocolos
- Desviaciones respecto a línea base

---

