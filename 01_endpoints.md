# Catálogo SOC GrayHats — Sección 1: Endpoints

---

## Índice

- [1.1 Windows](#11-windows)
  - [EP-01 — Malware y código malicioso](#ep-01--malware-y-código-malicioso)
    - EP.01.WIN.AV.001 — Malware detectado por SentinelOne
    - EP.01.WIN.AV.002 — Malware detectado por Microsoft Defender
    - EP.01.WIN.AV.003 — Malware detectado por Bitdefender GravityZone
  - [EP-02 — Intrusión o compromiso del endpoint](#ep-02--intrusión-o-compromiso-del-endpoint)
    - EP.02.WIN.AUTH.001 — Brute force de login remoto (RDP / SMB / WinRM)
    - EP.02.WIN.AUTH.003 — Cuenta de usuario bloqueada por intentos fallidos
    - **Ejecución remota sospechosa**
    - EP.02.WIN.EXEC.001 — Ejecución remota mediante PsExec / herramientas Sysinternals
    - EP.02.WIN.EXEC.002 — Ejecución remota mediante WMI
    - EP.02.WIN.EXEC.003 — Ejecución remota mediante PowerShell / WinRM
    - EP.02.WIN.EXEC.004 — Ejecución remota mediante Scheduled Task
    - EP.02.WIN.EXEC.005 — Correlación transversal: ejecución remota multi-vector
    - **Acceso con credenciales robadas**
    - EP.02.WIN.CRED.001 — Credential dumping: acceso a LSASS
    - EP.02.WIN.CRED.002 — Pass-the-Hash
    - EP.02.WIN.CRED.003 — Pass-the-Ticket
    - EP.02.WIN.CRED.004 — Kerberoasting
    - EP.02.WIN.CRED.005 — Herramientas de credential dumping conocidas
    - EP.02.WIN.CRED.006 — Uso de credenciales robadas: login exitoso anómalo
    - **Elevación de privilegios**
    - EP.02.WIN.PRIVESC.001 — Bypass de UAC
    - EP.02.WIN.PRIVESC.002 — Token impersonation / manipulación de tokens
    - EP.02.WIN.PRIVESC.003 — Explotación de vulnerabilidad local para escalada
    - EP.02.WIN.PRIVESC.004 — Abuso de servicios o tareas para escalada
    - EP.02.WIN.PRIVESC.005 — Correlación: escalada de privilegios confirmada
    - **Actividad post-explotación**
    - EP.02.WIN.POST.001 — Discovery: enumeración de usuarios y grupos
    - EP.02.WIN.POST.002 — Discovery: enumeración de hosts y shares de red
    - EP.02.WIN.POST.003 — Discovery: enumeración de AD (BloodHound / SharpHound)
    - EP.02.WIN.POST.004 — Staging: descarga de herramientas desde Internet (LOLBins)
    - EP.02.WIN.POST.005 — Staging: compresión y preparación de datos para exfiltración
    - EP.02.WIN.POST.006 — Lateral preparation: escaneo interno desde endpoint comprometido
    - EP.02.WIN.POST.007 — Correlación: secuencia post-explotación confirmada
    - **Herramientas de pentesting y red team**
    - EP.02.WIN.REDTEAM.001 — Frameworks C2 (Cobalt Strike, Sliver, Havoc, Metasploit)
    - EP.02.WIN.REDTEAM.002 — Herramientas de explotación y post-explotación (Impacket, CME, Responder)
    - EP.02.WIN.REDTEAM.003 — Herramientas de reconocimiento y escaneo no autorizadas
    - EP.02.WIN.REDTEAM.004 — Ejecución de payloads en memoria (process injection, shellcode)
    - EP.02.WIN.REDTEAM.005 — Correlación: perfil de red team activo en el endpoint
    - **Explotación de vulnerabilidades locales**
    - EP.02.WIN.EXPLOIT.001 — Explotación de aplicaciones de usuario (Office, browsers, PDF)
    - EP.02.WIN.EXPLOIT.002 — Explotación de servicios y aplicaciones locales
    - EP.02.WIN.EXPLOIT.003 — Uso de exploits públicos conocidos (PoC de CVE recientes)
    - EP.02.WIN.EXPLOIT.004 — Correlación: explotación confirmada y payload ejecutado
  - [EP-03 — Persistencia](#ep-03--persistencia)
    - **Creación de servicios**
    - EP.03.WIN.PERS.001 — Instalación de servicio nuevo (detección básica)
    - EP.03.WIN.SVC.001 — Servicio persistente con binario sospechoso o proceso anómalo
    - **Tareas programadas**
    - EP.03.WIN.PERS.002 — Creación o modificación de tarea programada (detección básica)
    - EP.03.WIN.TASK.001 — Tarea programada con acción sospechosa o proceso anómalo
    - **Claves Run/RunOnce y autoarranque**
    - EP.03.WIN.RUN.001 — Escritura en claves Run/RunOnce por proceso sospechoso
    - EP.03.WIN.RUN.002 — Claves de autoarranque avanzadas (AppInit_DLLs, Winlogon, IFEO)
    - EP.03.WIN.RUN.003 — Persistencia en HKCU Run sin privilegios de administrador
    - **Modificación de inicio de sesión**
    - EP.03.WIN.LOGON.001 — Modificación de proveedores de autenticación
    - EP.03.WIN.LOGON.002 — Scripts de logon/logoff y Winlogon Notify
    - EP.03.WIN.LOGON.003 — Abuso de ScreenSaver como mecanismo de persistencia
    - EP.03.WIN.LOGON.004 — Abuso de Active Setup para persistencia por usuario
    - **Instalación de drivers**
    - EP.03.WIN.DRV.001 — Driver no firmado o con firma inválida
    - EP.03.WIN.DRV.002 — BYOVD: driver legítimo vulnerable usado para evasión o escalada
    - EP.03.WIN.DRV.003 — Driver instalado desde ruta anómala o por proceso no autorizado
    - **DLL Hijacking**
    - EP.03.WIN.DLL.001 — DLL Search Order Hijacking
    - EP.03.WIN.DLL.002 — DLL Sideloading
    - EP.03.WIN.DLL.003 — Phantom DLL Hijacking
    - EP.03.WIN.DLL.004 — DLL de sistema sobrescrita o reemplazada
    - *(Pendiente: scripts de arranque, web shells, cuentas locales persistentes, GPO locales)*
  - [EP-04 — Robo o abuso de credenciales](#ep-04--robo-o-abuso-de-credenciales)
    - EP.04.WIN.AUTH.002 — Brute force de login local
    - EP.04.WIN.IDM.003 — Modificación de cuenta de usuario
    - EP.04.WIN.IDM.004 — Cambio de contraseña por otro usuario
  - [EP-08 — Comportamiento anómalo del usuario o del equipo](#ep-08--comportamiento-anómalo-del-usuario-o-del-equipo)
    - EP.08.WIN.AUTH.004 — Login interactivo con cuenta privilegiada
  - [EP-09 — Violación de políticas de seguridad](#ep-09--violación-de-políticas-de-seguridad)
    - EP.09.WIN.FIM.001 — Modificación de ficheros críticos del sistema
  - [EP-10 — Manipulación defensiva y evasión](#ep-10--manipulación-defensiva-y-evasión)
    - EP.10.WIN.AUDIT.001 — Limpieza del log de auditoría de seguridad
    - EP.10.WIN.AUDIT.002 — Modificación de la política de auditoría
    - EP.10.WIN.AV.001 — Microsoft Defender deshabilitado o manipulado
- [1.3 Linux](#13-linux) *(pendiente)*
- [1.4 macOS](#14-macos) *(pendiente)*

---

## 1. Endpoints

Detecciones orientadas a identificar actividad maliciosa, sospechosa o anómala ejecutándose directamente en los endpoints monitorizados. La cobertura se organiza por sistema operativo y fase de despliegue.

---

### 1.1 Windows

#### Alcance de la Windows

**Familias cubiertas:**

- **WIN.AUTH.\*** — Autenticación y acceso: fuerza bruta, cuentas bloqueadas, sesiones privilegiadas.
- **WIN.IDM.\*** — Gestión de identidad: creación/modificación de cuentas, cambios en grupos privilegiados.
- **WIN.AUDIT.\*** — Auditoría: limpieza de logs, modificación de política de auditoría.
- **WIN.PERS.\*** — Persistencia: instalación de servicios, tareas programadas.
- **WIN.AV.\*** — Protección antimalware: manipulación de Defender y detecciones.
- **WIN.FIM.\*** — Integridad de ficheros: modificación de ficheros críticos del sistema.

**Casos de uso pendientes de desarrollo:**

- Credential dumping (acceso a LSASS)
- Persistencia en claves de registro (Run, RunOnce, AppInit_DLLs)
- Ejecución sospechosa de procesos (rutas anómalas, LOLBin)
- Análisis de PowerShell ScriptBlock
- Detección heurística de ransomware en tiempo real (la aporta el EDR)
- Comunicaciones C2 salientes (requiere visibilidad de red)

#### Telemetría requerida en el agente

| Canal | Casos de uso que alimenta | Por defecto |
|---|---|---|
| Security | AUTH.001-004, IDM.001-004, AUDIT.001-002, PERS.002 | Sí |
| System | PERS.001, AV.001 (parada servicio Defender) | Sí |
| Windows Defender/Operational | AV.001, AV.002 | No |
| TaskScheduler/Operational | PERS.002 (alternativa con detalle) | No |
| Módulo FIM (syscheck) | FIM.001 | Sí |

#### Catálogo resumido

| ID | Caso de uso | MITRE | Sev. | Built-in |
|---|---|---|---|---|
| EP.01.WIN.AV.001 | Malware detectado por SentinelOne | Variable | Variable | Comunitario |
| EP.01.WIN.AV.002 | Malware detectado por Defender | — | Variable | Sí |
| EP.01.WIN.AV.003 | Malware detectado por GravityZone | Variable | Variable | Comunitario |
| EP.02.WIN.AUTH.001 | Brute force remoto (RDP/SMB/WinRM) | T1110 | Alta | Sí |
| EP.02.WIN.AUTH.003 | Cuenta de usuario bloqueada | T1110 | Alta | Sí |
| EP.03.WIN.IDM.001 | Creación de cuenta local | T1136.001 | Alta | Sí |
| EP.03.WIN.IDM.002 | Añadido a grupo Administradores | T1098 | Alta | Sí |
| EP.03.WIN.PERS.001 | Instalación de servicio nuevo | T1543.003 | Media-Alta | Sí |
| EP.03.WIN.PERS.002 | Tarea programada creada/modificada | T1053.005 | Media-Alta | Sí |
| EP.04.WIN.AUTH.002 | Brute force local (consola/teclado) | T1110.001 | Media-Alta | Custom |
| EP.04.WIN.IDM.003 | Modificación de cuenta de usuario | T1098 | Media | Sí |
| EP.04.WIN.IDM.004 | Cambio de contraseña por otro usuario | T1098 | Media | Sí |
| EP.08.WIN.AUTH.004 | Login interactivo privilegiado | T1078 | Media | Sí |
| EP.09.WIN.FIM.001 | Modificación de ficheros críticos | T1565.001 | Media | Sí |
| EP.10.WIN.AUDIT.001 | Limpieza del log de seguridad | T1070.001 | Crítica | Sí |
| EP.10.WIN.AUDIT.002 | Modificación de política de auditoría | T1562.002 | Alta | Sí |
| EP.10.WIN.AV.001 | Defender deshabilitado o manipulado | T1562.001 | Alta | Sí |

---

#### Fichas detalladas

---

##### EP-01 — Malware y código malicioso

---

###### EP.01.WIN.AV.001 — Malware detectado por SentinelOne

| Campo | Detalle |
|---|---|
| **Descripción** | SentinelOne ha detectado y respondido ante una amenaza en el endpoint. La consola de gestión S1 reenvía la alerta vía syslog al manager Wazuh. El SOC debe investigar el vector de entrada, el proceso implicado y verificar que la amenaza no ha generado persistencia adicional antes de que S1 respondiera. |
| **Clasificación GrayHats** | 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Syslog desde la consola de gestión SentinelOne (Management Console → Syslog Integration) hacia el manager Wazuh. Se configuran en la consola únicamente los eventos de tipo **Threat** (alertas de malware); el resto de tipos de evento no se reenvían en esta fase. El manager recibe los mensajes en formato JSON sobre UDP/TCP. |
| **Ingesta en Wazuh** | `<localfile>` en `ossec.conf` del manager apuntando al puerto syslog receptor, con `log_format` establecido a `syslog`. El decoder del grupo `sentinelone` parsea el JSON embebido en el mensaje syslog y extrae los campos clave: `threatInfo.classification`, `threatInfo.mitreTechnique`, `agentDetectionInfo.agentComputerName`, `threatInfo.filePath`. |
| **Lógica de detección** | Reglas del grupo `sentinelone` (ruleset comunitario socfortress/Wazuh-Rules). Niveles orientativos: Suspicious → nivel 6, Malicious → nivel 10, Malicious + acción Kill/Quarantine → nivel 12. |
| **MITRE ATT&CK** | Variable — S1 reporta la técnica en `threatInfo.mitreTechnique`; el ruleset la mapea a `rule.mitre.id`. |
| **Severidad** | Variable según clasificación del agente S1 |
| **Esfuerzo** | Medio — configuración del syslog en la consola S1, apertura de puerto en el manager, validación de decoder y ajuste de niveles de alerta. |
| **Falsos positivos** | Muy bajos. S1 aplica su propio filtrado antes de alertar; cualquier evento que llega a Wazuh merece atención. |
| **Aplicabilidad** | Endpoints con SentinelOne desplegado. Sustituye a `EP.01.WIN.AV.002` (Defender) en esos equipos, ya que S1 desactiva Defender por diseño. |
| **Estado** | Pendiente de validación en entorno de laboratorio. |

---

###### EP.01.WIN.AV.002 — Malware detectado por Microsoft Defender

| Campo | Detalle |
|---|---|
| **Descripción** | Defender ha detectado malware o una amenaza en el endpoint. Aunque la herramienta ya respondió, el SOC debe investigar el vector de entrada y verificar que la amenaza no ha persistido. |
| **Clasificación GrayHats** | 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Microsoft-Windows-Windows Defender/Operational — Event IDs 1116 (Detected malware), 1117 (Action taken), 1118 (Action failed), 1006/1007/1008. |
| **Lógica de detección** | Reglas built-in del grupo `windows_defender` (nivel 9-12 según severidad). |
| **MITRE ATT&CK** | — |
| **Severidad** | Variable según el indicador |
| **Esfuerzo** | Bajo — solo añadir el canal Defender al `agent.conf`. |
| **Aplicabilidad** | No aplica en endpoints con EDR de terceros (SentinelOne, CrowdStrike). Cubierto por reglas del EDR correspondiente. |

---

###### EP.01.WIN.AV.003 — Malware detectado por Bitdefender GravityZone

| Campo | Detalle |
|---|---|
| **Descripción** | Bitdefender GravityZone ha detectado y respondido ante una amenaza en el endpoint. La consola GZ reenvía la alerta al manager Wazuh a través de un conector Ubuntu intermediario. El SOC debe investigar el vector de entrada, el proceso implicado y verificar que la amenaza no ha generado persistencia adicional antes de que GZ respondiera. |
| **Clasificación GrayHats** | 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | La consola GravityZone envía eventos vía API push (Event Push Service) en formato CEF hacia un endpoint Ubuntu conector con el paquete `gz-evpsc` de Bitdefender instalado. El conector reenvía los eventos por syslog (TCP/UDP, puerto configurable) al manager Wazuh. En esta fase se suscribe únicamente el tipo de evento `av` (antivirus/malware); el resto de tipos (`fw`, `ransomware-mitigation`, `network-sandboxing`, etc.) no se activan. |
| **Arquitectura de ingesta** | `Consola GZ → (HTTPS/CEF) → Ubuntu conector gz-evpsc → (syslog TCP) → Manager Wazuh`. El conector requiere IP pública o accesibilidad desde la nube GZ. Puerto por defecto del Event Push Service: `3200`. Puerto syslog hacia Wazuh: configurable (ej. `514`). |
| **Configuración del conector** | Instalar `gz-evpsc` en Ubuntu (`apt install gz-evpsc`). Ejecutar `config.sh` con los parámetros de puerto, protocolo, IP del manager y clave de autenticación. Habilitar y arrancar el servicio (`systemctl enable/start gz-evpsc`). Configurar el API push en la consola GZ mediante llamada JSON-RPC `setPushEventSettings` con `serviceType: cef` y `subscribeToEventTypes: {av: true}` y el resto a `false`. |
| **Ingesta en Wazuh** | `<localfile>` en `ossec.conf` del manager apuntando al puerto syslog del conector. El decoder del grupo `bitdefender` parsea el formato CEF y extrae los campos clave: `BitdefenderGZModule`, `dvchost` (nombre del endpoint), `filePath`, severidad y clasificación de la amenaza. |
| **Lógica de detección** | Reglas del grupo `bitdefender` (ruleset comunitario socfortress/Wazuh-Rules o reglas custom equivalentes). Niveles orientativos según severidad CEF: nivel 5-6 (Suspicious), nivel 10 (Malicious), nivel 12 (Malicious + acción de remediación). |
| **MITRE ATT&CK** | Variable — GravityZone reporta la técnica en los metadatos CEF cuando está disponible. |
| **Severidad** | Variable según clasificación del agente GZ |
| **Esfuerzo** | Alto — requiere desplegar y mantener el conector Ubuntu intermediario, gestionar certificados TLS, configurar el API push en la consola GZ y validar el decoder CEF. Mayor complejidad operativa que la integración con SentinelOne. |
| **Falsos positivos** | Muy bajos. GZ aplica su propio filtrado antes de alertar. |
| **Aplicabilidad** | Endpoints con Bitdefender GravityZone desplegado. Puede coexistir con SentinelOne en algunos clientes (productos distintos en flotas distintas del mismo cliente). En endpoints con GZ, Defender queda desactivado por diseño. |
| **Dependencia** | Ubuntu conector con `gz-evpsc` desplegado y accesible desde la nube GZ. Decoder/reglas custom o ruleset comunitario con soporte CEF de Bitdefender. |
| **Estado** | Pendiente de validación en entorno de laboratorio. |
| **Referencia** | [wazuh.com/blog/integrating-bitdefender-gravityzone-with-wazuh](https://wazuh.com/blog/integrating-bitdefender-gravityzone-with-wazuh/) |

---

##### EP-02 — Intrusión o compromiso del endpoint

---

###### EP.02.WIN.AUTH.001 — Brute force de login remoto (RDP / SMB / WinRM)

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de múltiples intentos de autenticación fallidos contra un endpoint Windows desde la misma IP de origen. Patrón típico de fuerza bruta o password spraying contra servicios remotos expuestos. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Canal Security — Event ID 4625 (An account failed to log on) con campo `ipAddress` poblado. |
| **Lógica de detección** | Regla built-in 60122 (nivel 5) detecta el fallo individual. Regla built-in 60204 (nivel 10) correla 8 fallos en 240s con la misma `ipAddress`. |
| **MITRE ATT&CK** | T1110 — Brute Force |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. Solo requiere audit policy Logon en failure activada. |
| **Falsos positivos** | Bajos. Posible FP por escáneres autorizados; mitigación con whitelist por IP. |

---

###### EP.02.WIN.AUTH.003 — Cuenta de usuario bloqueada por intentos fallidos

| Campo | Detalle |
|---|---|
| **Descripción** | El sistema bloquea automáticamente una cuenta tras superar el umbral de intentos fallidos. Indicador fiable de un ataque de fuerza bruta consumado contra esa cuenta. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Canal Security — Event ID 4740 (A user account was locked out). |
| **Lógica de detección** | Regla built-in 60115 (nivel 9). Dispara con cada lockout individual. |
| **MITRE ATT&CK** | T1110 — Brute Force (resultado) |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. Requiere política de lockout activa en el dominio o local. |
| **Falsos positivos** | Muy bajos. Cualquier 4740 merece investigación. |

---

##### EP-03 — Persistencia

> ¿El atacante está intentando mantenerse en el sistema?

---

##### Fichas detalladas — EP-03 (Creación de servicios)

---

###### EP.03.WIN.PERS.001 — Instalación de servicio nuevo en el sistema (detección básica)

| Campo | Detalle |
|---|---|
| **Descripción** | Se instala un servicio nuevo en el endpoint. Técnica clásica de persistencia tras compromiso y vector común de malware (servicios maliciosos que arrancan con el sistema). |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal System — Event ID 7045 (A new service was installed) y/o canal Security — Event ID 4697. |
| **Lógica de detección** | Regla built-in 61138 (nivel 5 por defecto; recomendado overwrite a 8). |
| **MITRE ATT&CK** | T1543.003 — Create or Modify System Process: Windows Service |
| **Severidad** | Media-Alta |
| **Esfuerzo** | Bajo — built-in. Se recomienda whitelist de servicios legítimos del cliente. |
| **Falsos positivos** | Medios el primer mes; baja drásticamente tras tuning inicial. |

---

###### EP.03.WIN.SVC.001 — Servicio persistente con binario sospechoso o proceso de origen anómalo

| Campo | Detalle |
|---|---|
| **Descripción** | Se instala un servicio cuyo binario se encuentra en una ruta anómala (ruta temporal, directorio de usuario, AppData) o cuyo proceso creador no es una herramienta de administración autorizada. Amplía EP.03.WIN.PERS.001 añadiendo contexto de proceso origen y ruta del binario — los dos discriminadores más efectivos para separar servicios maliciosos de instalaciones legítimas de software. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — proceso `sc.exe` o `services.exe` con `CommandLine` conteniendo `create` y ruta de binario en `%TEMP%`, `%APPDATA%`, `%PUBLIC%`, `C:\Users\`. Security log — Event ID 7045 con `ImagePath` en ruta de usuario o temporal. Sysmon Event ID 13 (Registry value set) — escritura en `HKLM\SYSTEM\CurrentControlSet\Services\` con `ImagePath` apuntando a ruta anómala. |
| **Lógica de detección** | Regla custom alta confianza: Event ID 7045 con `ImagePath` conteniendo `%TEMP%`, `%APPDATA%`, `C:\Users\`, `C:\ProgramData\` (fuera de rutas de programa estándar) → nivel 12. Regla Sysmon: `sc.exe create` ejecutado desde proceso interactivo (cmd, powershell) por cuenta de usuario estándar → nivel 10. Regla Event ID 13: `ImagePath` escrito en clave de servicio por proceso no de sistema → nivel 10. Correlación: 7045 con ruta anómala + Event ID 3 (conexión saliente desde ese binario) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1543.003 — Create or Modify System Process: Windows Service |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — requiere Sysmon y reglas custom de análisis de ruta. La whitelist de rutas legítimas de instalación de software es esencial. |
| **Falsos positivos** | Bajos. Servicios legítimos raramente se instalan desde rutas temporales o de usuario. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Tareas programadas)

---

###### EP.03.WIN.PERS.002 — Creación o modificación de tarea programada (detección básica)

| Campo | Detalle |
|---|---|
| **Descripción** | Se crea o modifica una tarea programada en el endpoint. Vector de persistencia muy frecuente en malware y ataques manuales. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4698 (Scheduled task created), 4702 (updated). Alternativamente `Microsoft-Windows-TaskScheduler/Operational`. |
| **Lógica de detección** | Regla built-in 60228 (nivel 4 por defecto; recomendado overwrite a 8). El campo `TaskContent` contiene el XML completo, útil para investigación. |
| **MITRE ATT&CK** | T1053.005 — Scheduled Task |
| **Severidad** | Media-Alta |
| **Esfuerzo** | Bajo — built-in. Whitelist de tareas legítimas del cliente. |
| **Falsos positivos** | Medios el primer mes. |

---

###### EP.03.WIN.TASK.001 — Tarea programada con acción sospechosa o proceso de origen anómalo

| Campo | Detalle |
|---|---|
| **Descripción** | Se crea una tarea programada cuya acción ejecuta un intérprete de comandos, un LOLBin o un script desde ruta anómala, o cuyo proceso creador no es una herramienta de administración autorizada. Amplía EP.03.WIN.PERS.002 analizando el contenido de la acción de la tarea y el proceso que la crea — los indicadores más fiables de tarea maliciosa frente a tarea legítima. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4698 con campo `TaskContent` (XML) conteniendo en `<Command>` referencias a `powershell.exe`, `cmd.exe`, `wscript.exe`, `mshta.exe`, `certutil.exe`, `bitsadmin.exe` o ruta en `%TEMP%`/`%APPDATA%`. Sysmon Event ID 1 — `schtasks.exe` con `/create` y argumento `/tr` apuntando a LOLBin o ruta temporal. Microsoft-Windows-TaskScheduler/Operational — Event ID 106 (task registered) seguido de Event ID 200 (action started) con proceso hijo sospechoso. |
| **Lógica de detección** | Regla custom: Event ID 4698 con `TaskContent` conteniendo `<Command>powershell` o `<Command>cmd` con argumento codificado en base64 o con `IEX`/`DownloadString` → nivel 12. Regla Sysmon: `schtasks.exe /create` con `/tr` apuntando a `%TEMP%` o a LOLBin (`certutil`, `mshta`) → nivel 12. Regla TaskScheduler: Event ID 200 con acción spawneando intérprete de comandos desde proceso de sistema (svchost TaskScheduler) → nivel 10. Correlación: Event ID 4698 + Event ID 3 (conexión saliente desde el binario de la tarea) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1053.005 — Scheduled Task/Job: Scheduled Task / T1059.001 — PowerShell / T1218 — System Binary Proxy Execution |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — requiere parsing del campo `TaskContent` XML en la regla Wazuh. El decoder debe extraer el contenido de `<Command>` y `<Arguments>` del XML para que la regla pueda filtrar por ellos. |
| **Falsos positivos** | Bajos. Tareas legítimas raramente ejecutan intérpretes de comandos con argumentos codificados. |
| **Nota operativa** | El campo `TaskContent` del Event ID 4698 contiene el XML completo de la tarea — incluye el comando, los argumentos, el trigger y el contexto de seguridad. Es la fuente forense más completa para investigar tareas maliciosas. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Claves Run/RunOnce y autoarranque)

---

###### EP.03.WIN.RUN.001 — Escritura en claves Run/RunOnce por proceso sospechoso

| Campo | Detalle |
|---|---|
| **Descripción** | Un proceso escribe en las claves de registro de autoarranque `Run` o `RunOnce` en `HKLM` o `HKCU` para ejecutar un programa automáticamente en cada inicio de sesión o arranque del sistema. Es una de las técnicas de persistencia más comunes — cualquier valor añadido a estas claves por un proceso no administrativo o desde una ruta anómala es altamente sospechoso. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 (RegistryEvent - Value Set) — `TargetObject` conteniendo `\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` o `\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce` en `HKLM` o `HKCU`. Campos clave: `Image` (proceso que escribe), `Details` (valor escrito — ruta del binario de persistencia), `TargetObject` (clave exacta). |
| **Lógica de detección** | Regla Sysmon: Event ID 13 con `TargetObject` conteniendo `\CurrentVersion\Run` desde proceso no instalador → nivel 8. Alta confianza: mismo patrón con `Details` apuntando a `%TEMP%`, `%APPDATA%`, `C:\Users\` → nivel 12. Crítica: `Image` = `cmd.exe` o `powershell.exe` escribiendo en clave Run → nivel 12. Correlación: escritura en Run + Event ID 3 (conexión saliente desde el binario registrado) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1547.001 — Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — Sysmon Event ID 13 con clave específica es muy preciso. Whitelist de procesos instaladores autorizados esencial. |
| **Falsos positivos** | Medios. Instaladores legítimos escriben en Run (Teams, OneDrive, agentes de gestión). Whitelist de valores conocidos y procesos instaladores autorizados esencial. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.RUN.002 — Claves de autoarranque avanzadas (AppInit_DLLs, Winlogon, IFEO)

| Campo | Detalle |
|---|---|
| **Descripción** | Un proceso modifica claves de registro de autoarranque menos conocidas pero igualmente efectivas: `AppInit_DLLs` (DLL inyectada en todos los procesos que cargan user32.dll), `Winlogon` (ejecutado durante el login), `Image File Execution Options` (IFEO — permite sustituir un proceso legítimo por otro, técnica de accessibility features backdoor), `UserInitMprLogonScript`. Preferidas por atacantes avanzados al ser menos monitorizadas que Run/RunOnce. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — `TargetObject` conteniendo: `\AppInit_DLLs`, `\Winlogon\Userinit`, `\Winlogon\Shell`, `\Image File Execution Options\*\Debugger`, `\UserInitMprLogonScript`, `\BootExecute`, `\SessionManager\SubSystems`. Campos clave: `Image`, `Details`, `TargetObject`. |
| **Lógica de detección** | Regla alta confianza: Event ID 13 con `TargetObject` conteniendo `AppInit_DLLs` con `Details` no vacío → nivel 12. Crítica: `TargetObject` conteniendo `\Image File Execution Options\` + `\Debugger` → nivel 12 (IFEO debugger hijacking). Modificación de `Winlogon\Userinit` o `Winlogon\Shell` con valor distinto al estándar → nivel 12. |
| **MITRE ATT&CK** | T1546.010 — AppInit DLLs / T1546.012 — Image File Execution Options Injection / T1547.004 — Winlogon Helper DLL |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — claves muy específicas, raramente modificadas en operación normal. Volumen de FP muy bajo. |
| **Falsos positivos** | Muy bajos. `AppInit_DLLs` con valor no vacío es prácticamente siempre sospechoso. `IFEO\Debugger` fuera de entornos de desarrollo es siempre sospechoso. |
| **Nota operativa** | IFEO es especialmente insidiosa: el atacante establece `sethc.exe` (Sticky Keys) o `utilman.exe` con un Debugger apuntando a `cmd.exe`, obteniendo una shell SYSTEM desde la pantalla de login sin autenticación. Si se detecta, investigar accesos físicos o RDP recientes al endpoint. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.RUN.003 — Persistencia en HKCU Run sin privilegios de administrador

| Campo | Detalle |
|---|---|
| **Descripción** | Un proceso escribe en las claves Run de `HKCU` para establecer persistencia en el contexto del usuario actual sin necesitar privilegios de administrador. A diferencia de `HKLM\Run`, `HKCU\Run` puede ser escrita por cualquier proceso del usuario — muy frecuente en infostealers, RATs y adware que no han podido escalar privilegios. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — `TargetObject` conteniendo `HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` o `RunOnce`. Campos clave: `Image`, `Details` (ruta del binario registrado), `User`. |
| **Lógica de detección** | Regla Sysmon: Event ID 13 con `TargetObject` conteniendo `HKCU\*\CurrentVersion\Run` desde proceso en `%TEMP%`, `%APPDATA%` o `Downloads` → nivel 12. `Details` apuntando a ruta fuera de `C:\Program Files\` o `C:\Windows\` → nivel 10. Correlación: escritura en `HKCU\Run` + conexión saliente en 300s → nivel 12. `Details` contiene comando PowerShell codificado o LOLBin → nivel 12. |
| **MITRE ATT&CK** | T1547.001 — Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — misma lógica que RUN.001 sobre HKCU. Whitelist de aplicaciones de usuario conocidas (Teams, Slack, Spotify) esencial. |
| **Falsos positivos** | Medios. Muchas aplicaciones de usuario se registran en HKCU\Run legítimamente. La ruta del binario registrado es el discriminador principal — rutas temporales siempre sospechosas. |
| **Diferencia con RUN.001** | RUN.001 cubre HKLM (requiere privilegios). Esta ficha cubre HKCU (sin privilegios, más frecuente en malware de usuario) con la ruta del binario como discriminador principal. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Modificación de inicio de sesión)

---

###### EP.03.WIN.LOGON.001 — Modificación de proveedores de autenticación

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica las claves de registro que controlan los proveedores de autenticación y paquetes de seguridad de Windows (`Security Packages`, `Authentication Packages`, `Notification Packages`) para cargar una DLL maliciosa durante el proceso de autenticación. La DLL se ejecuta en el contexto de LSASS, dándole acceso a todas las credenciales que pasan por el subsistema de seguridad. Técnica avanzada y muy persistente — sobrevive reinicios y es difícil de detectar sin telemetría de registro. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — `TargetObject` conteniendo `HKLM\SYSTEM\CurrentControlSet\Control\Lsa\Security Packages`, `\Authentication Packages` o `\Notification Packages`. Campos clave: `Image` (proceso que modifica), `Details` (nuevo valor — nombre de la DLL maliciosa). Sysmon Event ID 7 — DLL cargada por `lsass.exe` con nombre no reconocido o sin firma válida tras el cambio. |
| **Lógica de detección** | Regla Sysmon alta confianza: Event ID 13 con `TargetObject` conteniendo `\Lsa\Security Packages` o `\Lsa\Authentication Packages` desde proceso distinto a `lsass.exe` o `services.exe` → nivel 12. Regla Event ID 7: DLL cargada por `lsass.exe` sin firma válida → nivel 12. Correlación: modificación de `\Lsa\*Packages` + DLL no firmada cargada por LSASS en 300s → nivel 12. |
| **MITRE ATT&CK** | T1547.005 — Security Support Provider / T1556.002 — Password Filter DLL |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — claves muy específicas, volumen de modificaciones legítimas prácticamente nulo en producción. |
| **Falsos positivos** | Muy bajos. Modificaciones legítimas de estos paquetes son extremadamente raras fuera de instalaciones de software de seguridad. |
| **Nota operativa** | Una DLL cargada como Security Package tiene acceso a todas las credenciales en texto claro que pasan por LSASS. Si se detecta, asumir que todas las credenciales del sistema están comprometidas — forzar reset de todas las cuentas que hayan iniciado sesión en el endpoint. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.LOGON.002 — Scripts de logon/logoff y Winlogon Notify

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante registra scripts que se ejecutan automáticamente durante el inicio o cierre de sesión del usuario: scripts de logon/logoff vía GPO local (`HKLM\SOFTWARE\Policies\Microsoft\Windows\System\Scripts`), o registra un handler en `Winlogon\Notify` para ejecutar código en eventos de autenticación. Estas técnicas permiten ejecutar código malicioso en cada inicio de sesión sin necesidad de modificar Run/RunOnce. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — `TargetObject` conteniendo `\Policies\Microsoft\Windows\System\Scripts\Logon`, `\Scripts\Logoff` o `\Winlogon\Notify\`. Sysmon Event ID 11 — creación de script (`.bat`, `.vbs`, `.ps1`) en `C:\Windows\System32\GroupPolicy\`. Sysmon Event ID 1 — `winlogon.exe` spawneando proceso sospechoso durante evento de logon. |
| **Lógica de detección** | Regla Sysmon Event ID 13: modificación de `\System\Scripts\Logon` o `\Scripts\Logoff` desde proceso no de administración de políticas → nivel 10. Regla Event ID 11: creación de script en directorio GroupPolicy por proceso de usuario → nivel 10. Regla Event ID 1: `winlogon.exe` spawneando `cmd.exe`, `powershell.exe` o proceso en ruta temporal → nivel 12. |
| **MITRE ATT&CK** | T1037.001 — Boot or Logon Initialization Scripts: Logon Script / T1547.004 — Winlogon Helper DLL |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — detección de scripts en GroupPolicy requiere FIM configurado sobre esa ruta además de Sysmon Event ID 13. |
| **Falsos positivos** | Bajos. Scripts de logon legítimos se gestionan desde el DC vía GPO del dominio, no desde el endpoint local. Modificaciones locales son siempre sospechosas. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.LOGON.003 — Abuso de ScreenSaver como mecanismo de persistencia

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica la configuración del salvapantallas de Windows para ejecutar un binario malicioso cuando el sistema lleva inactivo un tiempo determinado. El salvapantallas se ejecuta bajo el contexto del usuario activo. La extensión `.scr` es reconocida por Windows como ejecutable — cualquier `.exe` puede renombrarse a `.scr` para evasión. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — `TargetObject` conteniendo `HKCU\Control Panel\Desktop\SCRNSAVE.EXE` con `Details` apuntando a ruta anómala. `TargetObject` conteniendo `\Desktop\ScreenSaverIsSecure = 0` (desactivando contraseña al volver). Sysmon Event ID 11 — creación de fichero `.scr` en ruta de usuario o temporal. |
| **Lógica de detección** | Regla Sysmon: Event ID 13 con `TargetObject` = `HKCU\Control Panel\Desktop\SCRNSAVE.EXE` con `Details` fuera de `C:\Windows\System32\` → nivel 12. Regla: creación de fichero `.scr` en `%TEMP%`, `%APPDATA%` o `C:\Users\` → nivel 10. Correlación: modificación de SCRNSAVE.EXE + fichero `.scr` en ruta temporal en 120s → nivel 12. |
| **MITRE ATT&CK** | T1546.002 — Event Triggered Execution: Screensaver |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — clave de registro muy específica, volumen de FP muy bajo. |
| **Falsos positivos** | Muy bajos. Los usuarios raramente modifican el salvapantallas desde procesos no interactivos. |
| **Nota operativa** | El binario del salvapantallas se ejecuta con los permisos del usuario activo — no requiere privilegios de administrador. Frecuente en malware de usuario que no ha conseguido escalar privilegios. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.LOGON.004 — Abuso de Active Setup para persistencia por usuario

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante abusa del mecanismo Active Setup de Windows para ejecutar código malicioso en el contexto de cada usuario que inicia sesión por primera vez. Active Setup es un mecanismo legítimo para replicar configuraciones de HKLM a HKCU en el primer logon — el atacante registra un componente malicioso en `HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\` que se ejecutará automáticamente en el logon de cualquier usuario nuevo. Técnica de alta persistencia y baja visibilidad. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 12/13 — creación o modificación de clave bajo `HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\` con subclave nueva (GUID no reconocido) y valor `StubPath` apuntando a comando o ruta anómala. Campos clave: `TargetObject` (clave creada), `Details` (`StubPath` — comando a ejecutar). |
| **Lógica de detección** | Regla Sysmon: Event ID 12 con `TargetObject` conteniendo `\Active Setup\Installed Components\` + GUID no en whitelist → nivel 10. Crítica: Event ID 13 con `\Active Setup\Installed Components\*\StubPath` con `Details` apuntando a `%TEMP%`, `%APPDATA%` o LOLBin → nivel 12. Correlación: nueva entrada Active Setup + proceso hijo de `userinit.exe` coincidente con el `StubPath` → nivel 12. |
| **MITRE ATT&CK** | T1547.014 — Boot or Logon Autostart Execution: Active Setup |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere whitelist de GUIDs de componentes Active Setup legítimos del sistema (Internet Explorer, DirectX, Office). |
| **Falsos positivos** | Medios. Windows y algunas aplicaciones legítimas usan Active Setup. La whitelist de GUIDs conocidos reduce drásticamente los FP. |
| **Nota operativa** | Especialmente peligroso en sistemas con múltiples usuarios — el código malicioso se ejecuta en el contexto de cada usuario que hace logon, comprometiendo potencialmente todas las cuentas del sistema. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Instalación de drivers)

---

###### EP.03.WIN.DRV.001 — Driver no firmado o con firma inválida

| Campo | Detalle |
|---|---|
| **Descripción** | Se carga en el kernel de Windows un driver (`.sys`) sin firma digital válida o con firma revocada. Windows requiere firma de kernel (WHQL o EV) para cargar drivers en sistemas de 64 bits con Secure Boot — un driver no firmado que consigue cargarse indica que el atacante ha desactivado la verificación de firma o está usando un bootloader comprometido. Los rootkits y herramientas de evasión de EDR frecuentemente se implementan como drivers no firmados. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 6 (Driver Loaded) — campos clave: `ImageLoaded`, `Signed` (true/false), `Signature` (firmante), `SignatureStatus` (Valid/Expired/Revoked/Unavailable). Security log — Event ID 7045 con `ServiceType = kernel driver`. Sysmon Event ID 13 — modificación de `HKLM\SYSTEM\CurrentControlSet\Services\` con `Type = 1`. |
| **Lógica de detección** | Regla Sysmon: Event ID 6 con `Signed = false` → nivel 10. Crítica: Event ID 6 con `SignatureStatus = Revoked` o `Expired` → nivel 12. Correlación: driver no firmado + Event ID 4672 (privilegios especiales) en 60s → nivel 12. Regla Security log: Event ID 7045 con `ServiceType = kernel driver` desde proceso no de actualización de sistema → nivel 10. |
| **MITRE ATT&CK** | T1014 — Rootkit / T1543.003 — Create or Modify System Process: Windows Service |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — Sysmon Event ID 6 con `Signed = false` es de alta precisión. |
| **Falsos positivos** | Bajos. Drivers sin firma son raros en sistemas modernos de 64 bits. Whitelist por `ImageLoaded` de drivers conocidos y validados. |
| **Recomendación de hardening** | Activar Secure Boot y HVCI (Hypervisor-Protected Code Integrity) — impide la carga de drivers no firmados incluso con privilegios de administrador. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.DRV.002 — BYOVD: driver legítimo vulnerable usado para evasión o escalada

| Campo | Detalle |
|---|---|
| **Descripción** | El atacante carga un driver legítimo pero con vulnerabilidades conocidas (BYOVD — Bring Your Own Vulnerable Driver) para explotar esas vulnerabilidades desde el kernel: desactivar controles de seguridad (EDR, AV), escalar privilegios o leer/escribir memoria del kernel. El driver está firmado correctamente — lo que lo hace difícil de detectar por firma — pero proviene de software de terceros vulnerable (ej. `gdrv.sys` de GIGABYTE, `AsrDrv.sys` de ASRock, `mhyprot2.sys` de miHoYo). Técnica cada vez más frecuente en malware avanzado y ransomware. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 6 — `ImageLoaded` con nombre de driver vulnerable conocido, hash comparado contra lista de hashes BYOVD conocidos. Security log — Event ID 7045 con `ImagePath` apuntando a driver en ruta temporal o de usuario. |
| **Lógica de detección** | Regla Sysmon: Event ID 6 con `ImageLoaded` conteniendo nombre de driver BYOVD conocido (`gdrv.sys`, `AsrDrv103.sys`, `mhyprot2.sys`, `DBUtil_2_3.sys`, `Nal.sys`, `WinIo64.sys`) → nivel 12. Regla por hash: Event ID 6 con `Hashes` que coincida con CDB list de hashes BYOVD → nivel 12. Contextual: driver firmado por fabricante de hardware cargado desde `%TEMP%` → nivel 10. Correlación: carga de driver BYOVD + desaparición de proceso EDR en 300s → nivel 12 (kill EDR confirmado). |
| **MITRE ATT&CK** | T1068 — Exploitation for Privilege Escalation / T1562.001 — Disable or Modify Tools / T1014 — Rootkit |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — detección por nombre directa pero atacantes renombran los drivers. Detección por hash más robusta — requiere mantener actualizada la CDB list (fuente: LOLDrivers.io). |
| **Falsos positivos** | Medios por nombre (el mismo driver puede tener uso legítimo). Bajos por hash y ruta anómala. |
| **Nota operativa** | Mantener actualizada la lista de drivers BYOVD es una tarea operativa continua. LOLDrivers.io mantiene un repositorio público con hashes. Si se detecta BYOVD + kill de EDR, el sistema está efectivamente ciego — escalar a P1 inmediatamente y aislar el endpoint. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.DRV.003 — Driver instalado desde ruta anómala o por proceso no autorizado

| Campo | Detalle |
|---|---|
| **Descripción** | Se instala un driver de kernel desde una ruta anómala (directorio temporal, de usuario, de descarga) o el proceso que lo instala no es una herramienta de administración autorizada. Los drivers legítimos se instalan en `C:\Windows\System32\drivers\` mediante instaladores firmados — cualquier driver instalado fuera de este flujo es sospechoso independientemente de su estado de firma. Complementa DRV.001 y DRV.002 con un enfoque en el contexto de instalación. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 6 — `ImageLoaded` con ruta fuera de `C:\Windows\System32\drivers\` o `C:\Windows\SysWOW64\drivers\`. Security log — Event ID 7045 con `ImagePath` en `%TEMP%`, `%APPDATA%`, `C:\Users\` o `C:\ProgramData\`. Sysmon Event ID 1 — `sc.exe` con `type= kernel` y ruta anómala, o `PnPutil.exe` con `/add-driver` apuntando a ruta temporal. Sysmon Event ID 11 — creación de fichero `.sys` en ruta de usuario por proceso no instalador. |
| **Lógica de detección** | Regla Sysmon: Event ID 6 con `ImageLoaded` fuera de `C:\Windows\System32\drivers\` → nivel 10. Crítica: mismo patrón + `Signed = false` → nivel 12. Regla Security log: Event ID 7045 con `ServiceType = kernel driver` e `ImagePath` en `%TEMP%` o `C:\Users\` → nivel 12. Regla Event ID 1: `sc.exe` con `type= kernel` desde proceso interactivo → nivel 10. |
| **MITRE ATT&CK** | T1543.003 — Create or Modify System Process: Windows Service / T1014 — Rootkit |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — verificación de ruta directa con los campos `ImagePath` y `ImageLoaded`. |
| **Falsos positivos** | Bajos. Posibles FP con herramientas de virtualización (VMware, VirtualBox) — whitelist de rutas de instalación conocidas. |
| **Nota operativa** | La combinación de DRV.001, DRV.002 y DRV.003 proporciona cobertura en capas: sin firma, con firma pero vulnerable, y en ruta anómala. Un driver malicioso sofisticado puede evadir una capa pero difícilmente las tres simultáneamente. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (DLL Hijacking)

---

###### EP.03.WIN.DLL.001 — DLL Search Order Hijacking

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante coloca una DLL maliciosa en una ruta que Windows busca antes que la ruta donde se encuentra la DLL legítima. Windows sigue un orden de búsqueda predefinido al cargar DLLs (directorio de la aplicación, System32, SysWOW64, PATH...) — si el atacante puede escribir en el directorio de la aplicación o en una ruta de PATH anterior a System32, su DLL maliciosa se carga en lugar de la legítima. Técnica frecuente para persistencia y escalada de privilegios cuando la aplicación víctima se ejecuta con privilegios elevados. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 7 (Image Loaded) — nombre de DLL del sistema cargada desde ruta distinta a `C:\Windows\System32\` o `C:\Windows\SysWOW64\`. Campos clave: `Image`, `ImageLoaded`, `Signed`, `SignatureStatus`. Sysmon Event ID 11 — creación de `.dll` en directorio de aplicación o PATH por proceso no instalador. |
| **Lógica de detección** | Regla Sysmon: Event ID 7 con nombre de DLL de sistema conocida (`version.dll`, `wininet.dll`, `dbghelp.dll`, `wtsapi32.dll`, `dwrite.dll`) cargada desde ruta fuera de System32 → nivel 10. Crítica: misma DLL cargada desde `%TEMP%`, `%APPDATA%` o directorio de usuario → nivel 12. Regla Event ID 11: creación de `.dll` con nombre de DLL de sistema en directorio de aplicación por proceso no instalador → nivel 10. Correlación: creación de `.dll` en directorio de aplicación + carga de esa DLL por la aplicación en 300s → nivel 12. |
| **MITRE ATT&CK** | T1574.001 — Hijack Execution Flow: DLL Search Order Hijacking |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — el volumen de Event ID 7 puede ser muy alto. La clave es filtrar por DLLs de sistema cargadas desde rutas no estándar. Whitelist de aplicaciones que legítimamente cargan DLLs desde rutas no estándar. |
| **Falsos positivos** | Medios. Algunas aplicaciones legítimas incluyen versiones propias de DLLs del sistema en su directorio. Whitelist por `Image` + `ImageLoaded` de combinaciones conocidas. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.DLL.002 — DLL Sideloading

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante coloca una DLL maliciosa junto a un ejecutable legítimo y de confianza que carga DLLs por nombre sin verificar su ruta o firma. La aplicación legítima actúa como proxy para ejecutar el código malicioso — dado que el proceso padre es legítimo, muchas soluciones de seguridad no inspeccionan las DLLs que carga. Técnica muy frecuente en APTs y malware avanzado (abusar de `onedrive.exe`, `teams.exe`, `msiexec.exe`, aplicaciones de seguridad de terceros). |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 7 — aplicación legítima cargando DLL no firmada o con firma de fabricante diferente al ejecutable principal. Campos clave: `Image` (ejecutable legítimo), `ImageLoaded` (DLL cargada), `Signed`. Sysmon Event ID 11 — DLL creada en mismo directorio que ejecutable legítimo por proceso no relacionado con la aplicación. |
| **Lógica de detección** | Regla Sysmon: Event ID 7 con `Image` firmado por Microsoft + `ImageLoaded` con `Signed = false` desde mismo directorio → nivel 10. Crítica: ejecutable legítimo de sistema (`onedrive.exe`, `teams.exe`, `calc.exe`) cargando DLL no firmada desde su directorio → nivel 12. Regla Event ID 11: creación de `.dll` en directorio de aplicación de Microsoft por proceso no del fabricante → nivel 10. |
| **MITRE ATT&CK** | T1574.002 — Hijack Execution Flow: DLL Side-Loading |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — filtrado de ejecutables legítimos cargando DLLs no firmadas requiere whitelist exhaustiva. La correlación por directorio compartido entre ejecutable y DLL es el discriminador más efectivo. |
| **Falsos positivos** | Medios. Algunas aplicaciones legítimas incluyen DLLs propias sin firma. La combinación ejecutable de Microsoft + DLL no firmada en mismo directorio reduce los FP significativamente. |
| **Nota operativa** | DLL sideloading es especialmente difícil de detectar porque el proceso visible es un ejecutable legítimo y de confianza. SentinelOne debería aportar cobertura adicional mediante inspección del comportamiento de la DLL cargada. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.DLL.003 — Phantom DLL Hijacking

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante coloca una DLL en una ruta donde una aplicación intenta cargarla pero no existe — la aplicación falla silenciosamente en la carga sin que sea crítico para su funcionamiento, pero si el atacante coloca la DLL en esa ruta, se ejecuta su código. Más sigilosa que DLL search order hijacking porque no reemplaza ninguna DLL existente. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 7 — DLL cargada con `Signed = false` desde directorio de aplicación o System32 que no corresponde a ninguna DLL conocida del sistema. Sysmon Event ID 11 — creación de `.dll` con nombre no reconocido en directorio de aplicación o System32 por proceso no instalador. |
| **Lógica de detección** | Regla Sysmon: Event ID 11 — creación de `.dll` en `C:\Windows\System32\` por proceso que no sea `TrustedInstaller`, `msiexec.exe` o instalador firmado → nivel 12. Regla Event ID 7: DLL cargada con nombre no en lista de DLLs conocidas del sistema desde System32 → nivel 10. Correlación: creación de DLL en System32 por proceso no autorizado + carga de esa DLL en 300s → nivel 12. |
| **MITRE ATT&CK** | T1574.001 — Hijack Execution Flow: DLL Search Order Hijacking |
| **Severidad** | Alta |
| **Esfuerzo** | Alto — requiere lista de DLLs legítimas del sistema para detectar DLLs anómalas. La creación en System32 por procesos no autorizados es el indicador más fiable. |
| **Falsos positivos** | Bajos para creación en System32 por proceso no autorizado. Medios para detección por nombre de DLL desconocida. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.DLL.004 — DLL de sistema sobrescrita o reemplazada

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante sobrescribe o reemplaza una DLL legítima del sistema con una versión maliciosa que mantiene la interfaz de exportación original pero añade código malicioso. A diferencia de las técnicas anteriores, la DLL maliciosa está en la ruta correcta (`C:\Windows\System32\`) — la detección depende de cambios en el hash, firma o fecha de modificación. FIM es la fuente de detección principal. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 7.2 Modificación no autorizada de información |
| **Peligrosidad** | ALTO |
| **Telemetría** | FIM — Wazuh syscheck detectando modificación de `.dll` en `C:\Windows\System32\` o `C:\Windows\SysWOW64\` (cambio de hash MD5/SHA256, tamaño o fecha). Sysmon Event ID 11 — escritura en `.dll` existente en System32 por proceso no `TrustedInstaller` o Windows Update. Sysmon Event ID 7 — DLL de sistema cargada con `SignatureStatus = Invalid`. |
| **Lógica de detección** | Regla FIM: modificación de cualquier `.dll` en `C:\Windows\System32\` con cambio de hash → nivel 10. Crítica: modificación de DLL crítica del sistema (`ntdll.dll`, `kernel32.dll`, `advapi32.dll`, `ws2_32.dll`) → nivel 12. Regla Sysmon Event ID 11: escritura en `.dll` existente en System32 por proceso distinto a `TrustedInstaller.exe` → nivel 12. Correlación: modificación de DLL + `SignatureStatus = Invalid` en 300s → nivel 12. |
| **MITRE ATT&CK** | T1574.001 — DLL Search Order Hijacking / T1565.001 — Stored Data Manipulation |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — FIM sobre System32 puede generar ruido con Windows Update. Whitelist de procesos autorizados para modificar System32 (`TrustedInstaller`, `MpSigStub.exe`, agentes de patch management). |
| **Falsos positivos** | Medios. Windows Update modifica DLLs de sistema frecuentemente. Whitelist de procesos autorizados esencial. |
| **Nota operativa** | Si se detecta modificación de `ntdll.dll` o `kernel32.dll` por proceso no autorizado, tratar como compromiso de máxima gravedad — estas DLLs son cargadas por prácticamente todos los procesos del sistema. Aislar el endpoint inmediatamente sin intentar remediación en caliente. |
| **Estado** | Pendiente de validación. |

---

##### EP-04 — Robo o abuso de credenciales

---

###### EP.04.WIN.AUTH.002 — Brute force de login local (consola / teclado)

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de varios intentos fallidos de login local sobre el mismo endpoint. Caso típico de un atacante con acceso físico o sesión RDP ya iniciada que prueba contraseñas adicionales. |
| **Clasificación GrayHats** | 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Canal Security — Event ID 4625 con `ipAddress` = `"-"`, `"::1"` o `"127.0.0.1"` (login local sin origen de red). |
| **Lógica de detección** | Regla custom 100100 (Anexo B). Correla 5 eventos 60122 en 180s con `ipAddress` local. Necesaria porque la 60204 estándar agrupa por IP y no detecta este patrón. |
| **MITRE ATT&CK** | T1110.001 — Password Guessing |
| **Severidad** | Media-Alta |
| **Esfuerzo** | Bajo — una regla custom de aprox. 10 líneas en `local_rules.xml`. |
| **Falsos positivos** | Bajos. Usuarios despistados pueden generar 2-3 fallos legítimos; el umbral de 5 lo absorbe. |
| **Limitación** | Aplica solo a autenticación con contraseña. En endpoints solo-Hello (PIN/biometría) requiere telemetría adicional (Windows (Sysmon + SentinelOne)). |

---

###### EP.04.WIN.IDM.003 — Modificación de cuenta de usuario

| Campo | Detalle |
|---|---|
| **Descripción** | Se modifica una cuenta de usuario (cambio de nombre, atributos, flags como "Password never expires", deshabilitación). Indicador de manipulación de cuentas para evasión o persistencia. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4738 (A user account was changed). |
| **Lógica de detección** | Regla built-in 60110 (nivel 8). |
| **MITRE ATT&CK** | T1098 — Account Manipulation |
| **Severidad** | Media |
| **Esfuerzo** | Bajo — built-in. |
| **Falsos positivos** | Bajos. |

---

###### EP.04.WIN.IDM.004 — Cambio de contraseña realizado por otro usuario

| Campo | Detalle |
|---|---|
| **Descripción** | Una cuenta tiene su contraseña reseteada por otro usuario (no por el propio titular). Comportamiento legítimo en helpdesk; anómalo en otros contextos y técnica común tras compromiso de cuenta administrativa. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4724 (An attempt was made to reset an account password). |
| **Lógica de detección** | Regla built-in 60157 (nivel 3 — no se indexa). Requiere reglas custom de correlación (Anexo D) para casos relevantes: combinaciones con creación reciente, fuera de horario, fuera de whitelist de helpdesk. |
| **MITRE ATT&CK** | T1098 — Account Manipulation |
| **Severidad** | Media |
| **Esfuerzo** | Medio — diseño de reglas custom de correlación. |
| **Falsos positivos** | Medios. Whitelist de cuentas de helpdesk autorizadas. |

---

##### EP-08 — Comportamiento anómalo del usuario o del equipo

---

###### EP.08.WIN.AUTH.004 — Login interactivo con cuenta privilegiada

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario con privilegios administrativos inicia sesión interactivamente. Normal en helpdesk; anómalo si sucede fuera de ventanas previstas o sobre PCs de usuario final. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4624 (LogonType 2 o 10) seguido de 4672 (Special privileges assigned to new logon). |
| **Lógica de detección** | Reglas built-in 67028 (nivel 3) y derivadas. Requiere refinamiento con regla custom de correlación 4624+4672 + whitelist horaria (Anexo D). |
| **MITRE ATT&CK** | T1078 — Valid Accounts |
| **Severidad** | Media |
| **Esfuerzo** | Medio — la regla existe pero requiere tuning según la política de acceso del cliente. |
| **Falsos positivos** | Medios. Requiere whitelist de cuentas administrativas conocidas y franjas horarias permitidas. |

---

##### EP-09 — Violación de políticas de seguridad

---

###### EP.09.WIN.FIM.001 — Modificación de ficheros críticos del sistema

| Campo | Detalle |
|---|---|
| **Descripción** | Modificación, creación o eliminación de ficheros en directorios sensibles del SO (System32, drivers, fichero hosts, carpeta Startup). Indicador de malware con persistencia, manipulación de DNS local o tampering del sistema. |
| **Clasificación GrayHats** | 7.2 Modificación no autorizada de información / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Módulo File Integrity Monitoring nativo del agente (no requiere reglas custom; se configura en el bloque `<syscheck>`). |
| **Lógica de detección** | Reglas built-in 550 (file added, nivel 5), 553 (deleted, nivel 7), 554 (modified, nivel 7). |
| **MITRE ATT&CK** | T1565.001 — Stored Data Manipulation |
| **Severidad** | Media |
| **Esfuerzo** | Bajo — solo configurar paths a monitorizar en `agent.conf`. |
| **Falsos positivos** | Medios. Windows Update genera ruido en System32; mitigación con frecuencia diaria y whitelist de patrones. |

---

##### EP-10 — Manipulación defensiva y evasión

---

###### EP.10.WIN.AUDIT.001 — Limpieza del log de auditoría de seguridad

| Campo | Detalle |
|---|---|
| **Descripción** | Alguien ha vaciado el log de Seguridad de Windows. Acción raramente legítima y técnica directa de borrado de evidencias tras una intrusión. Bandera roja de máxima prioridad. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.2 Modificación no autorizada de información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 1102 (The audit log was cleared). |
| **Lógica de detección** | Regla built-in 60148 (nivel 12). |
| **MITRE ATT&CK** | T1070.001 — Clear Windows Event Logs |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — built-in. |
| **Falsos positivos** | Prácticamente nulos. Cada 1102 debe investigarse sin excepción. |

---

###### EP.10.WIN.AUDIT.002 — Modificación de la política de auditoría

| Campo | Detalle |
|---|---|
| **Descripción** | Se ha cambiado la política de auditoría del sistema (qué eventos se registran). Técnica de evasión: el atacante intenta dejar de generar logs antes de actuar. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4719 (System audit policy was changed). |
| **Lógica de detección** | Regla built-in 60112 (nivel 8). |
| **MITRE ATT&CK** | T1562.002 — Disable Windows Event Logging |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. |
| **Falsos positivos** | Bajos. Cambios legítimos suceden en bastión de configuración (descartable por hostname). |

---

###### EP.10.WIN.AV.001 — Microsoft Defender deshabilitado o manipulado

| Campo | Detalle |
|---|---|
| **Descripción** | Se ha detenido el servicio de Microsoft Defender, deshabilitado la protección en tiempo real, o añadido exclusiones a la configuración. Técnica de evasión de defensas: desactivar el antivirus antes de ejecutar el payload. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Microsoft-Windows-Windows Defender/Operational — Event IDs 5001 (RT protection disabled), 5004 (RT protection feature configuration changed), 5007 (Configuration changed). Canal System — Event ID 7036 con servicio WinDefend en estado stopped. |
| **Lógica de detección** | Reglas built-in del grupo `windows_defender` (nivel 9-12). |
| **MITRE ATT&CK** | T1562.001 — Disable or Modify Tools |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — solo añadir el canal Defender al `agent.conf`. |
| **Aplicabilidad** | No aplica en endpoints con EDR de terceros (SentinelOne, CrowdStrike). Cubierto por reglas del EDR correspondiente. |

---



---

#### EP-02 — Intrusión o compromiso del endpoint

> ¿Alguien está usando el endpoint como punto de entrada o pivote?

---

##### Fichas detalladas — EP-02 (Ejecución remota sospechosa)

---

###### EP.02.WIN.EXEC.001 — Ejecución remota mediante PsExec / herramientas Sysinternals

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa PsExec u otras herramientas de Sysinternals (PsExec64, paexec, remcom) para ejecutar comandos o procesos en el endpoint de forma remota. PsExec es una de las técnicas de movimiento lateral más frecuentes en ataques reales — instala un servicio temporal (PSEXESVC) en el sistema destino y ejecuta el payload bajo ese servicio. La detección combina la creación del servicio, el proceso hijo resultante y la autenticación de red asociada. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | (1) Security log — Event ID 7045 (servicio PSEXESVC instalado) o Event ID 4697. (2) Sysmon Event ID 1 (Process Create) — `Image` = `psexesvc.exe` o proceso hijo con `ParentImage` = `psexesvc.exe`. (3) Security log — Event ID 4624 (LogonType 3, red) + Event ID 4648 (explicit credentials) desde IP de origen. (4) Sysmon Event ID 13 (Registry value set) — clave de servicio PSEXESVC en `HKLM\SYSTEM\CurrentControlSet\Services`. |
| **Lógica de detección** | Regla built-in Wazuh 61138 (instalación de servicio, nivel 5 — recomendado overwrite a 8). Regla custom de alta confianza: Event ID 7045 con `ServiceName = PSEXESVC` → nivel 12. Regla Sysmon: `ParentImage` = `psexesvc.exe` con cualquier proceso hijo → nivel 12. Correlación: 4624 LogonType 3 + 7045 PSEXESVC desde mismo origen en 30s → nivel 12 (ejecución remota confirmada). Regla adicional: nombre de imagen que contenga `psexec`, `paexec`, `remcom` (case-insensitive) → nivel 10. |
| **MITRE ATT&CK** | T1569.002 — System Services: Service Execution / T1021.002 — Remote Services: SMB/Windows Admin Shares / T1543.003 — Create or Modify System Process |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo-Medio — la detección del servicio PSEXESVC es built-in. Las reglas Sysmon de proceso hijo requieren desarrollo custom pero son de alta confianza. |
| **Falsos positivos** | Bajos. PsExec tiene uso legítimo en administración de sistemas — whitelist de IPs de origen de equipos de IT/helpdesk. Cualquier uso desde IP no autorizada es sospechoso. |
| **Relación con otros CU** | Correlacionar con EP.02.WIN.AUTH.001 (brute force previo desde la misma IP) y EP.03.WIN.PERS.* (el atacante puede instalar persistencia tras ejecutar código). Si SentinelOne genera alerta simultánea (EP.01.WIN.AV.001), escalar a incidente crítico inmediato. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXEC.002 — Ejecución remota mediante WMI

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa Windows Management Instrumentation (WMI) de forma remota para ejecutar procesos en el endpoint: `wmic /node:TARGET process call create`, `Invoke-WmiMethod`, `Win32_Process.Create`. WMI es una técnica de ejecución remota muy frecuente en ataques avanzados porque no requiere copiar herramientas al disco (fileless), usa un protocolo legítimo del sistema (DCOM/RPC) y genera menos ruido que PsExec. El proceso resultante es hijo de `WmiPrvSE.exe`. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | (1) Sysmon Event ID 1 (Process Create) — `ParentImage` = `WmiPrvSE.exe` con proceso hijo sospechoso (cmd.exe, powershell.exe, cscript.exe, cualquier ejecutable en ruta anómala). (2) Sysmon Event ID 20 (WmiEvent ActivityId Filter) y Event ID 21 (WmiEvent Consumer) — creación de suscripciones WMI persistentes. (3) Security log — Event ID 4624 LogonType 3 desde IP origen + Event ID 4648 si usa credenciales explícitas. |
| **Lógica de detección** | Regla Sysmon de alta confianza: `ParentImage` = `C:\Windows\System32\wbem\WmiPrvSE.exe` con `Image` = `cmd.exe`, `powershell.exe`, `cscript.exe`, `wscript.exe`, `mshta.exe` → nivel 12. Regla adicional: `ParentImage` = `WmiPrvSE.exe` con `Image` en ruta fuera de `C:\Windows\` o `C:\Program Files\` → nivel 12. Correlación: 4624 LogonType 3 + WmiPrvSE spawneando proceso en 60s desde mismo origen → nivel 12. |
| **MITRE ATT&CK** | T1047 — Windows Management Instrumentation / T1021.006 — Remote Services: Windows Remote Management |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — requiere Sysmon con configuración que capture `ParentImage` correctamente. El volumen de procesos hijo de WmiPrvSE legítimos puede ser alto — whitelist esencial. |
| **Falsos positivos** | Medios. WmiPrvSE spawnea procesos legítimos en operaciones de gestión de sistema. La clave es filtrar por procesos hijo sospechosos (intérpretes de comandos, ejecutables en rutas anómalas). |
| **Nota operativa** | WMI remoto no deja artefactos en disco del atacante — el payload se ejecuta directamente en memoria del sistema destino. Los artefactos forenses estarán principalmente en los logs de Sysmon y en el registro de WMI (`C:\Windows\System32\wbem\Repository`). |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXEC.003 — Ejecución remota mediante PowerShell / WinRM

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa PowerShell Remoting (WinRM) para ejecutar comandos en el endpoint: `Invoke-Command`, `Enter-PSSession`, `New-PSSession`. WinRM usa el puerto 5985 (HTTP) o 5986 (HTTPS) y ejecuta los comandos bajo el proceso `wsmprovhost.exe`. Es una técnica frecuente en movimiento lateral en entornos con PowerShell Remoting habilitado. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | (1) Sysmon Event ID 1 — `ParentImage` = `wsmprovhost.exe` con proceso hijo (cmd.exe, powershell.exe, cualquier payload). (2) Security log — Event ID 4624 LogonType 3 desde IP origen en puerto 5985/5986. (3) PowerShell Operational log (Microsoft-Windows-PowerShell/Operational) — Event ID 4103 (Module logging) y 4104 (ScriptBlock logging) con contenido del comando ejecutado. (4) Sysmon Event ID 3 — conexión entrante en puerto 5985/5986. |
| **Ingesta en Wazuh** | Añadir canal `Microsoft-Windows-PowerShell/Operational` al `agent.conf`. Activar ScriptBlock logging vía GPO: `HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging = 1`. |
| **Lógica de detección** | Regla Sysmon: `ParentImage` = `wsmprovhost.exe` con proceso hijo sospechoso → nivel 12. Regla PowerShell ScriptBlock: Event ID 4104 con contenido que incluya `IEX`, `Invoke-Expression`, `DownloadString`, `EncodedCommand`, `FromBase64String` → nivel 10-12. Correlación: 4624 LogonType 3 puerto 5985 + wsmprovhost spawneando proceso en 30s → nivel 12. |
| **MITRE ATT&CK** | T1021.006 — Remote Services: Windows Remote Management / T1059.001 — Command and Scripting Interpreter: PowerShell |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — requiere activar ScriptBlock logging en GPO y añadir el canal PS/Operational a Wazuh. Las reglas Sysmon de wsmprovhost son de alta confianza. |
| **Falsos positivos** | Medios. WinRM tiene uso legítimo en administración remota (Ansible, DSC, scripts de IT). Whitelist de IPs de servidores de gestión autorizados. |
| **Ventaja de ScriptBlock logging** | Permite ver el contenido exacto del comando ejecutado remotamente, incluyendo payloads ofuscados que PowerShell desobfusca antes de ejecutar. Esencial para investigación forense. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXEC.004 — Ejecución remota mediante Scheduled Task

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante crea una tarea programada de forma remota en el endpoint para ejecutar un payload: `schtasks /create /s TARGET`, `Register-ScheduledTask` remoto, o usando la API de Task Scheduler vía RPC. A diferencia de la persistencia local (EP.03.WIN.PERS.002), este caso se focaliza en la creación remota como técnica de ejecución lateral — el atacante crea la tarea desde otro sistema comprometido para pivotar al endpoint destino. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | (1) Security log — Event ID 4698 (Scheduled task created) con campo `SubjectUserName` distinto al usuario local y `TaskContent` con XML de la tarea. (2) Security log — Event ID 4624 LogonType 3 desde IP origen precediendo la creación de la tarea. (3) Sysmon Event ID 1 — proceso `schtasks.exe` con argumento `/create` y `/s` (remoto) o proceso hijo de `taskeng.exe`/`svchost.exe` sospechoso. (4) Microsoft-Windows-TaskScheduler/Operational — Event ID 106 (task registered) y 200 (action started). |
| **Lógica de detección** | Regla built-in 60228 (task created, nivel 4 — recomendado overwrite a 8). Regla custom de alta confianza: Event ID 4698 con `SubjectLogonId` que corresponda a una sesión LogonType 3 reciente → nivel 12. Regla Sysmon: `schtasks.exe` con argumento `/s` (sistema remoto) → nivel 10. Correlación: 4624 LogonType 3 + 4698 en mismo `SubjectLogonId` en 120s → nivel 12. |
| **MITRE ATT&CK** | T1053.005 — Scheduled Task/Job: Scheduled Task / T1021 — Remote Services |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — la correlación LogonType 3 + creación de tarea requiere regla custom que cruce el `SubjectLogonId` entre dos eventos distintos. |
| **Falsos positivos** | Medios. Herramientas de gestión remota (SCCM, Ansible, scripts de administración) crean tareas remotas legítimamente. Whitelist de cuentas de servicio autorizadas y servidores de gestión. |
| **Diferencia con EP.03.WIN.PERS.002** | EP.03.WIN.PERS.002 detecta cualquier creación de tarea como indicador de persistencia. Esta ficha se focaliza en la creación remota como técnica de ejecución lateral — el contexto de sesión de red es el indicador diferenciador. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXEC.005 — Correlación transversal: ejecución remota multi-vector

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa múltiples técnicas de ejecución remota contra el mismo endpoint en una ventana de tiempo corta, o el mismo origen usa distintos vectores contra múltiples endpoints. Patrón de movimiento lateral agresivo o de un operador probando distintas técnicas tras obtener credenciales válidas. La correlación transversal eleva la confianza a incidente confirmado y permite identificar el endpoint de origen del atacante. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.02.WIN.EXEC.001-004 compartiendo `src_ip` (IP origen de la sesión de red) o `SubjectLogonId` (mismo contexto de autenticación) en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: 2+ alertas de distintas fichas EXEC.00* con el mismo `src_ip` en ventana de 300s → nivel 12 (movimiento lateral multi-vector activo). Regla adicional: mismo `src_ip` con eventos EXEC.00* contra 2+ `dst_ip` distintos en 600s → nivel 12 (pivotaje lateral desde endpoint comprometido hacia múltiples destinos). |
| **MITRE ATT&CK** | T1021 — Remote Services / T1570 — Lateral Tool Transfer / T1110 — Brute Force |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que las fichas EXEC.001-004 estén operativas y los campos IP normalizados entre fuentes. |
| **Falsos positivos** | Muy bajos. La combinación de múltiples técnicas de ejecución remota desde el mismo origen en ventana corta es prácticamente siempre indicativa de movimiento lateral activo. |
| **Nota operativa** | Cuando dispara esta regla, el endpoint origen (`src_ip`) es el pivote comprometido — la investigación debe arrancar ahí, no solo en el destino. Contener ambos endpoints simultáneamente. |
| **Prerequisito** | Fichas EP.02.WIN.EXEC.001-004 operativas y campos IP normalizados. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-02 (Acceso con credenciales robadas)

---

###### EP.02.WIN.CRED.001 — Credential dumping: acceso a LSASS

| Campo | Detalle |
|---|---|
| **Descripción** | Un proceso intenta acceder a la memoria del proceso LSASS (Local Security Authority Subsystem Service) para extraer credenciales en texto claro, hashes NTLM o tickets Kerberos. LSASS almacena las credenciales de los usuarios con sesión activa en el sistema. Sin PPL ni Credential Guard, cualquier proceso con privilegios suficientes puede leer su memoria. Técnica fundamental de casi todos los ataques avanzados — sin credenciales el movimiento lateral es muy limitado. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 10 (ProcessAccess) — campos clave: `TargetImage` = `C:\Windows\System32\lsass.exe`, `SourceImage` (proceso atacante), `GrantedAccess` (máscara de acceso solicitada). Accesos sospechosos: `GrantedAccess` con flags `0x1010`, `0x1410`, `0x1438`, `0x143a`, `0x1FFFFF`. Complementariamente Sysmon Event ID 1: proceso `procdump.exe`, `mimikatz.exe`, `nanodump.exe`, `lsassy` con argumento apuntando a lsass. |
| **Lógica de detección** | Regla Sysmon alta confianza: Event ID 10 con `TargetImage = lsass.exe` y `GrantedAccess` conteniendo flags de lectura de memoria desde proceso no firmado o fuera de rutas de sistema → nivel 12. Regla por nombre de herramienta: `SourceImage` conteniendo `mimikatz`, `procdump`, `nanodump`, `pypykatz`, `lsassy` → nivel 12. Regla de correlación: Event ID 10 a lsass + Event ID 3 (conexión saliente) desde mismo proceso en 60s → nivel 12 (dumping + exfiltración inmediata). |
| **MITRE ATT&CK** | T1003.001 — OS Credential Dumping: LSASS Memory |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — requiere Sysmon con configuración que capture Event ID 10 correctamente. Whitelist de procesos firmados de sistema imprescindible. |
| **Falsos positivos** | Medios para regla genérica de acceso a LSASS. Muy bajos para reglas por nombre de herramienta conocida. SentinelOne debería detectar mimikatz y variantes de forma independiente. |
| **Recomendación de hardening** | Activar PPL para LSASS vía registro: `HKLM\SYSTEM\CurrentControlSet\Control\Lsa\RunAsPPL = 1`. Activar Credential Guard en endpoints Windows 10/11 con Hyper-V. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.CRED.002 — Pass-the-Hash

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa el hash NTLM de una cuenta (obtenido mediante credential dumping) para autenticarse en otros sistemas sin conocer la contraseña en texto claro. El hash NTLM es suficiente para autenticarse en servicios que usan NTLM — SMB, WMI, WinRM. La detección se realiza desde el DC o el sistema destino analizando el patrón de autenticación: LogonType 3 con autenticación NTLM desde una IP que no es el equipo habitual del usuario. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log en el DC o sistema destino — Event ID 4624 con `LogonType = 3` y `AuthenticationPackageName = NTLM`. Campos clave: `SubjectUserName`, `IpAddress` (origen), `WorkstationName`, `LogonProcessName = NtLmSsp`. Complementariamente Event ID 4776 (NTLM authentication attempt) en el DC. |
| **Lógica de detección** | Regla custom: Event ID 4624 con `LogonType = 3` + `AuthenticationPackageName = NTLM` + `IpAddress` distinta al equipo habitual del usuario → nivel 8. Correlación de alta confianza: misma cuenta con 4624 NTLM LogonType 3 desde múltiples IPs distintas en 300s → nivel 12 (hash siendo usado desde varios sistemas). Regla adicional: 4624 NTLM desde IP que previamente generó alerta de credential dumping (EP.02.WIN.CRED.001) → nivel 12. |
| **MITRE ATT&CK** | T1550.002 — Use Alternate Authentication Material: Pass the Hash |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — la detección individual requiere distinguir NTLM de Kerberos en los logs. La correlación multi-IP requiere regla custom con estado. |
| **Falsos positivos** | Medios. NTLM se usa legítimamente cuando Kerberos no está disponible. La clave es detectar NTLM desde IPs no habituales para ese usuario. |
| **Nota operativa** | En entornos bien configurados la autenticación debería ser mayoritariamente Kerberos. Un alto volumen de autenticaciones NTLM es por sí mismo una señal de alerta. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.CRED.003 — Pass-the-Ticket

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante roba un ticket Kerberos (TGT o TGS) de la memoria de un endpoint comprometido y lo usa en otro sistema para autenticarse sin conocer la contraseña. Las variantes más comunes son Golden Ticket (TGT forjado con el hash de KRBTGT) y Silver Ticket (TGS forjado para un servicio específico). A diferencia de Pass-the-Hash, usa el protocolo Kerberos, lo que lo hace más difícil de detectar. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log en el DC — Event ID 4768 (TGT request), Event ID 4769 (TGS request), Event ID 4771 (Kerberos pre-authentication failed). Para Golden Ticket: Event ID 4624 con ticket Kerberos sin correspondencia con 4768 previo. Para Silver Ticket: ausencia de Event ID 4769 cuando debería haberlo. |
| **Lógica de detección** | **Sin auditoría Kerberos activa (situación actual):** cobertura muy limitada. **Con auditoría activada:** Event ID 4624 Kerberos LogonType 3 sin Event ID 4768 previo en el DC en los últimos 10 minutos → nivel 12 (posible Golden Ticket). Event ID 4769 con `TicketEncryptionType = 0x17` (RC4, cifrado débil usado por herramientas de ataque) → nivel 10. |
| **MITRE ATT&CK** | T1550.003 — Use Alternate Authentication Material: Pass the Ticket / T1558.001 — Golden Ticket / T1558.002 — Silver Ticket |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — requiere activar auditoría de Kerberos en los DCs y desarrollar reglas custom de correlación entre eventos de distintos sistemas. |
| **Prerequisito crítico** | Activar auditoría Kerberos en DCs: `auditpol /set /subcategory:"Kerberos Authentication Service" /success:enable /failure:enable` y `auditpol /set /subcategory:"Kerberos Service Ticket Operations" /success:enable /failure:enable`. Sin esto la cobertura es prácticamente nula. |
| **Estado** | Pendiente de validación. Requiere activar auditoría Kerberos en DCs. |

---

###### EP.02.WIN.CRED.004 — Kerberoasting

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante solicita tickets TGS para cuentas de servicio con SPN registrado y los extrae para atacarlos offline con fuerza bruta. Las cuentas de servicio suelen tener contraseñas estáticas sin expiración — si son débiles, el atacante obtiene credenciales de alta privilegio. La detección se realiza en el DC analizando solicitudes TGS inusuales con cifrado RC4. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log en el DC — Event ID 4769 (A Kerberos service ticket was requested) con `TicketEncryptionType = 0x17` (RC4-HMAC, cifrado débil que las herramientas de Kerberoasting solicitan deliberadamente) y `ServiceName` distinto a `krbtgt` o `$`. |
| **Lógica de detección** | **Sin auditoría Kerberos activa (situación actual):** cobertura nula. **Con auditoría activada:** Event ID 4769 con `TicketEncryptionType = 0x17` desde cuenta de usuario → nivel 10. Correlación: misma cuenta solicitando 5+ TGS con `EncryptionType = 0x17` para distintos servicios en 60s → nivel 12 (Kerberoasting automatizado con Rubeus o GetUserSPNs.py). |
| **MITRE ATT&CK** | T1558.003 — Steal or Forge Kerberos Tickets: Kerberoasting |
| **Severidad** | Alta |
| **Esfuerzo** | Alto — mismo prerequisito que EP.02.WIN.CRED.003: requiere activar auditoría Kerberos en los DCs. |
| **Prerequisito crítico** | Auditoría Kerberos activa en DCs (igual que EP.02.WIN.CRED.003). |
| **Recomendación de hardening** | Usar cuentas de servicio gestionadas (gMSA) que rotan automáticamente su contraseña. Configurar SPNs para usar AES en lugar de RC4 (`msDS-SupportedEncryptionTypes`). |
| **Estado** | Pendiente de validación. Requiere activar auditoría Kerberos en DCs. |

---

###### EP.02.WIN.CRED.005 — Herramientas de credential dumping conocidas

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de herramientas conocidas de extracción de credenciales ejecutadas en el endpoint: Mimikatz, Rubeus, Impacket, LaZagne, CrackMapExec, lsassy, Invoke-Mimikatz, SharpDump. La detección por nombre de herramienta o firma complementa EP.02.WIN.CRED.001 (que detecta el comportamiento de acceso a LSASS). SentinelOne debería detectar estas herramientas de forma independiente — esta ficha aporta la capa Sysmon como backstop si el EDR falla. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | (1) Sysmon Event ID 1 — `Image`, `OriginalFileName`, `Description`, `CommandLine` conteniendo nombres o argumentos de herramientas conocidas. (2) Sysmon Event ID 7 (Image Loaded) — DLLs características de Mimikatz (`wdigest.dll` cargada por proceso no esperado). (3) EP.01.WIN.AV.001 — alerta de SentinelOne sobre detección de herramienta de credential dumping. (4) FIM — creación de ficheros con nombres de herramientas conocidas en rutas temporales. |
| **Lógica de detección** | Regla Sysmon Event ID 1: `CommandLine` o `Image` conteniendo (case-insensitive): `mimikatz`, `sekurlsa`, `kerberos::`, `lsadump`, `rubeus`, `kerberoast`, `asreproast`, `lazagne`, `crackmapexec`, `lsassy`, `nanodump`, `sharpdump`, `pypykatz` → nivel 12. Regla Event ID 7: `ImageLoaded` = `wdigest.dll` desde proceso distinto a `lsass.exe` o `wininit.exe` → nivel 10. Correlación: alerta SentinelOne + Sysmon Event ID 10 a LSASS en mismo endpoint en 300s → nivel 12. |
| **MITRE ATT&CK** | T1003 — OS Credential Dumping / T1003.001 — LSASS Memory / T1558.003 — Kerberoasting |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo-Medio — la detección por nombre de herramienta es directa pero los atacantes sofisticados renombran los binarios. La detección por comportamiento es más robusta. |
| **Falsos positivos** | Muy bajos para nombres de herramientas de ataque conocidas. Medios para detección por comportamiento de DLLs. |
| **Nota operativa** | Si SentinelOne no detecta y Sysmon sí, investigar si el EDR está siendo evadido activamente — puede indicar un atacante sofisticado con capacidad de evasión de EDR. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.CRED.006 — Uso de credenciales robadas: login exitoso anómalo

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa credenciales obtenidas mediante credential dumping, phishing o compra en foros para autenticarse en sistemas corporativos. A diferencia de las fichas anteriores (que detectan el robo), esta ficha detecta el uso de esas credenciales — un login exitoso desde un contexto anómalo: IP no habitual, horario fuera de patrón, sistema de origen no esperado. Complementa EP.08.WIN.AUTH.004 con un enfoque más amplio de comportamiento anómalo. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4624 (login exitoso) con campos: `LogonType`, `IpAddress`, `WorkstationName`, `SubjectUserName`, `AuthenticationPackageName`, timestamp. Complementariamente Event ID 4648 (explicit credentials used) cuando se usan credenciales de otra cuenta. |
| **Lógica de detección** | Regla custom — login exitoso (4624) fuera del horario habitual entre 22:00 y 07:00 → nivel 8. Correlación: 4624 exitoso + 5+ fallos (4625) del mismo usuario en los 10 minutos previos desde misma IP → nivel 12 (credencial válida encontrada tras brute force). Regla de alta confianza: 4624 LogonType 3 de cuenta administrativa desde IP no identificada como servidor de gestión → nivel 12. Correlación avanzada: mismo usuario con 4624 exitoso desde dos IPs geográficamente distantes en menos de 2 horas → nivel 12 (impossible travel). |
| **MITRE ATT&CK** | T1078 — Valid Accounts / T1078.002 — Domain Accounts / T1078.003 — Local Accounts |
| **Severidad** | Alta / Crítica (según contexto) |
| **Esfuerzo** | Medio-Alto — las reglas individuales son moderadas. La correlación de impossible travel requiere geolocalización de IPs y retención de estado entre eventos. |
| **Falsos positivos** | Medios. Trabajo fuera de horario legítimo, VPNs que cambian la IP aparente, viajes de negocio. Proceso de excepción necesario. |
| **Relación con otros CU** | Cierra el ciclo completo: EP.02.WIN.CRED.001 (robo) → EP.02.WIN.CRED.002/003 (uso del hash/ticket) → EP.02.WIN.CRED.006 (login exitoso con las credenciales). Si las tres fichas disparan en secuencia desde el mismo origen, es un incidente confirmado de movimiento lateral. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-02 (Elevación de privilegios)

---

###### EP.02.WIN.PRIVESC.001 — Bypass de UAC (User Account Control)

| Campo | Detalle |
|---|---|
| **Descripción** | Un proceso intenta elevar sus privilegios sin mostrar el prompt UAC al usuario, usando técnicas de bypass conocidas. UAC es el mecanismo de Windows que solicita confirmación antes de ejecutar operaciones privilegiadas. Su bypass permite a malware con privilegios de usuario estándar obtener privilegios de administrador sin interacción del usuario. Técnicas comunes: eventvwr.exe hijacking, fodhelper.exe, ComputerDefaults.exe, DiskCleanup, token impersonation. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 (Process Create) — proceso conocido de bypass UAC (eventvwr.exe, fodhelper.exe, computerdefaults.exe, sdclt.exe) spawneando proceso hijo sospechoso (cmd.exe, powershell.exe, ejecutable en ruta anómala). Sysmon Event ID 13 (Registry value set) — modificación de claves de registro usadas en bypasses (ej. `HKCU\Software\Classes\mscfile\shell\open\command`). Security log — Event ID 4688 (Process creation) con `TokenElevationType = 2` (full token, elevación sin prompt). |
| **Lógica de detección** | Regla Sysmon alta confianza: `ParentImage` = `eventvwr.exe`, `fodhelper.exe`, `computerdefaults.exe`, `sdclt.exe` con proceso hijo fuera de rutas de sistema → nivel 12. Regla de registro: Event ID 13 con modificación de `HKCU\Software\Classes\*\shell\open\command` por proceso no administrativo → nivel 10. Regla Event ID 4688: proceso con `TokenElevationType = 2` (%%1937) iniciado desde proceso sin privilegios → nivel 10. |
| **MITRE ATT&CK** | T1548.002 — Abuse Elevation Control Mechanism: Bypass User Account Control |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — las reglas de proceso padre conocido son de alta confianza. La detección por registro requiere monitorización de claves específicas en la configuración de Sysmon. |
| **Falsos positivos** | Bajos. Los procesos conocidos de bypass UAC rara vez spawnean procesos interactivos en uso legítimo. |
| **Recomendación de hardening** | Configurar UAC en nivel máximo (siempre notificar). Gestionar los usuarios estándar sin derechos de administrador local. En entornos con Credential Guard, muchos bypasses UAC quedan neutralizados. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.PRIVESC.002 — Token impersonation / manipulación de tokens

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante roba o duplica el token de acceso de un proceso privilegiado para ejecutar código en ese contexto de seguridad — sin necesitar la contraseña del usuario privilegiado. Técnicas comunes: `SeImpersonatePrivilege` (JuicyPotato, RoguePotato, PrintSpoofer), `SeDebugPrivilege`, `CreateProcessWithToken`, `ImpersonateLoggedOnUser`. Muy frecuente tras comprometer una cuenta de servicio con SeImpersonatePrivilege. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — proceso `juicypotato.exe`, `roguepotato.exe`, `printspoofer.exe`, `godpotato.exe` o variantes. Security log — Event ID 4624 LogonType 2 o 3 con `ImpersonationLevel = Impersonation` o `Delegation` desde proceso de servicio. Event ID 4672 (Special privileges assigned) seguido de Event ID 4688 (proceso creado) desde cuenta de servicio no administrativa. Sysmon Event ID 8 (CreateRemoteThread) — inyección de hilo en proceso privilegiado para robar token. |
| **Lógica de detección** | Regla Sysmon: `Image` conteniendo `juicypotato`, `roguepotato`, `printspoofer`, `godpotato`, `sweetpotato` → nivel 12. Regla correlación: Event ID 4672 (privilegios especiales) desde cuenta de servicio + Event ID 4688 con proceso hijo sospechoso en 30s → nivel 12. Regla Sysmon Event ID 8: `CreateRemoteThread` desde proceso no firmado hacia `lsass.exe`, `winlogon.exe`, `services.exe` → nivel 12. |
| **MITRE ATT&CK** | T1134 — Access Token Manipulation / T1134.001 — Token Impersonation/Theft / T1134.002 — Create Process with Token |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — detección por nombre de herramienta directa. Detección por comportamiento (Event ID 8, correlación 4672+4688) requiere reglas custom con lógica de correlación. |
| **Falsos positivos** | Bajos para nombres de herramientas conocidas. Medios para detección por comportamiento (servicios legítimos usan impersonation). |
| **Nota operativa** | `SeImpersonatePrivilege` es concedido por defecto a cuentas de servicio IIS, SQL Server y servicios de red. Un atacante que comprometa cualquiera de estas cuentas puede escalar a SYSTEM con JuicyPotato o variantes. Auditar regularmente qué cuentas tienen este privilegio. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.PRIVESC.003 — Explotación de vulnerabilidad local para escalada de privilegios

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante explota una vulnerabilidad en el kernel de Windows, en un driver o en un servicio del sistema para elevar sus privilegios de usuario a SYSTEM o administrador. Técnicas: PrintNightmare (CVE-2021-1675), HiveNightmare (CVE-2021-36934), exploits de kernel (CVE-2020-0787, MS16-032), drivers vulnerables (BYOVD — Bring Your Own Vulnerable Driver). Frecuente en sistemas sin parches actualizados. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — proceso `spoolsv.exe` spawneando proceso hijo (PrintNightmare), proceso en ruta anómala con privilegios SYSTEM. Sysmon Event ID 6 (Driver loaded) — driver no firmado o con firma revocada cargado en kernel (BYOVD). Security log — Event ID 4688 con `MandatoryLabel` escalando de Medium a High o System. Event ID 7045 (nuevo servicio) con driver en ruta temporal. |
| **Lógica de detección** | Regla Sysmon: `spoolsv.exe` spawneando `cmd.exe` o `powershell.exe` → nivel 12 (PrintNightmare). Regla Event ID 6: driver cargado con firma no válida o de fabricante no habitual → nivel 10 (BYOVD). Regla correlación: proceso de usuario estándar ejecutando proceso hijo con `IntegrityLevel = System` en menos de 5s → nivel 12 (escalada instantánea típica de exploit). FIM: creación de DLL en `C:\Windows\System32\spool\drivers\` por proceso no esperado → nivel 12. |
| **MITRE ATT&CK** | T1068 — Exploitation for Privilege Escalation / T1543.003 — Create or Modify System Process / T1014 — Rootkit |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio-Alto — las reglas específicas por CVE son directas (PrintNightmare). La detección genérica de escalada por exploit requiere correlación de niveles de integridad entre procesos padre e hijo, que no es trivial en Wazuh. |
| **Falsos positivos** | Bajos para reglas específicas de CVE. Medios para detección genérica de drivers. |
| **Recomendación de hardening** | Mantener Windows Update al día es la medida más efectiva. Activar `DriverBlockList` en Windows Defender para bloquear drivers vulnerables conocidos. Deshabilitar Print Spooler en equipos que no necesiten impresión. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.PRIVESC.004 — Abuso de servicios o tareas programadas para escalada

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica un servicio existente o una tarea programada que se ejecuta con privilegios elevados (SYSTEM, administrador) para sustituir su binario o inyectar comandos maliciosos. La técnica aprovecha permisos incorrectos en los binarios de servicio, rutas con espacios sin comillas (unquoted service path) o permisos de escritura en directorios de servicios privilegiados. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — proceso de servicio (corriendo como SYSTEM) spawneando proceso hijo inesperado. Sysmon Event ID 11 (File created) — fichero ejecutable creado en directorio de servicio por proceso de usuario estándar. Security log — Event ID 4697 (servicio instalado) o 7040 (configuración de servicio cambiada) con cuenta de usuario no administrativo. Event ID 4698/4702 (tarea creada/modificada) con `TaskContent` cambiado por cuenta no autorizada. |
| **Lógica de detección** | Regla FIM: modificación de ejecutable en ruta de servicio privilegiado por proceso de usuario estándar → nivel 12. Regla Sysmon Event ID 11: creación de `.exe` o `.dll` en `C:\Program Files\`, `C:\Windows\System32\` por proceso sin privilegios administrativos → nivel 10. Regla correlación: Event ID 4697/7040 con cuenta no administrativa + proceso de ese servicio spawneando shell en 60s → nivel 12. |
| **MITRE ATT&CK** | T1574.009 — Hijack Execution Flow: Path Interception by Unquoted Path / T1574.010 — Services File Permissions Weakness / T1053.005 — Scheduled Task |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — la detección de modificación de binarios de servicio es directa con FIM. La detección de unquoted service path requiere enumeración previa de servicios vulnerables (tarea de hardening, no de detección reactiva). |
| **Falsos positivos** | Bajos. La modificación de binarios de servicios del sistema por procesos de usuario es prácticamente siempre anómala. |
| **Recomendación de hardening** | Auditar permisos de servicios con `sc sdshow` y herramientas como PowerSploit's `Get-ServiceUnquoted`. Corregir rutas con espacios añadiendo comillas. Restringir permisos de escritura en directorios de servicios privilegiados. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.PRIVESC.005 — Correlación transversal: escalada de privilegios confirmada

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de secuencia completa de escalada: proceso de usuario estándar intentando técnica de escalada seguido de ejecución exitosa con privilegios elevados. La correlación de la tentativa con el resultado eleva la confianza a incidente confirmado y permite identificar el vector exacto de escalada. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.02.WIN.PRIVESC.001-004 en el mismo endpoint + Event ID 4672 (Special privileges assigned) o proceso con `IntegrityLevel = System` en ventana de 300s. |
| **Lógica de detección** | Regla custom de segundo nivel: alerta de cualquier PRIVESC.00* en el mismo `hostname` + Event ID 4672 o proceso SYSTEM en 300s → nivel 12 (escalada confirmada). Regla adicional: cualquier PRIVESC.00* seguido de EP.02.WIN.EXEC.* desde el mismo endpoint en 600s → nivel 12 (escalada + movimiento lateral inmediato). |
| **MITRE ATT&CK** | T1548 — Abuse Elevation Control Mechanism / T1068 — Exploitation for Privilege Escalation / T1134 — Access Token Manipulation |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que las fichas PRIVESC.001-004 estén operativas. |
| **Falsos positivos** | Muy bajos. La combinación de intento de escalada + privilegios obtenidos en ventana corta es prácticamente siempre un incidente real. |
| **Nota operativa** | Cuando dispara esta regla, aislar el endpoint inmediatamente — el atacante ya tiene SYSTEM y puede desactivar controles de seguridad. Investigar también el vector de entrada inicial (cómo llegó al endpoint con privilegios de usuario). |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-02 (Actividad post-explotación)

---

###### EP.02.WIN.POST.001 — Discovery: enumeración de usuarios y grupos

| Campo | Detalle |
|---|---|
| **Descripción** | Tras comprometer un endpoint, el atacante enumera usuarios locales, grupos, cuentas de dominio y membresías de grupos privilegiados para entender el entorno y planificar el movimiento lateral. Técnicas comunes: `net user`, `net localgroup`, `net group /domain`, `whoami /all`, `Get-LocalUser`, `Get-ADUser`, `Get-ADGroupMember`. Es una de las primeras acciones de cualquier atacante tras obtener acceso. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `net.exe`, `net1.exe` con `CommandLine` conteniendo `user`, `localgroup`, `group /domain`. PowerShell ScriptBlock (Event ID 4104) con `Get-LocalUser`, `Get-ADUser`, `Get-ADGroupMember`, `Get-ADGroup`. Security log en DC — Event ID 4661 y 4662 sobre objetos de tipo `user` y `group` vía LDAP. |
| **Lógica de detección** | Regla Sysmon: `net.exe` o `net1.exe` con argumento `user`, `localgroup`, `group` desde proceso interactivo → nivel 8. Correlación: 3+ comandos de enumeración distintos desde mismo proceso en 60s → nivel 10 (enumeración sistemática). Regla PowerShell: Event ID 4104 con `Get-ADUser` o `Get-ADGroupMember` desde equipo de usuario → nivel 10. Regla DC: Event ID 4662 con `ObjectType = user` o `group` en volumen anómalo desde cuenta no administrativa → nivel 8. |
| **MITRE ATT&CK** | T1087 — Account Discovery / T1087.001 — Local Account / T1087.002 — Domain Account / T1069 — Permission Groups Discovery |
| **Severidad** | Media / Alta |
| **Esfuerzo** | Medio — `net.exe` tiene uso legítimo frecuente. La combinación de múltiples comandos en ventana corta y el contexto del proceso padre son los discriminadores clave. |
| **Falsos positivos** | Medios. Administradores usan estos comandos legítimamente. Whitelist de cuentas de IT y servidores de administración. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.POST.002 — Discovery: enumeración de hosts y shares de red

| Campo | Detalle |
|---|---|
| **Descripción** | El atacante enumera hosts activos en la red, recursos compartidos SMB, sesiones activas y configuración de red para mapear el entorno y encontrar objetivos de movimiento lateral. Técnicas comunes: `net view`, `net share`, `arp -a`, `ipconfig /all`, `nslookup`, `net session`, enumeración de shares con `net use`. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `net.exe`/`net1.exe` con `CommandLine` conteniendo `view`, `share`, `session`, `use`. `arp.exe` con argumento `-a`. `ipconfig.exe` con `/all`. Sysmon Event ID 3 — múltiples conexiones TCP/UDP a distintos hosts de la red interna desde el mismo proceso. |
| **Lógica de detección** | Regla Sysmon Event ID 1: `net view` o `net share` desde proceso interactivo → nivel 8. Correlación: `net view` + `arp -a` + `ipconfig /all` desde mismo proceso en 120s → nivel 10. Regla Event ID 3: mismo proceso iniciando conexiones a 10+ IPs distintas de red interna en 60s → nivel 10 (host sweep). |
| **MITRE ATT&CK** | T1135 — Network Share Discovery / T1016 — System Network Configuration Discovery / T1018 — Remote System Discovery |
| **Severidad** | Media / Alta |
| **Esfuerzo** | Medio — comandos de red tienen uso legítimo frecuente. La combinación de múltiples comandos de reconocimiento en ventana corta es el indicador de actividad maliciosa. |
| **Falsos positivos** | Medios. Scripts de monitorización y gestión usan estos comandos. Whitelist de procesos y cuentas de administración conocidos. |
| **Relación con otros CU** | Si tras esta ficha dispara NET.04 (escaneo interno desde red), la combinación indica movimiento lateral activo desde el endpoint comprometido. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.POST.003 — Discovery: enumeración de Active Directory (BloodHound / SharpHound)

| Campo | Detalle |
|---|---|
| **Descripción** | El atacante usa herramientas de enumeración de Active Directory para mapear relaciones de confianza, rutas de escalada de privilegios y cuentas con permisos excesivos. BloodHound/SharpHound recopila relaciones de grupos, ACLs, GPOs y sesiones activas en todo el dominio mediante consultas LDAP masivas. Otras herramientas: `ldapdomaindump`, `ADRecon`, `PowerView`. La enumeración AD masiva es uno de los indicadores más fiables de un ataque avanzado en curso. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `SharpHound.exe`, `bloodhound.exe`, `ldapdomaindump.py` o proceso con `CommandLine` conteniendo `-CollectionMethod All`, `--zip`. Security log en DC — Event ID 4662 con volumen anómalo de consultas LDAP en ventana corta desde misma cuenta/IP. PowerShell ScriptBlock Event ID 4104 con `Invoke-BloodHound`, `Get-DomainUser`, `Get-DomainGroupMember`, `Find-LocalAdminAccess`. |
| **Lógica de detección** | Regla Sysmon: `Image` conteniendo `sharphound`, `bloodhound`, `ldapdomaindump`, `adrecon` → nivel 12. Regla PowerShell: Event ID 4104 con `Invoke-BloodHound`, `Get-DomainTrust`, `Get-DomainGPO` → nivel 12. Regla DC: Event ID 4662 con 100+ consultas LDAP desde mismo `SubjectUserName` en 60s → nivel 10. Correlación: Event ID 4662 masivo + Sysmon herramienta conocida en mismo endpoint → nivel 12. |
| **MITRE ATT&CK** | T1482 — Domain Trust Discovery / T1069.002 — Domain Groups / T1087.002 — Domain Account / T1615 — Group Policy Discovery |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — detección por nombre de herramienta directa. Detección por volumen LDAP requiere baseline de actividad normal en el DC. |
| **Falsos positivos** | Muy bajos para nombres de herramientas conocidas. Medios para detección por volumen LDAP. |
| **Nota operativa** | SharpHound en modo `-CollectionMethod All` puede generar miles de consultas LDAP en minutos. Si se detecta, asumir que el atacante ya tiene un mapa completo del dominio — escalar a incidente crítico inmediatamente. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.POST.004 — Staging: descarga de herramientas desde Internet (LOLBins)

| Campo | Detalle |
|---|---|
| **Descripción** | El atacante descarga herramientas adicionales desde Internet usando utilidades nativas del sistema (Living off the Land / LOLBins): `certutil`, `bitsadmin`, `powershell Invoke-WebRequest`, `curl`, `mshta` con URL remota. Esta técnica evita traer herramientas en el vector de entrada inicial — el payload inicial es mínimo y descarga el arsenal después de establecer acceso. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `certutil.exe` con argumento `-urlcache` o `-decode`, `bitsadmin.exe` con `/transfer`, `mshta.exe` con URL como argumento. PowerShell ScriptBlock Event ID 4104 con `Invoke-WebRequest`, `IEX`, `DownloadString`, `DownloadFile`, `WebClient`. Sysmon Event ID 11 — ejecutable o script creado en `%TEMP%`, `%APPDATA%`, `%PUBLIC%` por proceso LOLBin. Sysmon Event ID 3 — conexión saliente desde `certutil.exe`, `bitsadmin.exe`, `powershell.exe` a IP/dominio externo. |
| **Lógica de detección** | Regla Sysmon Event ID 1: `certutil.exe` con `-urlcache -split -f` → nivel 12. `bitsadmin.exe` con `/transfer` hacia URL externa → nivel 12. `mshta.exe` con argumento comenzando por `http` → nivel 12. Regla PowerShell: `IEX` + `DownloadString` en mismo ScriptBlock → nivel 12. Correlación: LOLBin + Event ID 3 + Event ID 11 (fichero creado en ruta temporal) en 30s → nivel 12. |
| **MITRE ATT&CK** | T1105 — Ingress Tool Transfer / T1218 — System Binary Proxy Execution / T1059.001 — PowerShell |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo-Medio — LOLBins de descarga tienen firmas muy específicas. La combinación descarga + creación de fichero ejecutable es altamente fiable. |
| **Falsos positivos** | Bajos. `certutil` y `bitsadmin` raramente se usan para descargas en entornos corporativos gestionados. PowerShell con `IEX + DownloadString` es prácticamente siempre sospechoso. |
| **Nota operativa** | Si dispara esta ficha, buscar el proceso padre para identificar el vector de entrada inicial — esta técnica es la segunda fase de un ataque de dos etapas. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.POST.005 — Staging: compresión y preparación de datos para exfiltración

| Campo | Detalle |
|---|---|
| **Descripción** | El atacante recopila, comprime y cifra datos antes de exfiltrarlos. Técnicas comunes: `7z.exe`, `rar.exe`, `Compress-Archive`, creación de ficheros comprimidos en rutas temporales, uso de `robocopy` o `xcopy` para staging masivo de ficheros. La detección de esta fase permite interrumpir la exfiltración antes de que los datos salgan del endpoint. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 7.4 Pérdida de datos |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `7z.exe`, `rar.exe`, `winrar.exe` con argumentos de compresión en rutas temporales. PowerShell ScriptBlock Event ID 4104 con `Compress-Archive` apuntando a directorios de documentos. Sysmon Event ID 11 — creación de fichero `.zip`, `.7z`, `.rar` de tamaño grande en `%TEMP%`, `%APPDATA%`. Sysmon Event ID 1 — `robocopy.exe` o `xcopy.exe` copiando grandes volúmenes desde rutas de documentos a rutas temporales. |
| **Lógica de detección** | Regla Sysmon Event ID 1: compresor con argumento de salida en ruta temporal + origen en carpetas de documentos → nivel 10. Regla Event ID 11: creación de `.zip`/`.7z`/`.rar` > 50MB en `%TEMP%` o `%APPDATA%` → nivel 8. Correlación: compresión + Event ID 3 (conexión saliente) en 300s → nivel 12 (staging + exfiltración inmediata). Regla PowerShell: `Compress-Archive` con `-Path` apuntando a `C:\Users\*\Documents` o `C:\Users\*\Desktop` → nivel 10. |
| **MITRE ATT&CK** | T1560 — Archive Collected Data / T1560.001 — Archive via Utility / T1074 — Data Staged |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — compresores tienen uso legítimo frecuente. La combinación ruta de origen (documentos corporativos) + ruta de destino temporal + tamaño grande es el discriminador. |
| **Falsos positivos** | Medios. Usuarios comprimen ficheros legítimamente. Whitelist de operaciones de backup conocidas. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.POST.006 — Lateral preparation: escaneo interno desde endpoint comprometido

| Campo | Detalle |
|---|---|
| **Descripción** | El endpoint comprometido realiza escaneo activo de la red interna para descubrir nuevos objetivos de movimiento lateral: hosts activos, puertos abiertos, servicios expuestos. Técnicas: `ping` en bucle, `nmap`, PowerShell con `Test-NetConnection` masivo, herramientas de red integradas en frameworks C2. El escaneo interno desde un endpoint es uno de los indicadores más fiables de movimiento lateral en preparación. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 3 — múltiples conexiones TCP/ICMP desde el mismo proceso hacia distintos hosts de la red interna en ventana corta. Sysmon Event ID 1 — `nmap.exe`, `masscan.exe` o proceso con `CommandLine` conteniendo rangos de IP internos. PowerShell ScriptBlock Event ID 4104 con `Test-NetConnection` o `Test-Connection` en bucle. |
| **Lógica de detección** | Regla Sysmon: `nmap.exe`, `masscan.exe` ejecutados desde endpoint de usuario → nivel 12. Regla Event ID 3: mismo proceso iniciando conexiones a 20+ IPs distintas de red interna en 60s → nivel 10. Regla PowerShell: `Test-NetConnection` en bucle con más de 10 hosts distintos en 30s → nivel 10. Correlación: escaneo interno (esta ficha) + EP.02.WIN.EXEC.* desde el mismo endpoint en 600s → nivel 12. |
| **MITRE ATT&CK** | T1046 — Network Service Discovery / T1018 — Remote System Discovery / T1135 — Network Share Discovery |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — el volumen de conexiones internas es el indicador clave. Requiere baseline de tráfico lateral normal del endpoint. |
| **Falsos positivos** | Medios. Herramientas de monitorización realizan escaneos legítimos. Whitelist de IPs de servidores de monitorización (Nagios, Zabbix, SCCM). |
| **Relación con otros CU** | Complemento de NET.04 (reconocimiento y escaneo interno) en la capa de red. La combinación de ambas señales desde el mismo origen confirma movimiento lateral en preparación. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.POST.007 — Correlación: secuencia post-explotación confirmada

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la secuencia completa de actividad post-explotación en el mismo endpoint: discovery → staging → lateral preparation. La correlación de las tres fases en ventana temporal confirma un ataque avanzado en curso y permite al SOC intervenir antes de que el movimiento lateral o la exfiltración se completen. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.02.WIN.POST.001-006 en el mismo `hostname` en ventana temporal de 30 minutos. |
| **Lógica de detección** | Regla custom de segundo nivel: POST.001 o POST.002 (discovery) + POST.004 o POST.005 (staging) en el mismo hostname en 1800s → nivel 12. Regla de máxima prioridad: POST.003 (BloodHound) + POST.006 (escaneo interno) en mismo hostname en 600s → nivel 12. Correlación extendida: cualquier PRIVESC.00* + POST.00* en mismo hostname en 3600s → nivel 12. |
| **MITRE ATT&CK** | T1087 — Account Discovery / T1105 — Ingress Tool Transfer / T1046 — Network Service Discovery / T1482 — Domain Trust Discovery |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que las fichas POST.001-006 estén operativas. |
| **Falsos positivos** | Muy bajos. La secuencia discovery + staging + lateral prep en ventana corta es prácticamente siempre un ataque en curso. |
| **Nota operativa** | Cuando dispara esta regla el tiempo de respuesta es crítico — escalar a P1 inmediatamente, aislar el endpoint y activar el playbook de respuesta a incidentes. |
| **Prerequisito** | Fichas EP.02.WIN.POST.001-006 operativas. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-02 (Herramientas de pentesting y red team no autorizadas)

---

###### EP.02.WIN.REDTEAM.001 — Frameworks C2 en el endpoint (Cobalt Strike, Sliver, Havoc, Metasploit)

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la presencia o ejecución de frameworks de Command & Control en el endpoint: Cobalt Strike (beacon), Sliver, Havoc, Metasploit (meterpreter), Brute Ratel, Nighthawk. Estos frameworks son la herramienta principal de operadores de red team y atacantes avanzados para mantener acceso persistente y ejecutar acciones post-explotación. Su presencia en un endpoint de producción es un indicador de compromiso de máxima prioridad. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — nombre de imagen, descripción o `OriginalFileName` con cadenas asociadas a frameworks C2. Sysmon Event ID 7 (Image Loaded) — DLLs características (reflective loading de DLL sin ruta en disco). Sysmon Event ID 10 (ProcessAccess) — acceso a LSASS desde proceso sin firma en ruta temporal. Sysmon Event ID 3 — conexión saliente periódica desde proceso sospechoso. SentinelOne EP.01.WIN.AV.001 — alerta directa de detección de framework C2. |
| **Lógica de detección** | Regla Sysmon Event ID 1: `Image` o `CommandLine` conteniendo `beacon`, `meterpreter`, `sliver`, `havoc`, `bruteratel`, `nighthawk`, `cobaltstrike` (case-insensitive) → nivel 12. Regla Event ID 7: DLL cargada con `OriginalFileName` vacío o `FileVersion` ausente desde proceso en ruta temporal → nivel 10 (reflective DLL loading). Regla correlación: proceso en `%TEMP%` + Event ID 10 a LSASS + Event ID 3 a IP externa en 300s → nivel 12. JA3 hash de Cobalt Strike por defecto en tráfico saliente → nivel 12 (requiere SSL Decryption). |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1055 — Process Injection / T1003.001 — LSASS Memory / T1573 — Encrypted Channel |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — detección por nombre directa pero frameworks modernos usan nombres aleatorios. La detección por comportamiento es más robusta y requiere correlación de múltiples señales. |
| **Falsos positivos** | Muy bajos. Frameworks C2 no tienen uso legítimo en endpoints de producción. Si el cliente tiene ejercicios de red team, establecer ventanas de exclusión temporales. |
| **Nota operativa** | Coordinar con el cliente un proceso de notificación previa de ejercicios de red team autorizados. Cualquier actividad fuera de ventana notificada debe tratarse como compromiso real. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.REDTEAM.002 — Herramientas de explotación y post-explotación (Impacket, CrackMapExec, Responder)

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de herramientas de explotación de red y post-explotación ejecutadas en el endpoint: Impacket (psexec.py, secretsdump.py, wmiexec.py), CrackMapExec (CME), Responder (envenenamiento LLMNR/NBT-NS), Evil-WinRM, NetExec. Estas herramientas se usan para movimiento lateral, extracción de credenciales y explotación de protocolos de red. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `Image` o `CommandLine` con nombre de herramienta: `psexec.py`, `secretsdump.py`, `wmiexec.py`, `crackmapexec`, `cme`, `responder.py`, `evil-winrm`, `netexec`. Python ejecutando scripts de Impacket desde rutas temporales. Sysmon Event ID 11 — creación de scripts `.py` en rutas temporales. Security log — Event ID 4776 con volumen anómalo desde misma IP (Responder capturando hashes). |
| **Lógica de detección** | Regla Sysmon Event ID 1: `CommandLine` conteniendo `impacket`, `secretsdump`, `wmiexec`, `crackmapexec`, `responder`, `evil-winrm`, `netexec` → nivel 12. Regla: `python.exe` ejecutando script desde `%TEMP%` con argumento que contenga IP de red interna → nivel 10. Regla Security log: 10+ Event ID 4776 desde la misma IP en 60s → nivel 12. Regla Event ID 11: creación de `Responder.db` o `Responder.log` → nivel 12. |
| **MITRE ATT&CK** | T1557.001 — LLMNR/NBT-NS Poisoning / T1021.006 — Evil-WinRM / T1003 — Credential Dumping |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo-Medio — nombres de herramientas muy específicos. La detección de Responder por volumen de 4776 requiere correlación temporal. |
| **Falsos positivos** | Muy bajos. Estas herramientas no tienen uso legítimo en endpoints de producción. |
| **Nota operativa** | Responder puede capturar hashes NTLMv2 de cualquier usuario que intente resolver nombres en la red durante su ejecución. Si se detecta, revisar todos los eventos 4776 del periodo para identificar qué cuentas fueron comprometidas. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.REDTEAM.003 — Herramientas de reconocimiento y escaneo no autorizadas

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de herramientas de reconocimiento y escaneo de red no autorizadas en endpoints de producción: Nmap, Masscan, Nessus (instancia no autorizada), Shodan CLI, Angry IP Scanner, Advanced IP Scanner, Netcat en modo escaneo. Tienen uso legítimo en equipos de IT/seguridad pero son anómalas en endpoints de usuario o en contextos no autorizados. |
| **Clasificación GrayHats** | 3.1 Escaneo de redes (scanning) / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Sysmon Event ID 1 — `Image` conteniendo `nmap`, `masscan`, `nessus`, `angryip`, `advanced_ip_scanner`, `netcat`, `nc.exe`, `ncat`. `CommandLine` con argumentos de escaneo (`-sS`, `-sV`, `-p-`, `--top-ports`). Sysmon Event ID 3 — volumen anómalo de conexiones TCP/UDP a distintos hosts y puertos desde el mismo proceso. Sysmon Event ID 11 — creación de fichero `nmap-output.*` o `scan-results.*`. |
| **Lógica de detección** | Regla Sysmon Event ID 1: herramienta de escaneo desde equipo de usuario estándar → nivel 10. Misma herramienta desde equipo de IT → nivel 6 (informativo). Regla Event ID 3: proceso generando conexiones a 50+ puertos distintos en 30s → nivel 10. Contextualización por hostname: CDB list de equipos de IT/seguridad autorizados para reducir FP. |
| **MITRE ATT&CK** | T1046 — Network Service Discovery / T1595 — Active Reconnaissance |
| **Severidad** | Media / Alta (según contexto del endpoint) |
| **Esfuerzo** | Bajo — nombres de herramientas conocidos. La contextualización por tipo de equipo requiere CDB list de hostnames de equipos de IT. |
| **Falsos positivos** | Medios. Equipos de IT/seguridad usan estas herramientas legítimamente. En endpoints de usuario estándar es siempre sospechoso. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.REDTEAM.004 — Ejecución de payloads en memoria (process injection, shellcode)

| Campo | Detalle |
|---|---|
| **Descripción** | El atacante ejecuta código malicioso directamente en memoria sin escribir ficheros al disco usando técnicas de inyección de procesos: reflective DLL injection, process hollowing, shellcode injection, APC injection, thread hijacking. Estas técnicas evitan la detección basada en ficheros y son características de frameworks C2 avanzados y malware sofisticado. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 8 (CreateRemoteThread) — creación de hilo remoto en proceso legítimo desde proceso sospechoso. Sysmon Event ID 10 (ProcessAccess) — acceso a proceso legítimo con permisos de escritura de memoria (`PROCESS_VM_WRITE 0x0020`). Sysmon Event ID 25 (Process Tampering) — detección de process hollowing o herpaderping. Sysmon Event ID 7 (Image Loaded) — DLL cargada sin ruta en disco. SentinelOne — alerta de comportamiento de inyección de proceso. |
| **Lógica de detección** | Regla Sysmon Event ID 8: `CreateRemoteThread` desde proceso no firmado o en ruta temporal hacia proceso del sistema (explorer, svchost, notepad) → nivel 12. Regla Event ID 10: `GrantedAccess` = `0x1438` o `0x1F3FFF` desde proceso no de sistema hacia proceso de sistema → nivel 12. Regla Event ID 25: cualquier Process Tampering → nivel 12. Regla Event ID 7: DLL con `Signed = false` y `FileVersion` vacío desde proceso en ruta temporal → nivel 10. |
| **MITRE ATT&CK** | T1055 — Process Injection / T1055.001 — DLL Injection / T1055.012 — Process Hollowing / T1055.004 — APC Injection |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — Event ID 8 y Event ID 10 generan volumen alto de eventos legítimos. Whitelist de procesos legítimos (EDR, AV, depuradores) imprescindible. SentinelOne aporta cobertura complementaria de alto valor. |
| **Falsos positivos** | Medios para reglas individuales. Muy bajos para Event ID 25 — prácticamente siempre malicioso. |
| **Nota operativa** | Si SentinelOne no detecta process injection y Sysmon sí, indica que el atacante está usando técnicas de evasión de EDR activamente — escalar la prioridad del incidente. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.REDTEAM.005 — Correlación: perfil de red team activo en el endpoint

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la combinación de herramientas y técnicas que configuran un perfil de operación de red team o ataque avanzado en el endpoint: framework C2 + herramienta de explotación + herramienta de reconocimiento + inyección en memoria. La correlación de múltiples señales del bloque REDTEAM confirma una operación activa de máxima prioridad. |
| **Clasificación GrayHats** | 2.2 Servidor C&C (Mando y Control) / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.02.WIN.REDTEAM.001-004 en el mismo `hostname` en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: 2+ alertas de distintas fichas REDTEAM.00* en el mismo hostname en 600s → nivel 12. Regla de máxima prioridad: REDTEAM.001 (framework C2) + REDTEAM.004 (process injection) en mismo hostname en 300s → nivel 12. Correlación extendida: cualquier REDTEAM.00* + POST.00* + PRIVESC.00* en mismo hostname en 3600s → nivel 12 (cadena completa de ataque avanzado). |
| **MITRE ATT&CK** | T1071 — Application Layer Protocol / T1055 — Process Injection / T1046 — Network Service Discovery / T1003 — Credential Dumping |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que las fichas REDTEAM.001-004 estén operativas. |
| **Falsos positivos** | Prácticamente nulos. La combinación de múltiples herramientas de red team en ventana corta es siempre un incidente — real o ejercicio no notificado. |
| **Nota operativa** | Primera acción: verificar si hay ejercicio de red team autorizado en curso. Si no hay notificación previa documentada, tratar como compromiso real. Aislar el endpoint y preservar evidencias forenses (volcado de memoria) antes de cualquier remediación. |
| **Prerequisito** | Fichas EP.02.WIN.REDTEAM.001-004 operativas. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-02 (Explotación de vulnerabilidades locales)

---

###### EP.02.WIN.EXPLOIT.001 — Explotación de aplicaciones de usuario (Office, browsers, PDF readers)

| Campo | Detalle |
|---|---|
| **Descripción** | Una aplicación de usuario legítima (Microsoft Office, navegadores web, Adobe Reader, Foxit, WinRAR) es explotada para ejecutar código arbitrario — generalmente mediante un documento o fichero malicioso abierto por el usuario. El indicador principal es la aplicación spawneando procesos hijos anómalos: Office abriendo `cmd.exe`, un browser ejecutando `powershell.exe`, un visor de PDF lanzando `wscript.exe`. Técnica de entrada inicial muy frecuente en campañas de phishing con adjuntos maliciosos. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — proceso hijo sospechoso con `ParentImage` = aplicación de usuario: `WINWORD.EXE`, `EXCEL.EXE`, `POWERPNT.EXE`, `OUTLOOK.EXE`, `AcroRd32.exe`, `Foxit Reader.exe`, `chrome.exe`, `msedge.exe`, `firefox.exe`, `WinRAR.exe`. Proceso hijo anómalo: `cmd.exe`, `powershell.exe`, `wscript.exe`, `cscript.exe`, `mshta.exe`, `rundll32.exe`, cualquier ejecutable en `%TEMP%`. Sysmon Event ID 11 — creación de ejecutable o script en `%TEMP%` por aplicación de usuario. |
| **Lógica de detección** | Regla Sysmon alta confianza: `ParentImage` = aplicación Office o visor de documentos + `Image` = intérprete de comandos o proceso en ruta temporal → nivel 12. Regla browser: `ParentImage` = navegador + proceso hijo fuera de rutas de sistema del navegador → nivel 10. Regla Event ID 11: creación de `.exe`, `.dll`, `.ps1`, `.vbs` en `%TEMP%` por aplicación de usuario → nivel 8. Correlación: proceso hijo de Office + Event ID 3 (conexión saliente) en 60s → nivel 12. |
| **MITRE ATT&CK** | T1566.001 — Phishing: Spearphishing Attachment / T1203 — Exploitation for Client Execution / T1059 — Command and Scripting Interpreter |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — las reglas de proceso padre sospechoso son de alta confianza y bajo volumen de FP. Son de las detecciones más rentables del catálogo. |
| **Falsos positivos** | Muy bajos. Office spawneando `cmd.exe` no tiene justificación legítima en entornos corporativos modernos. Posible FP con macros de automatización legítimas — whitelist de documentos específicos si es imprescindible. |
| **Recomendación de hardening** | Activar Attack Surface Reduction (ASR) rules en Microsoft Defender: bloquear Office de crear procesos hijo. Deshabilitar macros por defecto vía GPO. Activar Protected View para documentos de Internet. |
| **Relación con otros CU** | Si tras esta ficha dispara EP.02.WIN.POST.004 (descarga LOLBins), la cadena es: documento malicioso → explotación → descarga de payload → compromiso. Escalar a P1 inmediatamente. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXPLOIT.002 — Explotación de servicios y aplicaciones locales

| Campo | Detalle |
|---|---|
| **Descripción** | Un servicio o aplicación local con escucha de red (IIS local, SQL Server Express, aplicación web interna, servicio RPC) es explotada por un atacante con acceso a la red local o desde el propio sistema. A diferencia de NET.01 (explotación perimetral), este caso se produce desde dentro de la red — típicamente en fase de movimiento lateral, cuando el atacante busca escalar privilegios o pivotar a otro sistema. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — proceso de servicio (`w3wp.exe`, `sqlservr.exe`) spawneando proceso hijo anómalo (`cmd.exe`, `powershell.exe`, `whoami.exe`). Sysmon Event ID 11 — creación de web shell (`.aspx`, `.php`, `.jsp`) en directorio web por proceso de servicio. Wazuh FIM — creación o modificación de ficheros en directorio raíz web (`C:\inetpub\wwwroot\`). |
| **Lógica de detección** | Regla Sysmon alta confianza: `ParentImage` = `w3wp.exe` + proceso hijo = intérprete de comandos → nivel 12 (web shell activo en IIS). `ParentImage` = `sqlservr.exe` + `Image` = `cmd.exe` o `powershell.exe` → nivel 12 (SQL injection con xp_cmdshell). FIM: creación de `.aspx` o `.php` en directorio web por proceso no de despliegue → nivel 12. Correlación: FIM web shell + Event ID 3 (conexión entrante al servicio web) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1190 — Exploit Public-Facing Application / T1505.003 — Web Shell / T1059 — Command and Scripting Interpreter |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — las reglas de proceso padre de servicio son de alta confianza. La detección de web shells por FIM requiere configurar los directorios web correctamente en `agent.conf`. |
| **Falsos positivos** | Muy bajos para `w3wp.exe` spawneando `cmd.exe`. Medios para FIM en directorios web (despliegues legítimos crean ficheros). Whitelist de procesos y cuentas de despliegue autorizados. |
| **Nota operativa** | Si se detecta un web shell, preservar el fichero como evidencia antes de eliminarlo. Su contenido puede revelar el vector de entrada y las acciones realizadas por el atacante. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXPLOIT.003 — Uso de exploits públicos conocidos (PoC de CVE recientes)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa un exploit público (PoC de GitHub, Exploit-DB, Metasploit module) para explotar una vulnerabilidad conocida en el sistema o en una aplicación instalada. Los indicadores incluyen nombres de ficheros de exploit conocidos, argumentos de línea de comandos característicos de PoCs publicados y comportamiento de proceso compatible con exploits conocidos. Complementa PRIVESC.003 con un enfoque más amplio de explotación de CVEs en cualquier contexto. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `Image` o `CommandLine` con nombres de exploits conocidos: `PrintSpoofer`, `EfsPotato`, `SweetPotato`, `GodPotato`, `JuicyPotatoNG`, `MS17-010`, `EternalBlue`, `BlueKeep`. Sysmon Event ID 6 (Driver loaded) — driver con firma inválida (BYOVD). Sysmon Event ID 7 — DLL de exploit cargada. SentinelOne — alerta de detección de exploit conocido. |
| **Lógica de detección** | Regla Sysmon Event ID 1: `Image` o `OriginalFileName` conteniendo nombre de exploit conocido → nivel 12. Regla Event ID 6: driver sin firma válida desde ruta temporal o de usuario → nivel 10. Regla: proceso con nombre que coincida con patrón `CVE-[0-9]{4}-[0-9]+` → nivel 10. Correlación: Event ID 6 (driver cargado) + Event ID 4672 (privilegios especiales) en 60s → nivel 12 (BYOVD con escalada confirmada). |
| **MITRE ATT&CK** | T1068 — Exploitation for Privilege Escalation / T1203 — Exploitation for Client Execution / T1014 — Rootkit |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — la detección por nombre de exploit requiere mantenimiento de la lista de exploits conocidos. La detección genérica por patrón CVE en nombre de fichero es más amplia pero con más FP. |
| **Falsos positivos** | Bajos para nombres de exploit específicos. Medios para detección de drivers sin firma. |
| **Nota operativa** | Mantener actualizada la lista de exploits conocidos es una tarea operativa continua. Suscribirse a alertas de CVE críticos (CISA KEV, NVD) para actualizar las reglas ante nuevos PoCs publicados. |
| **Estado** | Pendiente de validación. |

---

###### EP.02.WIN.EXPLOIT.004 — Correlación: explotación confirmada y payload ejecutado

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la secuencia completa de explotación: vulnerabilidad explotada seguida de ejecución de payload (proceso hijo anómalo, conexión C2, descarga de herramientas, escalada de privilegios). La correlación del evento de explotación con la acción posterior confirma el éxito del exploit y permite al SOC responder con prioridad máxima antes de que el atacante avance en la cadena de ataque. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.02.WIN.EXPLOIT.001-003 con alertas de fichas de ejecución o C2 en el mismo `hostname` en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: EXPLOIT.001 o EXPLOIT.002 + EP.02.WIN.POST.004 (descarga LOLBins) en mismo hostname en 300s → nivel 12. Regla de máxima prioridad: cualquier EXPLOIT.00* + NET.02.PALO.C2.* o NET.03.PALO.BEACON.* en mismo hostname en 600s → nivel 12. Correlación extendida: EXPLOIT.00* + PRIVESC.00* en mismo hostname en 600s → nivel 12. |
| **MITRE ATT&CK** | T1203 — Exploitation for Client Execution / T1068 — Exploitation for Privilege Escalation / T1105 — Ingress Tool Transfer |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que las fichas EXPLOIT.001-003 y las fichas de ejecución/C2 estén operativas. |
| **Falsos positivos** | Muy bajos. La combinación explotación + payload ejecutado en ventana corta es prácticamente siempre un incidente real. |
| **Nota operativa** | Cuando dispara, el endpoint está comprometido — iniciar respuesta a incidentes inmediatamente: aislamiento, preservación de evidencias (volcado de memoria, copia de logs), notificación al cliente. |
| **Prerequisito** | Fichas EP.02.WIN.EXPLOIT.001-003 operativas y normalizadas con fichas de ejecución/C2. |
| **Estado** | Pendiente de validación. |

---

### 1.3 Linux

> Pendiente de desarrollo. Se añadirán las fichas específicas cuando se desplieguen los agentes Wazuh en endpoints Linux y se definan los casos de uso correspondientes.

---

### 1.4 macOS

> Pendiente de desarrollo.

---

