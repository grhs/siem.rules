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
    - **Scripts de arranque**
    - EP.03.WIN.BOOT.001 — Modificación de scripts de inicio del sistema (BootExecute, SetupExecute)
    - EP.03.WIN.BOOT.002 — Modificación de la carpeta Startup (usuario y sistema)
    - EP.03.WIN.BOOT.003 — WMI Event Subscription para persistencia en arranque
    - **Web shells en servidores**
    - EP.03.WIN.SHELL.001 — Web shell en IIS
    - EP.03.WIN.SHELL.002 — Web shell en Apache / Nginx (Windows)
    - EP.03.WIN.SHELL.003 — Web shell genérica: detección por comportamiento
    - **Cuentas locales persistentes**
    - EP.03.WIN.IDM.001 — Creación de cuenta de usuario local (detección básica)
    - EP.03.WIN.IDM.002 — Usuario añadido a grupo Administradores local (detección básica)
    - EP.03.WIN.ACCT.001 — Cuenta local oculta o con nombre camuflado
    - EP.03.WIN.ACCT.002 — Reactivación de cuenta deshabilitada o manipulación de atributos
    - EP.03.WIN.ACCT.003 — Cuenta de servicio o técnica usada como backdoor
    - **Modificación de GPO locales**
    - EP.03.WIN.GPO.001 — Modificación de GPO local para deshabilitar controles de seguridad
    - EP.03.WIN.GPO.002 — Modificación de GPO local para establecer persistencia
    - EP.03.WIN.GPO.003 — Manipulación directa de ficheros de GPO local (GptTmpl.inf, Registry.pol)
  - [EP-04 — Robo o abuso de credenciales](#ep-04--robo-o-abuso-de-credenciales)
    - EP.04.WIN.AUTH.002 — Brute force de login local
    - EP.04.WIN.IDM.003 — Modificación de cuenta de usuario
    - EP.04.WIN.IDM.004 — Cambio de contraseña por otro usuario
    - EP.04.WIN.SAM.001 — Acceso a SAM/SYSTEM/SECURITY para extracción de hashes
    - EP.04.WIN.TOKEN.001 — Extracción y abuso de tokens de acceso
    - EP.04.WIN.BROWSER.001 — Robo de cookies y credenciales de navegador
    - EP.04.WIN.VAULT.001 — Acceso a Credential Manager y vaults locales
    - EP.04.WIN.PLAIN.001 — Credenciales en texto plano en ficheros, scripts y registro
  - [EP-05 — Movimiento lateral](#ep-05--movimiento-lateral)
    - EP.05.WIN.LAT.001 — Conexiones RDP laterales entre endpoints
    - EP.05.WIN.LAT.002 — Acceso a shares administrativos (C$, ADMIN$, IPC$)
    - EP.05.WIN.LAT.003 — Autenticaciones NTLM laterales inusuales
    - EP.05.WIN.LAT.004 — Herramientas administrativas usadas fuera de patrón
    - EP.05.WIN.LAT.005 — Correlación: perfil de movimiento lateral activo
  - [EP-06 — Exfiltración o preparación de exfiltración](#ep-06--exfiltración-o-preparación-de-exfiltración)
    - EP.06.WIN.EXFIL.001 — Herramientas de transferencia de ficheros (rclone, WinSCP, curl, scp, ftp)
    - EP.06.WIN.EXFIL.002 — Subida a servicios cloud no autorizados
    - EP.06.WIN.EXFIL.003 — Copia masiva a dispositivos USB
    - EP.06.WIN.EXFIL.004 — Acceso masivo a carpetas sensibles o fuera de horario
    - EP.06.WIN.EXFIL.005 — Correlación: preparación y exfiltración confirmada
  - [EP-07 — Uso anómalo de herramientas legítimas (LOLBins)](#ep-07--uso-anómalo-de-herramientas-legítimas-lolbins)
    - EP.07.WIN.LOLBIN.001 — PowerShell ofensivo: obfuscación, AMSI bypass, reflective loading
    - EP.07.WIN.LOLBIN.002 — Proxy de ejecución: Regsvr32, Rundll32, Mshta, Cscript/Wscript
    - EP.07.WIN.LOLBIN.003 — Netsh como proxy de red o persistencia
    - EP.07.WIN.LOLBIN.004 — Cmd.exe encadenado con scripts complejos
    - EP.07.WIN.LOLBIN.005 — Certutil y Bitsadmin para decode/encode y evasión
    - EP.07.WIN.LOLBIN.006 — Correlación: patrón LOLBin multi-herramienta
  - [EP-08 — Comportamiento anómalo del usuario o del equipo](#ep-08--comportamiento-anómalo-del-usuario-o-del-equipo)
    - EP.08.WIN.AUTH.004 — Login interactivo con cuenta privilegiada
    - EP.08.WIN.UBA.001 — Actividad fuera del horario habitual del usuario
    - EP.08.WIN.UBA.002 — Inicio de sesión desde equipo o ubicación no habitual
    - EP.08.WIN.UBA.003 — Ejecución de procesos inusuales para ese usuario o equipo
    - EP.08.WIN.UBA.004 — Uso intensivo de CPU/disco por proceso desconocido (criptominería, ransomware)
    - EP.08.WIN.UBA.005 — Actividad administrativa desde usuario no técnico
  - [EP-09 — Violación de políticas de seguridad](#ep-09--violación-de-políticas-de-seguridad)
    - EP.09.WIN.FIM.001 — Modificación de ficheros críticos del sistema
    - EP.09.WIN.POL.001 — EDR SentinelOne parado, manipulado o desinstalado
    - EP.09.WIN.POL.002 — Firewall local de Windows desactivado
    - EP.09.WIN.POL.003 — Shadow Copies eliminadas o servicio VSS manipulado ⚠️ máxima prioridad
    - EP.09.WIN.POL.004 — Software prohibido instalado o ejecutado
    - EP.09.WIN.POL.005 — Macros de Office habilitadas desde documento externo
    - EP.09.WIN.POL.006 — Software obsoleto o sin parches ejecutándose
  - [EP-10 — Manipulación defensiva y evasión](#ep-10--manipulación-defensiva-y-evasión)
    - EP.10.WIN.AUDIT.001 — Limpieza del log de auditoría de seguridad
    - EP.10.WIN.AUDIT.002 — Modificación de la política de auditoría
    - EP.10.WIN.AV.001 — Microsoft Defender deshabilitado o manipulado
    - EP.10.WIN.DEF.001 — Parada de servicios de seguridad
    - EP.10.WIN.DEF.002 — Cambios en exclusiones de AV/Defender
    - EP.10.WIN.DEF.003 — Borrado de logs de Windows (todos los canales)
    - EP.10.WIN.DEF.004 — Herramientas anti-forense (SDelete, timestomping, Eraser)
    - EP.10.WIN.DEF.005 — Correlación: perfil completo de evasión defensiva
- [1.3 Linux](#13-linux) *(pendiente)*
- [1.4 macOS](#14-macos) *(pendiente)*

---

## 1. Endpoints

Detecciones orientadas a identificar actividad maliciosa, sospechosa o anómala ejecutándose directamente en los endpoints monitorizados. La cobertura se organiza por sistema operativo y fase de despliegue.

---

### 1.1 Windows

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

##### Fichas detalladas — EP-03 (Scripts de arranque)

---

###### EP.03.WIN.BOOT.001 — Modificación de scripts de inicio del sistema (BootExecute, SetupExecute)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica las claves de registro que controlan la ejecución de programas durante las primeras fases del arranque del sistema operativo, antes de que los controles de seguridad estén completamente activos: `BootExecute` (programas ejecutados por Session Manager durante el boot, antes del login), `SetupExecute`, `PendingFileRenameOperations` (permite sustituir ficheros en el siguiente reinicio). El código se ejecuta antes que el EDR y el agente Wazuh. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — `TargetObject` conteniendo `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\BootExecute`, `\SetupExecute`, `\PendingFileRenameOperations`, `\Execute`. Campos clave: `Image` (proceso que modifica), `Details` (nuevo valor). FIM — modificación de las claves anteriores con cambio de valor respecto a la línea base. |
| **Lógica de detección** | Regla Sysmon alta confianza: Event ID 13 con `TargetObject` conteniendo `\Session Manager\BootExecute` con `Details` distinto al valor estándar (`autocheck autochk *`) → nivel 12. Regla: modificación de `\PendingFileRenameOperations` con valor que contenga ruta a ejecutable → nivel 10. Regla: cualquier escritura en `\Session Manager\Execute` o `\SetupExecute` desde proceso no de Windows Update → nivel 12. |
| **MITRE ATT&CK** | T1542.003 — Pre-OS Boot: Bootkit / T1547.001 — Boot or Logon Autostart Execution |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — claves muy específicas con valor estándar conocido. El valor legítimo de `BootExecute` es prácticamente siempre `autocheck autochk *`. |
| **Falsos positivos** | Muy bajos. `BootExecute` raramente se modifica en producción. `PendingFileRenameOperations` tiene uso legítimo en instalaciones de software — whitelist de procesos instaladores conocidos. |
| **Nota operativa** | El código en `BootExecute` se ejecuta antes que el antivirus y el EDR. Si se detecta esta modificación, considerar análisis offline del disco antes de reiniciar el endpoint. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.BOOT.002 — Modificación de la carpeta Startup (usuario y sistema)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante coloca un ejecutable, script o acceso directo en las carpetas de inicio automático de Windows: carpeta de sistema (`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup`) o del usuario actual (`C:\Users\<usuario>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`). Cualquier fichero en estas carpetas se ejecuta automáticamente al iniciar sesión. Técnica simple y muy frecuente en malware de baja sofisticación. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 11 — creación de fichero en `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\` o `C:\Users\*\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\`. Campos clave: `Image` (proceso que crea), `TargetFilename`. FIM — Wazuh syscheck monitorizando esas rutas con `realtime="yes"`. |
| **Lógica de detección** | Regla Sysmon: Event ID 11 con `TargetFilename` conteniendo `\Programs\Startup\` y extensión `.exe`, `.bat`, `.vbs`, `.ps1`, `.js`, `.lnk` desde proceso no instalador → nivel 10. Crítica: fichero `.exe` o script creado en Startup por proceso interactivo (cmd, powershell, navegador) → nivel 12. Regla FIM: cualquier fichero nuevo en carpeta Startup → nivel 8. Correlación: creación en Startup + Event ID 3 (conexión saliente del nuevo fichero) en el siguiente logon → nivel 12. |
| **MITRE ATT&CK** | T1547.001 — Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — rutas muy específicas. FIM sobre la carpeta Startup es suficiente. Wazuh syscheck monitoriza esta ruta por defecto. |
| **Falsos positivos** | Medios. Instaladores legítimos añaden accesos directos en Startup (Teams, Slack, OneDrive). Whitelist de ficheros `.lnk` conocidos y sus procesos creadores. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.BOOT.003 — WMI Event Subscription para persistencia en arranque

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante registra una suscripción de evento WMI permanente para ejecutar código malicioso ante eventos del sistema como el arranque, login de usuario o un intervalo de tiempo. Las suscripciones WMI permanentes sobreviven reinicios y son independientes del registro y de las carpetas Startup — lo que las hace especialmente difíciles de detectar. Técnica favorita de APTs avanzados. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 19 (WmiEvent - Filter activity) — creación de filtro de evento WMI. Event ID 20 (WmiEvent - Consumer activity) — creación de consumidor WMI (`CommandLineEventConsumer`, `ActiveScriptEventConsumer`). Event ID 21 (WmiEvent - FilterToConsumerBinding) — enlace entre filtro y consumidor. Campos clave: `Name`, `Query` (consulta WMI del filtro), `Destination` (comando a ejecutar). |
| **Lógica de detección** | Regla Sysmon: Event ID 19 con `Query` conteniendo `Win32_PerfFormattedData` (trigger de arranque) o `__InstanceCreationEvent` → nivel 10. Alta confianza: Event ID 20 con `ConsumerType = CommandLineEventConsumer` o `ActiveScriptEventConsumer` con `Destination` conteniendo `powershell`, `cmd`, `wscript`, `mshta` o URL → nivel 12. Crítica: Event ID 21 (binding confirmado) + Event ID 20 con destino sospechoso → nivel 12. Correlación: los tres eventos (19+20+21) desde el mismo proceso en 60s → nivel 12. |
| **MITRE ATT&CK** | T1546.003 — Event Triggered Execution: Windows Management Instrumentation Event Subscription |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — Sysmon Event IDs 19, 20 y 21 son específicos de WMI y de bajo volumen en producción. Filtrado por tipo de consumidor reduce drásticamente los FP. |
| **Falsos positivos** | Bajos. Suscripciones WMI permanentes con consumidores de línea de comandos no tienen uso legítimo frecuente. Whitelist de nombres de filtros/consumidores conocidos de software de gestión (SCCM, Ansible). |
| **Nota operativa** | Las suscripciones WMI se almacenan en el repositorio WMI (`C:\Windows\System32\wbem\Repository`), no en el registro ni en ficheros del sistema — invisibles para herramientas que solo analizan Run keys o carpetas Startup. Para limpiarlas usar `Get-WMIObject -Namespace root\subscription -Class __EventFilter` o Autoruns de Sysinternals. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Web shells en servidores)

---

###### EP.03.WIN.SHELL.001 — Web shell en IIS

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante ha subido o creado un web shell en un servidor IIS — un script (`.aspx`, `.ashx`, `.asmx`, `.asp`, `.cshtml`) que permite ejecutar comandos arbitrarios en el servidor a través de peticiones HTTP. La detección combina FIM sobre el directorio web, el proceso `w3wp.exe` spawneando procesos hijo anómalos, y conexiones salientes desde el proceso web. Web shells son el mecanismo de persistencia más frecuente tras la explotación de aplicaciones web. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | FIM — creación o modificación de fichero `.aspx`, `.ashx`, `.asmx`, `.asp`, `.cshtml`, `.config` en `C:\inetpub\wwwroot\` o cualquier directorio virtual de IIS. Sysmon Event ID 1 — `w3wp.exe` spawneando `cmd.exe`, `powershell.exe`, `cscript.exe`, `wscript.exe`, `certutil.exe` o ejecutable en ruta temporal. Sysmon Event ID 11 — creación de fichero ejecutable o script en directorio web por `w3wp.exe`. Sysmon Event ID 3 — conexión saliente desde `w3wp.exe` hacia IP externa. |
| **Lógica de detección** | Regla FIM: creación de `.aspx` o `.asp` en `C:\inetpub\wwwroot\` por proceso distinto a pipeline de despliegue autorizado → nivel 10. Regla Sysmon crítica: `w3wp.exe` spawneando `cmd.exe` o `powershell.exe` → nivel 12. Regla Event ID 3: `w3wp.exe` iniciando conexión saliente a IP externa → nivel 10. Correlación: FIM (nuevo `.aspx`) + Event ID 1 (`w3wp.exe` spawneando shell) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1505.003 — Server Software Component: Web Shell / T1190 — Exploit Public-Facing Application |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo-Medio — regla de `w3wp.exe` spawneando intérpretes es de alta confianza y bajo FP. FIM sobre wwwroot requiere configurar la ruta correcta y gestionar el ruido de despliegues legítimos. |
| **Falsos positivos** | Muy bajos para `w3wp.exe` spawneando `cmd.exe`. Medios para FIM (despliegues legítimos crean ficheros `.aspx`). Whitelist de cuentas y procesos de despliegue autorizados (Jenkins, Azure DevOps, Octopus Deploy). |
| **Nota operativa** | Preservar el fichero del web shell como evidencia antes de eliminarlo — su contenido revela el vector de entrada y puede contener credenciales hardcodeadas. Revisar los logs de acceso de IIS para identificar las peticiones al web shell y el origen del atacante. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.SHELL.002 — Web shell en Apache / Nginx (Windows)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante ha subido o creado un web shell en un servidor Apache o Nginx corriendo sobre Windows — típicamente scripts `.php`, `.py`, `.pl`, `.cgi`. La detección sigue el mismo patrón que IIS pero adaptada a los procesos `httpd.exe`, `nginx.exe`, `php-cgi.exe` y a los directorios de document root habituales de Apache/Nginx en Windows. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | FIM — creación o modificación de fichero `.php`, `.py`, `.pl`, `.cgi`, `.phtml` en el document root (`C:\Apache\htdocs\`, `C:\xampp\htdocs\`, `C:\nginx\html\` o ruta configurada en httpd.conf). Sysmon Event ID 1 — `httpd.exe`, `nginx.exe`, `php-cgi.exe`, `php.exe` spawneando `cmd.exe`, `powershell.exe` o ejecutable en ruta temporal. Sysmon Event ID 3 — conexión saliente desde `httpd.exe` o `php-cgi.exe` hacia IP externa. |
| **Lógica de detección** | Regla FIM: creación de `.php` en document root por proceso distinto a pipeline de despliegue → nivel 10. Regla Sysmon crítica: `httpd.exe` o `php-cgi.exe` spawneando `cmd.exe` o `powershell.exe` → nivel 12. Regla Event ID 3: proceso web iniciando conexión saliente → nivel 10. Correlación: FIM (nuevo `.php`) + proceso web spawneando shell en 300s → nivel 12. |
| **MITRE ATT&CK** | T1505.003 — Server Software Component: Web Shell / T1190 — Exploit Public-Facing Application |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — requiere conocer la ruta exacta del document root de cada cliente para configurar FIM. Whitelist de procesos de despliegue autorizado por cliente. |
| **Falsos positivos** | Muy bajos para proceso web spawneando `cmd.exe`. Medios para FIM en document root (despliegues frecuentes en entornos de desarrollo). |
| **Nota operativa** | En entornos con PHP, añadir `.htaccess` a la configuración de FIM — los atacantes lo modifican para redirigir peticiones al web shell o habilitar ejecución de PHP en directorios no esperados. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.SHELL.003 — Web shell genérica: detección por comportamiento

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de comportamiento característico de web shell activa, independientemente del servidor web o tecnología: el proceso del servidor web ejecuta comandos del sistema, realiza conexiones salientes anómalas o accede a recursos del sistema que no corresponden a la operación normal. Esta ficha complementa SHELL.001 y SHELL.002 con detección agnóstica a la tecnología — especialmente útil cuando el servidor web no está identificado de antemano o cuando el atacante usa técnicas de ofuscación para evadir FIM. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — cualquier proceso de servidor web conocido (`w3wp.exe`, `httpd.exe`, `nginx.exe`, `tomcat.exe`, `java.exe` en contexto web, `node.exe`) spawneando proceso hijo fuera de su operación normal. Sysmon Event ID 3 — conexión saliente desde proceso de servidor web hacia IP externa no de actualización o telemetría. Sysmon Event ID 10 — proceso de servidor web accediendo a `lsass.exe`. Sysmon Event ID 11 — proceso de servidor web creando fichero ejecutable fuera del document root. |
| **Lógica de detección** | Regla Sysmon crítica: cualquier proceso de servidor web spawneando `cmd.exe`, `powershell.exe`, `wscript.exe`, `cscript.exe`, `mshta.exe`, `certutil.exe`, `bitsadmin.exe` → nivel 12. Regla Event ID 3: proceso de servidor web iniciando conexión saliente a IP no en whitelist → nivel 8. Regla Event ID 10: proceso de servidor web con acceso a `lsass.exe` → nivel 12. Regla Event ID 11: proceso de servidor web creando `.exe` o `.dll` → nivel 12. |
| **MITRE ATT&CK** | T1505.003 — Server Software Component: Web Shell / T1059 — Command and Scripting Interpreter / T1003.001 — LSASS Memory |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — la lista de procesos de servidor web es finita y bien conocida. Las reglas de proceso web spawneando intérpretes son de la más alta confianza en todo el catálogo. |
| **Falsos positivos** | Muy bajos. Procesos de servidor web spawneando `cmd.exe` no tienen justificación legítima en producción. Entornos de desarrollo con scripts de build integrados pueden generar FP — separar entornos de desarrollo de producción. |
| **Nota operativa** | Esta ficha actúa como red de seguridad para web shells que evaden FIM (ficheros ofuscados, extensiones no comunes, web shells en memoria). Si solo dispara esta ficha sin FIM, el web shell puede estar en memoria o en extensión no monitorizada — investigar el historial de peticiones HTTP al servidor en el periodo previo. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Cuentas locales persistentes)

---

###### EP.03.WIN.IDM.001 — Creación de cuenta de usuario local

| Campo | Detalle |
|---|---|
| **Descripción** | Se crea una nueva cuenta de usuario local en el endpoint. En PCs de trabajador esto es altamente anómalo: la gestión de usuarios debe centralizarse en el directorio. Patrón típico de persistencia tras compromiso. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4720 (A user account was created). |
| **Lógica de detección** | Regla built-in 60109 (nivel 8). |
| **MITRE ATT&CK** | T1136.001 — Create Local Account |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. |
| **Falsos positivos** | Muy bajos en parque corporativo gestionado. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.IDM.002 — Usuario añadido a grupo Administradores local

| Campo | Detalle |
|---|---|
| **Descripción** | Una cuenta es añadida al grupo de Administradores locales del endpoint. Técnica clásica de elevación de privilegios y persistencia tras compromiso. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Canal Security — Event ID 4732 (A member was added to a security-enabled local group), filtrando por SID `S-1-5-32-544`. |
| **Lógica de detección** | Regla built-in 60154 (nivel 12 cuando aplica al grupo Administradores). |
| **MITRE ATT&CK** | T1098 — Account Manipulation |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — built-in. |
| **Falsos positivos** | Bajos en parque gestionado. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.ACCT.001 — Cuenta local oculta o con nombre camuflado

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante crea una cuenta local con nombre diseñado para pasar desapercibido: nombre idéntico o muy similar a cuentas de sistema legítimas (`Administrator$`, `SYSTEM_`, `svc_backup`), con el sufijo `$` para ocultarla de la salida de `net user`, o con caracteres Unicode que visualmente parecen letras latinas. La cuenta se usa como backdoor persistente que sobrevive incluso si el vector de entrada original es remediado. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4720 con `SamAccountName` que termine en `$`, contenga caracteres Unicode no ASCII, o tenga nombre similar a cuentas de sistema conocidas. Sysmon Event ID 1 — `net.exe` o `net1.exe` con argumentos `user /add` y nombre sospechoso. PowerShell ScriptBlock Event ID 4104 — `New-LocalUser` con nombre camuflado. |
| **Lógica de detección** | Regla custom: Event ID 4720 con `SamAccountName` terminando en `$` → nivel 10 (cuenta oculta a `net user`). Regla: nombre que coincida con patrón de cuenta de sistema con variación mínima → nivel 12. Regla Sysmon: `net user /add` con nombre terminado en `$` → nivel 12. Regla: Event ID 4720 seguido de Event ID 4732 (añadido a Administradores) en 60s → nivel 12. |
| **MITRE ATT&CK** | T1136.001 — Create Account: Local Account / T1564.002 — Hide Artifacts: Hidden Users |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — detección de `$` al final es directa. Detección por similitud con cuentas de sistema requiere CDB list con nombres conocidos del cliente. |
| **Falsos positivos** | Bajos. Cuentas con `$` al final son señal clara de intención de ocultación. |
| **Nota operativa** | Las cuentas con `$` no aparecen en `net user` pero sí en `Get-LocalUser` (PowerShell) o en herramientas forenses. Si se detecta, inventariar todas las cuentas locales del endpoint para identificar otras posibles backdoors. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.ACCT.002 — Reactivación de cuenta deshabilitada o manipulación de atributos

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante reactiva una cuenta de usuario previamente deshabilitada (cuentas de soporte, instalación, empleados antiguos) para usarla como backdoor sin crear una nueva cuenta que pueda llamar la atención. También incluye manipulación de atributos: establecer contraseña que nunca expira, eliminar el requisito de cambio de contraseña, desbloquear cuentas bloqueadas. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4722 (cuenta habilitada) con `SubjectUserName` distinto al propietario de la cuenta. Event ID 4738 (cuenta modificada) con cambio en flags `UserAccountControl` (`PasswordNeverExpires = true`, `PasswordNotRequired = true`). Event ID 4767 (cuenta desbloqueada). Sysmon Event ID 1 — `net user /active:yes` o `net user /expires:never` desde proceso interactivo. |
| **Lógica de detección** | Regla custom: Event ID 4722 (cuenta habilitada) desde cuenta no de helpdesk autorizado → nivel 10. Regla: Event ID 4738 con `PasswordNeverExpires = true` desde cuenta no autorizada → nivel 8. Alta confianza: Event ID 4722 + Event ID 4624 (login exitoso de la cuenta reactivada) en 300s → nivel 12. Correlación: reactivación + Event ID 4732 (añadida a Admins) en 120s → nivel 12. |
| **MITRE ATT&CK** | T1098 — Account Manipulation / T1136.001 — Create Account: Local Account |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere whitelist de cuentas de helpdesk autorizadas para reactivar cuentas y de cuentas de servicio con contraseña que no expira por diseño. |
| **Falsos positivos** | Medios. Helpdesk reactiva cuentas legítimamente. La clave es el contexto: quién reactiva y si se usa inmediatamente después. |
| **Nota operativa** | Mantener inventario actualizado de cuentas deshabilitadas por cliente. Una cuenta deshabilitada hace meses que se reactiva a las 2AM es un indicador claro de backdoor. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.ACCT.003 — Cuenta de servicio o técnica usada como backdoor

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante abusa de una cuenta de servicio o técnica existente (SQL Server, IIS, backup, monitorización) añadiéndola a grupos privilegiados, cambiando su contraseña para mantener acceso exclusivo, o usándola para iniciar sesiones interactivas cuando debería solo usarse para servicios. Las cuentas de servicio son objetivos atractivos por sus privilegios elevados, contraseñas estáticas y menor supervisión. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4624 con `LogonType = 2` o `10` (interactivo) para cuenta con nombre de patrón de servicio (`svc_*`, `_svc`, `sa`, `backup_*`, `monitor_*`). Event ID 4732 (añadida a grupo privilegiado) para cuenta de servicio. Event ID 4723/4724 (cambio de contraseña) en cuenta de servicio por usuario distinto al propietario del servicio. |
| **Lógica de detección** | Regla custom: Event ID 4624 LogonType 2 o 10 desde cuenta con patrón de nombre de servicio → nivel 10 (cuenta de servicio usada interactivamente). Alta confianza: Event ID 4732 (añadir a Admins) para cuenta de servicio → nivel 12. Regla: Event ID 4724 (reset de contraseña de cuenta de servicio) por cuenta no autorizada → nivel 10. Correlación: reset de contraseña de cuenta de servicio + login interactivo de esa cuenta en 300s → nivel 12. |
| **MITRE ATT&CK** | T1078.003 — Valid Accounts: Local Accounts / T1098 — Account Manipulation |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere CDB list de cuentas de servicio conocidas del cliente y sus patrones de uso legítimo. |
| **Falsos positivos** | Medios. Algunas cuentas de servicio tienen logins interactivos legítimos en procedimientos de mantenimiento. Whitelist de ventanas de mantenimiento autorizadas. |
| **Nota operativa** | Realizar un inventario de cuentas de servicio y sus privilegios reales como parte del onboarding de cada cliente — muchas tendrán privilegios excesivos que conviene reducir antes de activar esta ficha. |
| **Estado** | Pendiente de validación. |

---

##### Fichas detalladas — EP-03 (Modificación de GPO locales)

---

###### EP.03.WIN.GPO.001 — Modificación de GPO local para deshabilitar controles de seguridad

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica la Política de Grupo Local para deshabilitar controles de seguridad del endpoint: desactivar Windows Firewall, deshabilitar Windows Defender, reducir la política de contraseñas, deshabilitar UAC, permitir la ejecución de scripts PowerShell sin restricciones (`ExecutionPolicy = Unrestricted`). Los cambios de GPO local afectan al endpoint independientemente de las GPOs del dominio y pueden sobrevivir a la desconexión del dominio. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — modificación de claves bajo `HKLM\SOFTWARE\Policies\Microsoft\Windows\`, `\Policies\Microsoft\Windows Defender\`, `\Policies\Microsoft\Windows\PowerShell\`. Security log — Event ID 4719 (audit policy changed). Sysmon Event ID 1 — `secedit.exe /configure` desde proceso no autorizado. |
| **Lógica de detección** | Regla Sysmon: Event ID 13 con `TargetObject` conteniendo `\Windows Defender\DisableAntiSpyware = 1` o `DisableRealtimeMonitoring = 1` → nivel 12. Regla: `\Policies\Microsoft\Windows\PowerShell\ExecutionPolicy` con valor `Unrestricted` o `Bypass` → nivel 10. Regla: modificación de `\WindowsFirewall\` deshabilitando el firewall → nivel 10. Correlación: múltiples modificaciones de políticas de seguridad en 300s → nivel 12 (desmantelamiento sistemático de controles). |
| **MITRE ATT&CK** | T1562.001 — Impair Defenses: Disable or Modify Tools / T1562.002 — Disable Windows Event Logging / T1562.004 — Disable or Modify System Firewall |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — claves de registro de GPO específicas. FP bajo en entornos correctamente gestionados donde las GPOs se aplican desde el DC. |
| **Falsos positivos** | Bajos. Modificaciones de GPO local legítimas son raras en endpoints de dominio. |
| **Nota operativa** | En endpoints de dominio, revisar también si las GPOs del dominio están siendo bloqueadas (`Block Inheritance`) en la OU del endpoint cuando dispara esta ficha. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.GPO.002 — Modificación de GPO local para establecer persistencia

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica la GPO local para registrar scripts de inicio, apagado, logon o logoff que ejecutan código malicioso en cada arranque o sesión de usuario. A diferencia de BOOT.002 (carpetas Startup) y LOGON.002 (scripts en el registro), esta ficha se centra en la configuración de scripts a través del mecanismo de GPO local — más difícil de detectar porque los scripts pueden estar en rutas de sistema aparentemente legítimas. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.3 Compromiso de aplicaciones |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 11 — creación o modificación de ficheros en `C:\Windows\System32\GroupPolicy\Machine\Scripts\` o `C:\Windows\System32\GroupPolicy\User\Scripts\`. FIM — modificación de `scripts.ini` en subdirectorios Startup, Shutdown, Logon, Logoff de GroupPolicy. Sysmon Event ID 1 — `gpedit.msc` o `secedit.exe` ejecutados desde proceso no administrativo. |
| **Lógica de detección** | Regla Sysmon: Event ID 11 con `TargetFilename` conteniendo `\GroupPolicy\Machine\Scripts\Startup\` o `\GroupPolicy\User\Scripts\Logon\` por proceso no de administración → nivel 12. Regla FIM: modificación de `scripts.ini` en cualquier subdirectorio de GroupPolicy → nivel 10. Regla: creación de script (`.bat`, `.vbs`, `.ps1`) en directorio de GroupPolicy por proceso interactivo → nivel 12. |
| **MITRE ATT&CK** | T1037.001 — Boot or Logon Initialization Scripts: Logon Script (Windows) / T1037.003 — Network Logon Script |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — FIM sobre los directorios de GroupPolicy es el mecanismo principal. Requiere configurar correctamente las rutas en `agent.conf`. |
| **Falsos positivos** | Bajos. Modificaciones de scripts de GPO local son raras en endpoints de dominio gestionados. |
| **Estado** | Pendiente de validación. |

---

###### EP.03.WIN.GPO.003 — Manipulación directa de ficheros de GPO local (GptTmpl.inf, Registry.pol)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante modifica directamente los ficheros de configuración de la GPO local para alterar políticas de seguridad sin usar las herramientas estándar: `GptTmpl.inf` (configuración de seguridad: contraseñas, auditoría, derechos de usuario), `Registry.pol` (configuración de registro aplicada por GPO), `gpt.ini` (versión de la GPO). La modificación directa es más sigilosa porque puede no generar los mismos eventos de auditoría que el uso de herramientas de gestión. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | FIM — modificación de `C:\Windows\System32\GroupPolicy\Machine\Microsoft\Windows NT\SecEdit\GptTmpl.inf`, `C:\Windows\System32\GroupPolicy\Machine\Registry.pol`, `\User\Registry.pol`, `C:\Windows\System32\GroupPolicy\gpt.ini`. Sysmon Event ID 11 — escritura en cualquiera de estos ficheros por proceso no de herramientas de administración de GPO. |
| **Lógica de detección** | Regla FIM: modificación de `GptTmpl.inf` por proceso distinto a `gpedit.msc`, `secedit.exe`, `mmc.exe` o agente autorizado → nivel 12. Regla: modificación de `Registry.pol` por proceso no de gestión de GPO → nivel 10. Correlación: modificación de `gpt.ini` + modificación de `GptTmpl.inf` o `Registry.pol` en 60s → nivel 12 (actualización completa de GPO local). |
| **MITRE ATT&CK** | T1484.001 — Domain Policy Modification: Group Policy Modification / T1562.001 — Impair Defenses |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — rutas de fichero muy específicas. FIM sobre los ficheros de GPO local es suficiente y de bajo volumen. |
| **Falsos positivos** | Muy bajos. Modificación directa de `GptTmpl.inf` o `Registry.pol` fuera de herramientas de administración es prácticamente siempre anómala. |
| **Nota operativa** | Los cambios no se aplican inmediatamente — se aplican en el siguiente refresh de GPO (90 minutos por defecto o en reinicio/logon). Actuar antes del siguiente refresh para evitar que los cambios surtan efecto. El campo `Details` de FIM muestra el contenido modificado — revisar qué configuración exacta ha cambiado. |
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

##### Fichas detalladas — EP-04 (Robo de credenciales avanzado)

---

###### EP.04.WIN.SAM.001 — Acceso a SAM/SYSTEM/SECURITY para extracción de hashes

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante intenta acceder o copiar los ficheros SAM, SYSTEM y SECURITY del registro de Windows para extraer los hashes NTLM de las cuentas locales offline. SAM contiene los hashes de contraseñas de cuentas locales cifrados con la clave SYSKEY almacenada en SYSTEM. Con ambos ficheros, herramientas como `secretsdump.py` o Mimikatz (`lsadump::sam`) pueden extraer todos los hashes sin necesidad de acceder a LSASS en caliente. Técnica frecuente como alternativa a LSASS dumping cuando PPL está activo. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 11 — creación de copia de `SAM`, `SYSTEM` o `SECURITY` en ruta temporal. Sysmon Event ID 1 — `reg.exe save HKLM\SAM`, `reg.exe save HKLM\SYSTEM`, `reg.exe save HKLM\SECURITY` desde proceso no de backup autorizado. PowerShell ScriptBlock Event ID 4104 — acceso directo a claves SAM. Security log — Event ID 4656 (handle requested to SAM object) con acceso de lectura desde proceso no de sistema. Sysmon Event ID 1 — `vssadmin create shadow` seguido de copia de ficheros SAM desde shadow copy. |
| **Lógica de detección** | Regla Sysmon alta confianza: `reg.exe` con argumentos `save HKLM\SAM` o `save HKLM\SYSTEM` → nivel 12. Regla: `vssadmin.exe create shadow` desde proceso no de backup + creación de fichero `SAM` en ruta temporal en 300s → nivel 12 (VSS SAM dump). Regla: `ntdsutil.exe` con argumento `ifm` → nivel 12. Regla PowerShell: acceso a `HKLM:\SAM\SAM\Domains\Account\Users` → nivel 10. |
| **MITRE ATT&CK** | T1003.002 — OS Credential Dumping: Security Account Manager / T1003.003 — NTDS |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — comandos de volcado de SAM muy específicos y raramente legítimos. |
| **Falsos positivos** | Muy bajos. `reg save HKLM\SAM` fuera de procesos de backup documentados es prácticamente siempre malicioso. |
| **Recomendación de hardening** | Restringir acceso a `reg save` de claves sensibles mediante GPO. Monitorizar y limitar el uso de VSS a cuentas de backup autorizadas. |
| **Estado** | Pendiente de validación. |

---

###### EP.04.WIN.TOKEN.001 — Extracción y abuso de tokens de acceso

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante roba o duplica tokens de acceso de procesos privilegiados para ejecutar código en ese contexto de seguridad sin conocer las credenciales del usuario. Esta ficha cubre el robo de tokens como técnica de acceso a credenciales y recursos, complementando PRIVESC.002 que lo cubre desde el ángulo de escalada de privilegios. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4624 con `ImpersonationLevel = Impersonation` o `Delegation` desde proceso no de sistema. Event ID 4648 (explicit credentials used) desde proceso interactivo. Sysmon Event ID 8 (CreateRemoteThread) hacia proceso con token privilegiado. PowerShell ScriptBlock Event ID 4104 — `[System.Security.Principal.WindowsIdentity]::Impersonate`, `DuplicateToken`, `ImpersonateLoggedOnUser`. |
| **Lógica de detección** | Regla Security log: Event ID 4648 desde proceso no administrativo conocido con cuenta distinta al usuario de la sesión → nivel 8. Regla: Event ID 4624 con `ImpersonationLevel = Delegation` desde proceso de usuario estándar → nivel 10. Regla PowerShell: `Impersonate`, `DuplicateToken`, `ImpersonateLoggedOnUser` desde proceso no de gestión → nivel 10. Correlación: `runas /savecred` + acceso a recurso privilegiado en 60s → nivel 10. |
| **MITRE ATT&CK** | T1134 — Access Token Manipulation / T1134.001 — Token Impersonation/Theft / T1134.003 — Make and Impersonate Token |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere distinguir usos legítimos de impersonation (servicios de sistema) de usos maliciosos. El campo `ImpersonationLevel` es el discriminador clave. |
| **Falsos positivos** | Medios. Muchos servicios legítimos usan impersonation. La combinación con proceso origen no de sistema y cuenta destino privilegiada reduce los FP. |
| **Estado** | Pendiente de validación. |

---

###### EP.04.WIN.BROWSER.001 — Robo de cookies y credenciales de navegador

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante extrae credenciales guardadas, cookies de sesión y tokens de autenticación almacenados por los navegadores web (Chrome, Edge, Firefox). Las credenciales se cifran con DPAPI ligado al perfil del usuario — desde el contexto del usuario comprometido pueden descifrarse sin contraseña adicional. Las cookies de sesión permiten bypasear MFA completamente. Técnica muy frecuente en infostealers (Redline, Vidar, Raccoon) y en post-explotación manual. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 11 — acceso de lectura a ficheros de credenciales de navegador: `C:\Users\*\AppData\Local\Google\Chrome\User Data\Default\Login Data`, `\Default\Cookies`, `AppData\Local\Microsoft\Edge\User Data\Default\Login Data`, `AppData\Roaming\Mozilla\Firefox\Profiles\*\logins.json`, `key4.db`. Sysmon Event ID 1 — herramientas conocidas (`SharpChrome.exe`, `HackBrowserData.exe`, `BrowserGhost.exe`). |
| **Lógica de detección** | Regla Sysmon: Event ID 11 con `TargetFilename` conteniendo `\Chrome\User Data\Default\Login Data` o `\Edge\User Data\Default\Login Data` desde proceso distinto al navegador → nivel 10. Crítica: mismo patrón desde proceso en `%TEMP%` o `%APPDATA%` → nivel 12. Regla Event ID 1: `Image` conteniendo `sharpchrome`, `hackbrowserdata`, `browserghost`, `chromecookiesview` → nivel 12. Correlación: acceso a `Login Data` de Chrome + Edge + `logins.json` de Firefox desde mismo proceso en 60s → nivel 12 (recolección masiva). |
| **MITRE ATT&CK** | T1555.003 — Credentials from Web Browsers / T1539 — Steal Web Session Cookie |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — rutas de ficheros de credenciales de navegador fijas y bien conocidas. Alta confianza al detectar proceso no-navegador accediendo a estos ficheros. |
| **Falsos positivos** | Bajos. Gestores de contraseñas legítimos acceden a sus propios ficheros, no a los del navegador. |
| **Nota operativa** | Las cookies de sesión robadas permiten bypasear MFA completamente. Si se detecta esta ficha, invalidar todas las sesiones activas del usuario en servicios web críticos (M365, CRM, banca) de forma inmediata. |
| **Estado** | Pendiente de validación. |

---

###### EP.04.WIN.VAULT.001 — Acceso a Credential Manager y vaults locales

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante extrae credenciales almacenadas en el Credential Manager de Windows (credenciales de red, credenciales genéricas, certificados). El Credential Manager puede contener credenciales de dominio, VPN, RDP y servicios cloud. Técnicas: `cmdkey /list` para enumerar, Mimikatz `dpapi::cred`, `vaultcmd /list`, acceso directo a `%APPDATA%\Microsoft\Credentials\`. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `cmdkey.exe /list` o `vaultcmd.exe /list` desde proceso interactivo no administrativo. PowerShell ScriptBlock Event ID 4104 — `[Windows.Security.Credentials.PasswordVault]::new()`, `Get-StoredCredential`. Sysmon Event ID 11 — acceso de lectura a `%APPDATA%\Microsoft\Credentials\` desde proceso no de sistema. Sysmon Event ID 1 — Mimikatz con módulo `dpapi::cred` o `sekurlsa::dpapi`. |
| **Lógica de detección** | Regla Sysmon: `cmdkey.exe` con argumento `/list` desde proceso interactivo → nivel 6. Regla: `vaultcmd.exe` con `/list` desde proceso no administrativo → nivel 8. Regla: acceso de lectura a `%APPDATA%\Microsoft\Credentials\` desde proceso distinto a `lsass.exe` o `svchost.exe` → nivel 10. Crítica: Mimikatz con módulo `dpapi` → nivel 12. Correlación: `cmdkey /list` + acceso a directorio Credentials en 120s → nivel 10. |
| **MITRE ATT&CK** | T1555.004 — Credentials from Windows Credential Manager / T1555 — Credentials from Password Stores |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — acceso al directorio Credentials puede generar FP con procesos de sistema. La combinación enumeración + acceso al directorio es el indicador de mayor confianza. |
| **Falsos positivos** | Medios. `cmdkey /list` tiene uso legítimo frecuente. Discriminador: proceso origen interactivo vs proceso de sistema. |
| **Estado** | Pendiente de validación. |

---

###### EP.04.WIN.PLAIN.001 — Credenciales en texto plano en ficheros, scripts y registro

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante busca credenciales almacenadas en texto plano en el endpoint: ficheros de configuración con contraseñas hardcodeadas (`.config`, `.xml`, `.ini`, `.env`, `web.config`), scripts PowerShell o batch con credenciales, claves de registro con contraseñas, historial de comandos PowerShell (`ConsoleHost_history.txt`), ficheros de respuesta de instalación (`unattend.xml`, `sysprep.inf`). Muchos entornos corporativos tienen credenciales en texto plano en ubicaciones predecibles. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `findstr /si password`, `Select-String -Pattern password`, `grep -r password`. PowerShell ScriptBlock Event ID 4104 — búsqueda de patrones de credenciales en ficheros. Sysmon Event ID 11 — acceso de lectura a `C:\Windows\Panther\unattend.xml`, `C:\Windows\system32\sysprep\unattend.xml`, `C:\Windows\system32\sysprep\sysprep.inf`. |
| **Lógica de detección** | Regla Sysmon: `findstr.exe` con `/si` y término `password`, `passwd`, `credential`, `secret`, `apikey` → nivel 8. Regla PowerShell: `Select-String` + patrón de credencial en múltiples ficheros en 60s → nivel 10. Alta confianza: acceso de lectura a `unattend.xml` o `sysprep.inf` desde proceso no de instalación → nivel 10. Regla: acceso a `ConsoleHost_history.txt` desde proceso no de PowerShell → nivel 8. Correlación: `findstr` con término de credencial + acceso a múltiples ficheros de configuración en 300s → nivel 12. |
| **MITRE ATT&CK** | T1552.001 — Unsecured Credentials: Credentials In Files / T1552.002 — Credentials in Registry / T1552.004 — Private Keys |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — `findstr` con términos de credencial puede generar volumen alto. El parámetro `/si` (recursivo) y la correlación con múltiples accesos son los discriminadores clave. |
| **Falsos positivos** | Medios. Desarrolladores y administradores buscan ficheros de configuración legítimamente. La búsqueda recursiva desde directorios de sistema es el indicador de actividad maliciosa. |
| **Nota operativa** | Si se detecta acceso a `unattend.xml` o `sysprep.inf`, revisar inmediatamente su contenido — con frecuencia contienen la contraseña del administrador local en texto plano. Si contienen credenciales, forzar reset en todos los endpoints desplegados con esa imagen. |
| **Estado** | Pendiente de validación. |

---

##### EP-05 — Movimiento lateral

> ¿Este endpoint está siendo usado para moverse hacia otros sistemas?

---

##### Fichas detalladas — EP-05 (Movimiento lateral)

---

###### EP.05.WIN.LAT.001 — Conexiones RDP laterales entre endpoints

| Campo | Detalle |
|---|---|
| **Descripción** | Un endpoint establece conexiones RDP hacia otros endpoints de la red interna — no desde Internet sino de máquina a máquina dentro de la red corporativa. En entornos bien gestionados, RDP lateral entre endpoints de usuario es anómalo: los administradores se conectan desde jumpboxes, no desde PCs de usuario. Patrón habitual de movimiento lateral tras comprometer un endpoint de usuario. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 3 — conexión TCP saliente desde `mstsc.exe` hacia IP interna en puerto 3389. Security log — Event ID 4648 con aplicación `TERMSRV/` seguido de IP interna. En el sistema destino: Event ID 4624 LogonType 10 con IP origen de otro endpoint de usuario. |
| **Lógica de detección** | Regla Sysmon: Event ID 3 con `Image = mstsc.exe` y `DestinationPort = 3389` hacia IP interna desde equipo de usuario estándar → nivel 8. Alta prioridad: Event ID 4624 LogonType 10 en endpoint de usuario con `IpAddress` de otro endpoint de usuario (no jumpbox) → nivel 10. Correlación: `mstsc.exe` iniciando conexión + Event ID 4624 LogonType 10 en destino en 60s → nivel 12. Regla adicional: mismo endpoint iniciando RDP a 3+ hosts distintos en 300s → nivel 12 (RDP scanning lateral). |
| **MITRE ATT&CK** | T1021.001 — Remote Services: Remote Desktop Protocol |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere CDB list de IPs de jumpboxes y servidores de administración autorizados. |
| **Falsos positivos** | Medios. Soporte técnico usa RDP entre equipos legítimamente. La clave es el origen: RDP desde PC de usuario estándar es sospechoso; desde jumpbox es normal. |
| **Diferencia con NET.01.WIN.RDP.001** | NET.01.WIN.RDP.001 detecta RDP entrante desde Internet. Esta ficha detecta RDP lateral interno entre IPs internas. |
| **Estado** | Pendiente de validación. |

---

###### EP.05.WIN.LAT.002 — Acceso a shares administrativos (C$, ADMIN$, IPC$)

| Campo | Detalle |
|---|---|
| **Descripción** | Un endpoint accede a los shares administrativos ocultos de otro sistema interno: `C$` (raíz del disco C), `ADMIN$` (directorio de Windows), `IPC$` (comunicación entre procesos). El acceso a estos shares requiere credenciales de administrador local y es el mecanismo subyacente de herramientas como PsExec, Impacket y CrackMapExec para el movimiento lateral. El acceso desde un endpoint de usuario a shares administrativos de otro endpoint es altamente anómalo. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log en el sistema destino — Event ID 5140 con `ShareName` = `\\*\C$`, `\\*\ADMIN$`, `\\*\IPC$` y `IpAddress` de otro endpoint de usuario. Event ID 5145 con shares administrativos. En el sistema origen: Sysmon Event ID 3 — conexión TCP a puerto 445 de host interno desde proceso no de backup o administración autorizado. |
| **Lógica de detección** | Regla Security log: Event ID 5140 con `ShareName` conteniendo `C$` o `ADMIN$` desde IP que no sea servidor de administración o backup → nivel 10. Crítica: mismo patrón con cuenta de usuario estándar → nivel 12. Regla Sysmon: Event ID 3 desde `net.exe`, `cmd.exe`, `powershell.exe` a puerto 445 de host interno → nivel 8. Correlación: acceso a `C$` + creación de fichero en la ruta accedida en 300s → nivel 12 (acceso + staging confirmado). |
| **MITRE ATT&CK** | T1021.002 — Remote Services: SMB/Windows Admin Shares / T1570 — Lateral Tool Transfer |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere que el sistema destino tenga agente Wazuh y auditoría de Object Access activa. |
| **Falsos positivos** | Medios. Backups, SCCM y herramientas de gestión acceden a shares administrativos legítimamente. Whitelist de cuentas de servicio y servidores de gestión autorizados. |
| **Nota operativa** | El acceso a `IPC$` puede ser legítimo. El acceso a `C$` o `ADMIN$` desde un endpoint de usuario es siempre sospechoso y merece investigación inmediata. |
| **Estado** | Pendiente de validación. |

---

###### EP.05.WIN.LAT.003 — Autenticaciones NTLM laterales inusuales

| Campo | Detalle |
|---|---|
| **Descripción** | Un endpoint genera un volumen inusual de autenticaciones NTLM hacia múltiples hosts internos en ventana corta — patrón de movimiento lateral mediante Pass-the-Hash o uso de credenciales robadas para pivotar entre sistemas. A diferencia de EP.02.WIN.CRED.002 (que detecta PTH desde el DC), esta ficha se centra en el patrón de autenticaciones laterales desde el endpoint origen. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 4.2 Intento de acceso con vulneración de credenciales |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log en el endpoint origen — Event ID 4648 hacia múltiples `TargetServerName` distintos en ventana corta. Security log en endpoints destino — Event ID 4624 LogonType 3 con `AuthenticationPackageName = NTLM` desde la misma IP origen. Sysmon Event ID 3 — múltiples conexiones TCP a puerto 445 o 135 de hosts internos distintos desde proceso interactivo. |
| **Lógica de detección** | Regla correlación: Event ID 4648 hacia 3+ `TargetServerName` distintos en 300s → nivel 10. Crítica: misma cuenta con Event ID 4624 LogonType 3 NTLM en 3+ endpoints distintos en 300s → nivel 12 (PTH lateral confirmado). Regla Sysmon: proceso interactivo iniciando conexiones a puerto 445 de 5+ IPs internas en 60s → nivel 10. |
| **MITRE ATT&CK** | T1550.002 — Pass the Hash / T1021.002 — SMB/Windows Admin Shares / T1078 — Valid Accounts |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — requiere correlación entre eventos de múltiples endpoints. La normalización del campo de IP origen es el principal reto técnico. |
| **Falsos positivos** | Medios. Scripts de administración y herramientas de monitorización generan autenticaciones hacia múltiples hosts. Whitelist de cuentas de servicio y servidores de administración. |
| **Relación con otros CU** | Complementa EP.02.WIN.CRED.002 (PTH visto desde el DC) con visibilidad desde el endpoint origen y los endpoints destino. |
| **Estado** | Pendiente de validación. |

---

###### EP.05.WIN.LAT.004 — Herramientas administrativas usadas fuera de patrón

| Campo | Detalle |
|---|---|
| **Descripción** | Herramientas de administración remota legítimas (RSAT, MMC remoto, WMIC remoto, WinRM, `dsquery`, `nltest`) son usadas desde un endpoint de usuario estándar — indicador de Living off the Land lateral. Estas herramientas son confiables para el sistema operativo pero su uso desde un PC de usuario hacia múltiples destinos o fuera de horario es indicador de actividad maliciosa. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `wmic.exe` con argumento `/node:`, `winrs.exe`, `dsquery.exe` con scope de dominio, `nltest.exe /dclist` o `/domain_trusts`, `net.exe` con comandos de administración remota. PowerShell ScriptBlock Event ID 4104 — `Invoke-Command -ComputerName`, `Enter-PSSession -ComputerName`, `Get-WmiObject -ComputerName`. |
| **Lógica de detección** | Regla Sysmon: `wmic.exe` con `/node:` desde endpoint de usuario → nivel 8. `winrs.exe` desde proceso interactivo → nivel 10. `dsquery.exe` con scope completo de dominio desde endpoint de usuario → nivel 8. Regla PowerShell: `Invoke-Command -ComputerName` hacia IP interna desde equipo de usuario → nivel 10. Regla fuera de horario: cualquiera de las anteriores entre 22:00-07:00 → nivel +2. Correlación: 3+ herramientas administrativas distintas desde mismo endpoint en 300s → nivel 12. |
| **MITRE ATT&CK** | T1021.006 — Remote Services: Windows Remote Management / T1047 — Windows Management Instrumentation / T1069 — Permission Groups Discovery |
| **Severidad** | Media / Alta (según contexto) |
| **Esfuerzo** | Medio — requiere CDB list de endpoints de usuario vs servidores de administración para contextualizar. |
| **Falsos positivos** | Medios. Administradores de sistemas usan estas herramientas legítimamente. La clave es el origen: PC de usuario estándar vs servidor de administración. |
| **Estado** | Pendiente de validación. |

---

###### EP.05.WIN.LAT.005 — Correlación: perfil de movimiento lateral activo

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la combinación de señales que configura un perfil de movimiento lateral activo: acceso a shares administrativos + autenticaciones laterales + herramientas de administración remota + conexiones RDP internas desde el mismo origen en ventana temporal. La correlación de múltiples señales confirma el incidente e identifica el endpoint pivote. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.05.WIN.LAT.001-004 y EP.02.WIN.EXEC.001-004 en el mismo `hostname` o `src_ip` en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: 2+ alertas de distintas fichas LAT.00* desde el mismo `src_ip` en 600s → nivel 12. Máxima prioridad: LAT.002 (admin shares) + LAT.003 (NTLM lateral) en mismo origen en 300s → nivel 12. Correlación extendida: cualquier LAT.00* + EP.02.WIN.CRED.00* en mismo hostname en 3600s → nivel 12. |
| **MITRE ATT&CK** | T1021 — Remote Services / T1550 — Use Alternate Authentication Material / T1570 — Lateral Tool Transfer |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que las fichas LAT.001-004 estén operativas y campos IP normalizados. |
| **Falsos positivos** | Muy bajos. Combinación de múltiples técnicas de movimiento lateral en ventana corta es prácticamente siempre un incidente real. |
| **Nota operativa** | Cuando dispara, el endpoint origen es el pivote comprometido — contener origen y destinos simultáneamente. Iniciar respuesta a incidentes: aislamiento, volcado de memoria del endpoint origen, revisión de todos los destinos alcanzados. |
| **Prerequisito** | Fichas EP.05.WIN.LAT.001-004 operativas y campos IP normalizados. |
| **Estado** | Pendiente de validación. |

---

##### EP-06 — Exfiltración o preparación de exfiltración

> ¿Se están preparando o sacando datos desde el endpoint?

---

##### Fichas detalladas — EP-06 (Exfiltración)

---

###### EP.06.WIN.EXFIL.001 — Herramientas de transferencia de ficheros (rclone, WinSCP, curl, scp, ftp)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa herramientas de transferencia de ficheros para exfiltrar datos desde el endpoint hacia un destino externo: `rclone` (sincronización con cloud storage), `WinSCP` (SFTP/SCP gráfico), `pscp.exe` (SCP de PuTTY), `curl` o `wget` con método PUT/POST, cliente FTP nativo. El indicador de exfiltración es el contexto: volumen de datos, destino externo, fuera de horario, proceso padre anómalo. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 7.4 Pérdida de datos |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `rclone.exe`, `WinSCP.exe`, `pscp.exe`, `psftp.exe`, `ftp.exe` con argumentos de transferencia hacia IP externa. `curl.exe` o `wget.exe` con método `PUT`, `POST` o `--upload-file` hacia URL externa. PowerShell ScriptBlock Event ID 4104 — `Invoke-WebRequest` con método `PUT` o `POST` con fichero adjunto. Sysmon Event ID 3 — conexión saliente desde estas herramientas hacia IP externa en puertos 21, 22, 443. Sysmon Event ID 11 — creación de `rclone.conf` con credenciales de cloud storage. |
| **Lógica de detección** | Regla Sysmon: `rclone.exe` ejecutado desde endpoint de usuario → nivel 10. Crítica: `rclone.exe` con argumento `copy` o `sync` hacia destino remoto → nivel 12. Regla: `pscp.exe` o `psftp.exe` con argumento de ruta local + destino externo → nivel 10. Regla: `ftp.exe` iniciando conexión saliente + comandos `put` o `mput` → nivel 10. Regla: `curl.exe` con `--upload-file` o `-T` hacia URL externa → nivel 8. Correlación: herramienta de transferencia + fichero comprimido en `%TEMP%` en 600s → nivel 12. |
| **MITRE ATT&CK** | T1048 — Exfiltration Over Alternative Protocol / T1048.003 — Exfiltration Over Unencrypted Non-C2 Protocol / T1567 — Exfiltration Over Web Service |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo-Medio — `rclone` y `pscp` raramente tienen uso legítimo en endpoints de usuario. `curl` y `ftp` tienen más FP — el argumento de upload es el discriminador. |
| **Falsos positivos** | Medios para `curl` y `ftp`. Muy bajos para `rclone` y `pscp` en endpoints corporativos. |
| **Nota operativa** | `rclone.conf` puede contener tokens de acceso a cloud storage — si se detecta su creación, revisar el contenido para identificar el servicio destino y revocar los tokens inmediatamente. |
| **Estado** | Pendiente de validación. |

---

###### EP.06.WIN.EXFIL.002 — Subida a servicios cloud no autorizados

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario o proceso sube datos corporativos a servicios cloud de almacenamiento o compartición no autorizados: Dropbox personal, Mega, WeTransfer, Pastebin, file.io, transfer.sh, Google Drive personal, OneDrive personal. La detección combina URL Filtering de Palo Alto con la actividad de procesos del navegador y herramientas de sincronización no autorizadas. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 7.4 Pérdida de datos |
| **Peligrosidad** | ALTO |
| **Telemetría** | Palo Alto URL Filtering log — acceso a categorías `file-sharing`, `storage-backup` hacia dominios no autorizados (`mega.nz`, `wetransfer.com`, `dropbox.com` personal, `pastebin.com`, `file.io`). Sysmon Event ID 3 — conexión saliente desde navegador hacia IP de servicios cloud no autorizados con volumen de datos enviados elevado. Sysmon Event ID 1 — cliente de sincronización no autorizado (`MEGAsync.exe`, `Dropbox.exe` en ruta de usuario) instalado/ejecutado. |
| **Lógica de detección** | Regla PA URL Filtering: acceso a `mega.nz`, `wetransfer.com`, `pastebin.com`, `file.io`, `transfer.sh` → nivel 6. Correlación: URL Filtering hacia file-sharing + volumen de datos subidos > 10MB → nivel 10. Regla Sysmon: cliente de sincronización no autorizado ejecutado desde endpoint corporativo → nivel 8. Crítica: cualquiera de las anteriores + fichero comprimido creado recientemente en 600s → nivel 12. |
| **MITRE ATT&CK** | T1567.002 — Exfiltration to Cloud Storage / T1048 — Exfiltration Over Alternative Protocol |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere URL Filtering activo en Palo Alto. Sin PA la detección depende de procesos de cliente de sincronización (cobertura parcial). |
| **Falsos positivos** | Medios. Empleados usan servicios cloud personales legítimamente. La correlación con volumen de datos y ficheros comprimidos recientes es el discriminador. |
| **Estado** | Pendiente de validación. |

---

###### EP.06.WIN.EXFIL.003 — Copia masiva a dispositivos USB

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario o proceso copia un volumen anómalo de ficheros a un dispositivo USB conectado al endpoint. Los dispositivos USB son un vector de exfiltración frecuente en insider threats y en ataques con acceso físico. La detección combina el evento de conexión del dispositivo, el volumen de ficheros copiados y la sensibilidad de los datos accedidos antes de la copia. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 7.4 Pérdida de datos |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 6416 (A new external device was recognized) con `ClassName = DiskDrive` o `USB`. Sysmon Event ID 11 — creación masiva de ficheros en ruta de letra de unidad USB (`D:\`, `E:\`, `F:\`). Sysmon Event ID 1 — `robocopy.exe`, `xcopy.exe` con destino en letra de unidad USB. FIM — acceso de lectura masivo a carpetas de documentos seguido de escritura en unidad USB. |
| **Lógica de detección** | Regla Security log: Event ID 6416 con dispositivo USB de almacenamiento → nivel 4. Correlación: Event ID 6416 + creación de 50+ ficheros en la unidad USB en 300s → nivel 10. Crítica: Event ID 6416 + copia de ficheros con extensiones sensibles (`.docx`, `.xlsx`, `.pdf`, `.pst`, `.db`, `.sql`, `.bak`) en volumen > 100MB en 600s → nivel 12. Regla: `robocopy` o `xcopy` con destino en unidad USB desde proceso interactivo fuera de horario → nivel 10. |
| **MITRE ATT&CK** | T1052.001 — Exfiltration Over Physical Medium: Exfiltration over USB |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — requiere configurar monitorización de letras de unidad removibles en FIM. El umbral debe ajustarse al baseline del cliente. |
| **Falsos positivos** | Medios. Empleados copian ficheros a USB legítimamente. El discriminador es el volumen y tipo de ficheros. En clientes con política de USB bloqueado por GPO esta ficha no aplica. |
| **Recomendación de hardening** | Implementar política de control de dispositivos USB (Windows Device Control o SentinelOne Device Control) para bloquear o limitar el uso de USB en endpoints corporativos. |
| **Estado** | Pendiente de validación. |

---

###### EP.06.WIN.EXFIL.004 — Acceso masivo a carpetas sensibles o fuera de horario

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario o proceso accede a un volumen inusualmente alto de ficheros en carpetas sensibles del endpoint o de shares de red, o realiza este acceso fuera del horario laboral habitual. Patrón de recolección de datos previo a la exfiltración, insider threat con descarga masiva antes de abandonar la empresa, o acceso con credenciales robadas. Complementa EP.02.WIN.POST.005 (compresión) con la fase previa de acceso y recolección. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 8.1 Uso no autorizado de recursos |
| **Peligrosidad** | ALTO |
| **Telemetría** | FIM — acceso de lectura masivo a `C:\Users\*\Documents\`, `\Desktop\`, `\Downloads\`, directorios de proyecto, shares de red montados. Sysmon Event ID 11 — creación de ficheros en ruta temporal con nombres copiados desde carpetas de documentos. Security log — Event ID 4663 (Object Access — fichero abierto) en volumen anómalo desde misma cuenta en ventana corta. Sysmon Event ID 1 — `xcopy`, `robocopy`, `Copy-Item` con origen en carpetas sensibles y destino en ruta temporal. |
| **Lógica de detección** | Regla FIM: acceso de lectura a 100+ ficheros en `C:\Users\*\Documents\` en 300s desde proceso no de backup → nivel 8. Crítica: acceso a ficheros con extensiones sensibles (`.docx`, `.pdf`, `.xlsx`, `.pst`, `.msg`, `.kdbx`) en volumen > 500 ficheros en 600s → nivel 10. Regla fuera de horario: acceso masivo a carpetas sensibles entre 22:00-06:00 → nivel +2. Correlación: acceso masivo a documentos + compresión (EP.02.WIN.POST.005) en 600s → nivel 12. |
| **MITRE ATT&CK** | T1005 — Data from Local System / T1074.001 — Data Staged: Local Data Staging / T1083 — File and Directory Discovery |
| **Severidad** | Alta |
| **Esfuerzo** | Medio-Alto — FIM sobre carpetas de usuario genera volumen alto de eventos. El umbral debe calibrarse con el baseline de actividad normal del cliente. |
| **Falsos positivos** | Medios. Indexación de Windows, antivirus y backup generan el mismo patrón. Whitelist de procesos de indexación y backup conocidos. |
| **Nota operativa** | Especialmente relevante para detección de insider threats en periodos críticos: empleados próximos a salida, procesos de M&A, empleados que han recibido oferta de empresa competidora. |
| **Estado** | Pendiente de validación. |

---

###### EP.06.WIN.EXFIL.005 — Correlación: preparación y exfiltración confirmada

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la cadena completa de exfiltración: acceso masivo a datos + compresión/staging + transferencia hacia el exterior. La correlación de las tres fases confirma exfiltración activa con alta confianza y permite al SOC intervenir — idealmente cortando la transferencia antes de que todos los datos hayan salido. |
| **Clasificación GrayHats** | 7.1 Acceso no autorizado a información / 7.4 Pérdida de datos |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.06.WIN.EXFIL.001-004 y EP.02.WIN.POST.005 en el mismo `hostname` en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: EXFIL.004 (acceso masivo) + EP.02.WIN.POST.005 (compresión) en mismo hostname en 1800s → nivel 12 (staging confirmado, exfiltración inminente). Regla crítica: POST.005 (compresión) + EXFIL.001 o EXFIL.002 (transferencia) en mismo hostname en 600s → nivel 12. Máxima prioridad: EXFIL.004 + POST.005 + EXFIL.001 en mismo hostname en 3600s → nivel 12 (cadena completa confirmada). |
| **MITRE ATT&CK** | T1005 — Data from Local System / T1560 — Archive Collected Data / T1048 — Exfiltration Over Alternative Protocol / T1567 — Exfiltration Over Web Service |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que fichas EXFIL.001-004 y POST.005 estén operativas. |
| **Falsos positivos** | Muy bajos. La cadena acceso masivo + compresión + transferencia en 1 hora es prácticamente siempre exfiltración real o ejercicio de red team. |
| **Nota operativa** | El objetivo es intervenir antes de que la transferencia complete — bloquear la conexión saliente en el firewall, aislar el endpoint y notificar al cliente. Documentar el volumen de datos que puede haber salido antes de la detección para el informe de impacto. |
| **Prerequisito** | Fichas EP.06.WIN.EXFIL.001-004 y EP.02.WIN.POST.005 operativas. |
| **Estado** | Pendiente de validación. |

---

##### EP-07 — Uso anómalo de herramientas legítimas (LOLBins)

> ¿Se están usando herramientas legítimas de forma ofensiva?

---

##### Fichas detalladas — EP-07 (LOLBins)

---

###### EP.07.WIN.LOLBIN.001 — PowerShell ofensivo: obfuscación, AMSI bypass, reflective loading

| Campo | Detalle |
|---|---|
| **Descripción** | PowerShell es usado de forma ofensiva más allá de la descarga y ejecución remota: técnicas de obfuscación para evadir detección basada en firmas (`-EncodedCommand`, string concatenation, `[char]` arrays), bypass de AMSI para ejecutar código malicioso sin que el AV lo inspeccione, y reflective loading de módulos en memoria sin tocar disco. Estas técnicas son características de operadores avanzados que intentan evadir controles de seguridad. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | PowerShell ScriptBlock Event ID 4104 — `ScriptBlockText` conteniendo patrones de bypass AMSI (`AmsiScanBuffer`, `amsiInitFailed`, `[Ref].Assembly.GetType`), obfuscación (`[char][int]`, `join`, `replace` encadenados), o loading de módulos desde bytes (`[System.Reflection.Assembly]::Load`). Sysmon Event ID 1 — `powershell.exe` con argumento `-EncodedCommand` de longitud > 200 caracteres. |
| **Lógica de detección** | Regla ScriptBlock: Event ID 4104 con `ScriptBlockText` conteniendo `AmsiScanBuffer`, `amsiInitFailed`, `[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils')` → nivel 12. Regla: `[System.Reflection.Assembly]::Load([Convert]::FromBase64String` → nivel 12. Regla Sysmon: `powershell.exe` con `-EncodedCommand` de payload > 500 caracteres en base64 → nivel 10. Regla: `ScriptBlockText` con 5+ operaciones de string manipulation en una línea → nivel 8. Correlación: AMSI bypass + reflective loading en mismo proceso en 60s → nivel 12. |
| **MITRE ATT&CK** | T1059.001 — PowerShell / T1027 — Obfuscated Files or Information / T1562.001 — Disable or Modify Tools (AMSI bypass) |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — ScriptBlock logging debe estar activo (GPO). El volumen de Event ID 4104 puede ser alto — filtrar por patrones específicos de ofensiva. |
| **Falsos positivos** | Bajos para AMSI bypass y reflective loading. Medios para detección de obfuscación (algunos scripts legítimos usan string manipulation). |
| **Nota operativa** | ScriptBlock logging captura el código PowerShell desobfuscado — incluso con obfuscación compleja, el Event ID 4104 muestra el código real a ejecutar. Es la fuente forense más valiosa para investigar incidentes con PowerShell ofensivo. |
| **Estado** | Pendiente de validación. |

---

###### EP.07.WIN.LOLBIN.002 — Proxy de ejecución: Regsvr32, Rundll32, Mshta, Cscript/Wscript

| Campo | Detalle |
|---|---|
| **Descripción** | Binarios legítimos de Windows son usados como proxy para ejecutar código malicioso, evadiendo controles basados en lista blanca de aplicaciones: `regsvr32.exe` con SCT remoto (Squiblydoo), `rundll32.exe` ejecutando DLL maliciosa o función JavaScript, `mshta.exe` ejecutando HTA con código VBScript/JScript, `cscript.exe`/`wscript.exe` ejecutando scripts maliciosos desde rutas temporales. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `regsvr32.exe` con argumento `/s /n /u /i:http` (Squiblydoo). `rundll32.exe` con argumento no DLL de sistema o con función JavaScript (`javascript:`). `mshta.exe` con argumento URL o script inline. `cscript.exe` o `wscript.exe` con script en `%TEMP%` o `%APPDATA%`. Sysmon Event ID 3 — conexión saliente desde `regsvr32.exe` o `mshta.exe`. |
| **Lógica de detección** | Regla Sysmon: `regsvr32.exe` con argumento `/i:http` o `/i:ftp` → nivel 12. `mshta.exe` con URL como argumento → nivel 12. `rundll32.exe` con argumento `javascript:` → nivel 12. Regla: `cscript.exe` o `wscript.exe` ejecutando script en ruta temporal → nivel 10. Regla Event ID 3: conexión saliente desde `regsvr32.exe`, `mshta.exe`, `cscript.exe`, `wscript.exe` → nivel 10. Correlación: proxy de ejecución + proceso hijo (cmd, powershell) en 30s → nivel 12. |
| **MITRE ATT&CK** | T1218.010 — Regsvr32 / T1218.011 — Rundll32 / T1218.005 — Mshta / T1059.005 — VBScript / T1059.007 — JavaScript |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — patrones de uso ofensivo muy específicos. Regsvr32 con URL y Mshta con URL son prácticamente siempre maliciosos. |
| **Falsos positivos** | Muy bajos para Regsvr32 y Mshta con URL. Medios para Rundll32 (muchos usos legítimos). La conexión de red desde estos binarios es el discriminador de mayor confianza. |
| **Estado** | Pendiente de validación. |

---

###### EP.07.WIN.LOLBIN.003 — Netsh como proxy de red o persistencia

| Campo | Detalle |
|---|---|
| **Descripción** | `netsh.exe` es usado de forma ofensiva: port forwarding para crear túneles de red (`netsh interface portproxy add`), desactivación del firewall de Windows (`netsh advfirewall set allprofiles state off`), o registro de DLL helper maliciosa para persistencia (`netsh add helper`). El port forwarding permite al atacante redirigir tráfico a través del endpoint comprometido hacia otros segmentos de red. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `netsh.exe` con argumentos `interface portproxy add v4tov4`, `advfirewall set allprofiles state off`, `add helper`. Security log — Event ID 4950 (Windows Firewall setting changed) desde proceso no de administración. Sysmon Event ID 13 — modificación de `HKLM\SYSTEM\CurrentControlSet\Services\PortProxy\`. |
| **Lógica de detección** | Regla Sysmon: `netsh.exe` con `interface portproxy add` → nivel 12. `netsh advfirewall set allprofiles state off` → nivel 12. `netsh add helper` con DLL en ruta no de sistema → nivel 12. Regla Security log: Event ID 4950 desde proceso no de administración → nivel 8. Regla Event ID 13: escritura en `\Services\PortProxy\` → nivel 10. |
| **MITRE ATT&CK** | T1090.001 — Proxy: Internal Proxy / T1562.004 — Disable or Modify System Firewall / T1546.007 — Netsh Helper DLL |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — argumentos ofensivos de netsh muy específicos. `portproxy add` y `advfirewall set state off` raramente tienen uso legítimo desde procesos interactivos en endpoints de usuario. |
| **Falsos positivos** | Bajos. Whitelist de cuentas de administración autorizadas para gestión de firewall. |
| **Nota operativa** | El port forwarding mediante `netsh portproxy` persiste en el registro y sobrevive reinicios. Si se detecta, revisar `HKLM\SYSTEM\CurrentControlSet\Services\PortProxy\v4tov4\tcp` para identificar todos los forwards activos y eliminarlos. |
| **Estado** | Pendiente de validación. |

---

###### EP.07.WIN.LOLBIN.004 — Cmd.exe encadenado con scripts complejos

| Campo | Detalle |
|---|---|
| **Descripción** | `cmd.exe` es usado para ejecutar cadenas de comandos complejas con objetivos ofensivos: descarga y ejecución en una línea, pivoting de variables de entorno para evadir detección (`set c=cmd & !c!`), uso de `for` loops para iterar sobre sistemas de la red, o pipes complejos que procesan la salida de comandos de reconocimiento. Los one-liners de cmd son más difíciles de detectar que PowerShell porque no tienen ScriptBlock logging equivalente. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `cmd.exe` con `CommandLine` de longitud > 200 caracteres conteniendo múltiples operadores de encadenamiento (`&&`, `||`, `|`, `^`, `%`). `CommandLine` con patrones de obfuscación de cmd (`set` + `!variable!`, `%variable:~N,M%`). Sysmon Event ID 1 — `cmd.exe /c` lanzado desde proceso no interactivo con payload complejo. |
| **Lógica de detección** | Regla Sysmon: `cmd.exe` con `CommandLine` > 300 caracteres → nivel 6. Alta confianza: `cmd.exe` con patrón de obfuscación `set` + delayed expansion + ejecución → nivel 10. Regla: `cmd.exe /c` con múltiples `&&` encadenando herramientas ofensivas (certutil, bitsadmin, powershell, net) → nivel 10. Regla: `cmd.exe` ejecutado desde proceso de servicio o tarea programada con payload > 100 caracteres → nivel 10. Correlación: cmd con one-liner complejo + proceso hijo sospechoso en 30s → nivel 12. |
| **MITRE ATT&CK** | T1059.003 — Windows Command Shell / T1027 — Obfuscated Files or Information |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — `cmd.exe` con líneas largas tiene muchos usos legítimos en scripts de instalación. El contexto del proceso padre y la presencia de herramientas ofensivas son los discriminadores. |
| **Falsos positivos** | Medios. Scripts de instalación legítimos usan cmd con comandos largos. La combinación longitud + herramientas ofensivas + proceso padre no interactivo es la señal más precisa. |
| **Estado** | Pendiente de validación. |

---

###### EP.07.WIN.LOLBIN.005 — Certutil y Bitsadmin para decode/encode y evasión

| Campo | Detalle |
|---|---|
| **Descripción** | `certutil.exe` y `bitsadmin.exe` son usados más allá de la descarga (cubierta en EP.02.WIN.POST.004) para codificar/decodificar payloads en base64 como técnica de evasión, o para crear BITS jobs persistentes con ejecución de comando al completar. `certutil -decode` es frecuentemente el segundo paso tras `certutil -urlcache` — el payload se descarga codificado y se decodifica localmente para evadir detección en tránsito. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 4.1 Explotación de vulnerabilidades conocidas |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `certutil.exe` con argumento `-decode` o `-decodehex` sobre fichero en `%TEMP%` o `%APPDATA%`. `certutil.exe` con `-encode` sobre fichero ejecutable o script. `bitsadmin.exe` con `/create` + `/addfile` + `/resume`. `bitsadmin.exe` con `/SetNotifyCmdLine`. Sysmon Event ID 11 — fichero `.exe` o `.dll` creado en `%TEMP%` tras `certutil -decode`. |
| **Lógica de detección** | Regla Sysmon: `certutil.exe` con `-decode` + fichero de salida en `%TEMP%` → nivel 10. Crítica: `certutil -decode` + creación de fichero ejecutable en ruta temporal en 30s → nivel 12. Regla: `bitsadmin.exe` con `/SetNotifyCmdLine` apuntando a proceso sospechoso → nivel 12. Regla: `certutil.exe` con `-encode` sobre fichero `.pst`, `.docx`, `.xlsx` → nivel 10 (posible exfiltración codificada). |
| **MITRE ATT&CK** | T1140 — Deobfuscate/Decode Files or Information / T1197 — BITS Jobs / T1027 — Obfuscated Files or Information |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — argumentos ofensivos de certutil (`-decode`) específicos. BITS jobs con NotifyCmdLine son prácticamente siempre maliciosos. |
| **Falsos positivos** | Bajos. `certutil -decode` en entornos corporativos no tiene uso legítimo frecuente fuera de gestión de certificados. |
| **Relación con otros CU** | EP.02.WIN.POST.004 cubre certutil para descarga (`-urlcache`). Esta ficha cubre certutil para decode/encode — el segundo paso del patrón descarga + decode. |
| **Estado** | Pendiente de validación. |

---

###### EP.07.WIN.LOLBIN.006 — Correlación: patrón LOLBin multi-herramienta

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa múltiples LOLBins en secuencia o combinación en el mismo endpoint en ventana temporal corta — patrón de operación ofensiva sistemática usando herramientas del sistema para evadir controles. La combinación de varias herramientas del bloque EP-07 eleva la confianza significativamente respecto a alertas individuales. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.07.WIN.LOLBIN.001-005 en el mismo `hostname` en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: 2+ alertas de distintas fichas LOLBIN.00* en el mismo hostname en 300s → nivel 12. Máxima prioridad: LOLBIN.001 (PowerShell ofensivo) + LOLBIN.002 (proxy de ejecución) en mismo hostname en 120s → nivel 12. Correlación extendida: cualquier LOLBIN.00* + EP.02.WIN.POST.004 (descarga) + NET.02.PALO.C2.* en mismo hostname en 3600s → nivel 12. |
| **MITRE ATT&CK** | T1218 — System Binary Proxy Execution / T1059 — Command and Scripting Interpreter / T1027 — Obfuscated Files or Information |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que fichas LOLBIN.001-005 estén operativas. |
| **Falsos positivos** | Muy bajos. Combinación de múltiples LOLBins en ventana corta es prácticamente siempre operación ofensiva. |
| **Nota operativa** | SentinelOne debería complementar la cobertura de Wazuh detectando el comportamiento de los procesos hijos generados, no solo los LOLBins en sí. Si SentinelOne no detecta y Wazuh sí, investigar si el EDR está siendo evadido activamente. |
| **Prerequisito** | Fichas EP.07.WIN.LOLBIN.001-005 operativas. |
| **Estado** | Pendiente de validación. |

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

##### Fichas detalladas — EP-08 (Comportamiento anómalo del usuario)

---

###### EP.08.WIN.UBA.001 — Actividad fuera del horario habitual del usuario

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario realiza actividad significativa en el endpoint fuera de su horario laboral habitual: inicio de sesión, ejecución de procesos, acceso a ficheros o conexiones de red en horas en las que normalmente no trabaja. No se trata de una actividad específicamente maliciosa sino de una desviación del patrón normal que puede indicar uso de credenciales robadas, insider threat, o acceso no autorizado. El contexto del cliente (turnos, trabajo en remoto, zonas horarias) es esencial para calibrar esta ficha. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Security log — Event ID 4624 (login exitoso) con timestamp fuera del horario habitual del usuario. Sysmon Event ID 1 — ejecución de procesos interactivos fuera de horario laboral. Event ID 4663 (Object Access) con acceso a ficheros sensibles fuera de horario. Sysmon Event ID 3 — conexiones de red salientes fuera de horario. |
| **Lógica de detección** | Regla custom: Event ID 4624 LogonType 2 o 10 entre 22:00-06:00 para cuenta de usuario estándar → nivel 6. Alta confianza: Event ID 4624 en fin de semana o festivo desde cuenta no de turno → nivel 8. Regla: ejecución de proceso interactivo (cmd, powershell, navegador) entre 22:00-06:00 desde cuenta no técnica → nivel 6. Correlación: login fuera de horario + acceso a carpetas sensibles + conexión saliente en 600s → nivel 10. Regla adicional: cuenta con 0 logins en los últimos 30 días que inicia sesión → nivel 8 (cuenta inactiva usada). |
| **MITRE ATT&CK** | T1078 — Valid Accounts / T1078.003 — Local Accounts |
| **Severidad** | Media |
| **Esfuerzo** | Alto — requiere definir el horario habitual de cada usuario o rol (CDB list por usuario o grupo AD). En entornos con trabajo en remoto o turnos variables la calibración es compleja. |
| **Falsos positivos** | Altos sin calibración. Con whitelist de horarios por rol: medios. Trabajo urgente, viajes, cambios de turno generan FP — coordinación con RRHH necesaria. |
| **Estado** | Pendiente de validación. |

---

###### EP.08.WIN.UBA.002 — Inicio de sesión desde equipo o ubicación no habitual

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario inicia sesión desde un endpoint distinto al que usa habitualmente o desde una ubicación geográfica diferente. Patrón de uso de credenciales robadas, de movimiento lateral, o de impossible travel (el usuario no puede estar físicamente en dos lugares al mismo tiempo). |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4624 con `WorkstationName` o `IpAddress` distinto al endpoint habitual del usuario. Event ID 4648 desde máquina no habitual. En el DC: Event ID 4624 del mismo usuario desde dos IPs geográficamente distantes en ventana corta. Complementariamente: GlobalProtect GP.002 (VPN desde ubicación anómala). |
| **Lógica de detección** | Regla custom: Event ID 4624 desde `WorkstationName` no en CDB list de equipos habituales del usuario → nivel 8. Correlación: mismo usuario con Event ID 4624 desde 2+ `WorkstationName` distintos en 300s → nivel 10. Regla: login desde equipo de diferente departamento (según OU en AD) → nivel 8. Impossible travel: mismo usuario con Event ID 4624 desde IPs de países distintos en menos de 4 horas → nivel 12. |
| **MITRE ATT&CK** | T1078 — Valid Accounts / T1078.002 — Domain Accounts |
| **Severidad** | Alta |
| **Esfuerzo** | Alto — requiere CDB list de equipos habituales por usuario (mínimo 30 días de baseline). Geolocalización de IPs para impossible travel. |
| **Falsos positivos** | Medios. Cambio de puesto, visita a otra oficina, portátil vs desktop, trabajo desde casa. Proceso de excepción necesario. |
| **Relación con otros CU** | Complementa NET.01.PALO.GP.002 (VPN desde ubicación anómala) con visibilidad de logins locales en red interna. |
| **Estado** | Pendiente de validación. |

---

###### EP.08.WIN.UBA.003 — Ejecución de procesos inusuales para ese usuario o equipo

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario ejecuta procesos que nunca o raramente ha ejecutado — herramientas de línea de comandos en un usuario que normalmente solo usa aplicaciones de negocio, herramientas de desarrollo en un equipo de contabilidad, o herramientas de administración de red en un PC de usuario estándar. La anomalía no está en el proceso en sí sino en su aparición en un contexto donde históricamente no se había visto. Señal débil individual pero valiosa en correlación. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 3.1 Escaneo de redes (scanning) |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Sysmon Event ID 1 — proceso ejecutado por primera vez en ese endpoint en los últimos 30 días. Security log — Event ID 4688 con proceso no habitual para el perfil del equipo. |
| **Lógica de detección** | Regla custom: proceso ejecutado por primera vez en el endpoint en 30 días + pertenece a categoría de riesgo (herramientas de red, intérpretes, compresores) → nivel 6. Alta confianza: primera ejecución de herramienta de administración (netstat, ipconfig, whoami, net) por cuenta de usuario no técnico → nivel 8. Correlación: primera ejecución + Event ID 3 (conexión saliente desde esa herramienta) en 60s → nivel 10. Regla: proceso en ruta temporal ejecutado por primera vez → nivel 8. |
| **MITRE ATT&CK** | T1078 — Valid Accounts / T1059 — Command and Scripting Interpreter |
| **Severidad** | Media |
| **Esfuerzo** | Alto — requiere mantener historial de procesos por endpoint (CDB lists actualizadas periódicamente o análisis de historial de alertas). |
| **Falsos positivos** | Altos sin baseline. Con baseline de 30+ días: medios. Instalaciones de software y cambios de rol generan FP. |
| **Nota operativa** | Mayor valor como señal de correlación que como alerta standalone. Proceso nuevo + actividad fuera de horario + acceso a carpetas sensibles es combinación de alta confianza aunque cada señal individual sea débil. |
| **Estado** | Pendiente de validación. |

---

###### EP.08.WIN.UBA.004 — Uso intensivo de CPU/disco por proceso desconocido (criptominería, ransomware)

| Campo | Detalle |
|---|---|
| **Descripción** | Un proceso desconocido o raramente ejecutado consume recursos intensivos de CPU o disco de forma sostenida — patrón compatible con criptominería (CPU/GPU intensivo), ransomware en fase de cifrado (CPU alta + I/O masivo de lectura/escritura), o exfiltración comprimida (CPU alta + I/O de lectura). La detección de consumo anómalo complementa la detección basada en firmas con una señal de impacto operacional. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 6.6 Agotamiento de recursos |
| **Peligrosidad** | MUY ALTO |
| **Telemetría** | Wazuh módulo `wodle command` — consumo de CPU > umbral por proceso específico durante > 5 minutos. Sysmon Event ID 1 — proceso con nombre aleatorio o en ruta temporal. Sysmon Event ID 11 — creación masiva de ficheros con extensiones inusuales (`.locked`, `.encrypted`, extensión aleatoria de 5-8 caracteres). FIM — modificación masiva de ficheros de documentos en ventana corta. |
| **Lógica de detección** | Regla Wazuh system monitor: proceso en `%TEMP%` con CPU > 80% durante > 300s → nivel 10 (posible criptominería). Regla FIM: modificación de 100+ ficheros con extensiones `.docx`, `.xlsx`, `.pdf` en 300s por el mismo proceso → nivel 12 (patrón de cifrado masivo — ransomware). Regla Sysmon: creación de ficheros con extensión no estándar en carpetas de documentos → nivel 12. Correlación: CPU alta + proceso en ruta temporal + conexión saliente en 600s → nivel 12 (criptominería con C2). |
| **MITRE ATT&CK** | T1496 — Resource Hijacking / T1486 — Data Encrypted for Impact |
| **Severidad** | Crítica |
| **Esfuerzo** | Medio — detección de ransomware por FIM directa. Detección de criptominería por CPU requiere módulo de monitorización de procesos de Wazuh. |
| **Falsos positivos** | Medios para CPU alta (compilación, rendering, antivirus scan). Muy bajos para modificación masiva de extensiones de documentos. |
| **Nota operativa** | Si se detecta patrón de ransomware (FIM con modificación masiva), aislar el endpoint inmediatamente — cada segundo permite cifrar más ficheros. No remediar en caliente; preservar para análisis forense y trabajar sobre backups. |
| **Estado** | Pendiente de validación. |

---

###### EP.08.WIN.UBA.005 — Actividad administrativa desde usuario no técnico

| Campo | Detalle |
|---|---|
| **Descripción** | Un usuario sin perfil técnico (contabilidad, RRHH, ventas, dirección) ejecuta herramientas o acciones de administración de sistemas fuera de su rol habitual: uso de PowerShell, acceso a `Computer Management`, modificación del registro, uso de `net user` o `net group`, instalación de software. Puede indicar compromiso de credenciales, escalada lograda, o insider threat con conocimientos técnicos. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.1 Acceso no autorizado a información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — herramienta administrativa (`powershell.exe`, `cmd.exe`, `regedit.exe`, `mmc.exe`, `net.exe`, `wmic.exe`) ejecutada desde cuenta de usuario en OU no técnica. Security log — Event ID 4688 con herramienta administrativa desde cuenta no técnica. Event ID 4732 (añadido a grupo privilegiado) por cuenta no técnica. |
| **Lógica de detección** | Regla custom: `powershell.exe` o `cmd.exe` desde cuenta en OU de RRHH, Contabilidad, Ventas, Dirección (CDB list de OUs no técnicas) → nivel 8. Alta confianza: `regedit.exe`, `mmc.exe`, `compmgmt.msc` desde cuenta no técnica → nivel 8. Regla: Event ID 4732 por cuenta no técnica → nivel 10. Regla: `net user /add` o `net localgroup administrators /add` desde cuenta no técnica → nivel 12. Correlación: 3+ herramientas administrativas desde misma cuenta no técnica en 300s → nivel 10. |
| **MITRE ATT&CK** | T1078 — Valid Accounts / T1059.001 — PowerShell / T1087 — Account Discovery |
| **Severidad** | Media / Alta (según herramienta y acción) |
| **Esfuerzo** | Alto — requiere clasificación de usuarios por perfil técnico/no técnico en AD (atributo `Department` o membresía en OU). Sin esta clasificación los FP son muy altos. |
| **Falsos positivos** | Altos sin clasificación. Con clasificación por OU: medios. Usuarios power-users en departamentos no técnicos generan FP. |
| **Nota operativa** | Mayor efectividad combinada con UBA.001 (horario) — usuario de contabilidad ejecutando PowerShell a las 2AM es prácticamente siempre un incidente, mientras que a las 10AM podría tener justificación legítima. |
| **Estado** | Pendiente de validación. |

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

##### Fichas detalladas — EP-09 (Violación de políticas de seguridad)

---

###### EP.09.WIN.POL.001 — EDR SentinelOne parado, manipulado o desinstalado

| Campo | Detalle |
|---|---|
| **Descripción** | El agente de SentinelOne en el endpoint ha sido detenido, manipulado o desinstalado. Esta es una de las acciones más críticas que puede realizar un atacante — sin EDR el endpoint queda prácticamente ciego para detecciones basadas en comportamiento. Dado que SentinelOne es el mecanismo de rollback ante ransomware, su eliminación es un precursor directo de ataque de ransomware. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 7036 con `ServiceName` = `SentinelAgent` o `SentinelHelperService` en estado `stopped`. Event ID 7045 con nombre de servicio de SentinelOne (desinstalación). Wazuh — pérdida de heartbeat del agente en el endpoint. Sysmon Event ID 1 — `MsiExec.exe` con argumento de desinstalación del GUID de SentinelOne. FIM — modificación o eliminación de ficheros en `C:\Program Files\SentinelOne\`. |
| **Lógica de detección** | Regla Security log crítica: Event ID 7036 con `ServiceName` conteniendo `Sentinel` y estado `stopped` → nivel 12. Regla: Event ID 7040 con cambio de tipo de inicio de servicio SentinelOne a `disabled` → nivel 12. Wazuh: agente sin heartbeat durante > 5 minutos → nivel 10. FIM: modificación de ficheros en directorio de SentinelOne por proceso distinto al agente oficial → nivel 12. Correlación: parada de SentinelOne + EP.03.WIN.DRV.002 (BYOVD) en 300s → nivel 12 (kill EDR mediante BYOVD confirmado). |
| **MITRE ATT&CK** | T1562.001 — Impair Defenses: Disable or Modify Tools |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — parada del servicio SentinelOne es evento muy específico de alta confianza. |
| **Falsos positivos** | Muy bajos. SentinelOne se detiene legítimamente solo durante actualizaciones del propio agente — whitelist de ventanas de mantenimiento y proceso de actualización oficial. |
| **Nota operativa** | Notificar al cliente de forma inmediata. Si coincide con pérdida de heartbeat de Wazuh, el endpoint puede estar completamente comprometido. La combinación POL.001 + POL.003 (VSS eliminado) indica preparación completa para ransomware sin capacidad de rollback. |
| **Estado** | Pendiente de validación. |

---

###### EP.09.WIN.POL.002 — Firewall local de Windows desactivado

| Campo | Detalle |
|---|---|
| **Descripción** | El firewall local de Windows ha sido desactivado — acción que elimina una capa de defensa en profundidad y facilita conexiones entrantes y salientes sin restricción. En endpoints correctamente gestionados el firewall local debería mantenerse activo incluso con firewall perimetral. La desactivación puede indicar preparación para movimiento lateral, instalación de backdoor o evasión de controles. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 4950 (Windows Firewall setting changed) con perfil desactivado. Event ID 7036 con `ServiceName = MpsSvc` en estado `stopped`. Sysmon Event ID 13 — modificación de `HKLM\SYSTEM\CurrentControlSet\Services\MpsSvc\Start` a valor `4` (disabled). |
| **Lógica de detección** | Regla Security log: Event ID 4950 con perfil Domain, Private o Public desactivado → nivel 10. Regla: Event ID 7036 con `ServiceName = MpsSvc` en estado `stopped` → nivel 10. Regla Sysmon: Event ID 13 con `MpsSvc\Start = 4` → nivel 10. Correlación: desactivación del firewall + Event ID 4624 LogonType 3 (conexión entrante) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1562.004 — Impair Defenses: Disable or Modify System Firewall |
| **Severidad** | Alta |
| **Esfuerzo** | Bajo — Event ID 4950 y estado del servicio MpsSvc son eventos específicos de baja ambigüedad. |
| **Falsos positivos** | Bajos. Whitelist de cuentas de administración autorizadas y ventanas de mantenimiento. |
| **Estado** | Pendiente de validación. |

---

###### EP.09.WIN.POL.003 — Shadow Copies eliminadas o servicio VSS manipulado

| Campo | Detalle |
|---|---|
| **Descripción** | Las Shadow Copies han sido eliminadas o el servicio VSS ha sido manipulado. Las Shadow Copies son el mecanismo de recuperación de versiones anteriores de ficheros en Windows y la base del rollback automático de SentinelOne ante ransomware. Su eliminación es uno de los primeros pasos de prácticamente todos los ataques de ransomware modernos. Esta ficha tiene máxima prioridad operativa: su disparo debe interpretarse como precursor inmediato de ransomware o como ransomware ya activo. |
| **Clasificación GrayHats** | 7.2 Modificación no autorizada de información / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `vssadmin.exe delete shadows /all /quiet`, `wmic shadowcopy delete`, `wbadmin delete catalog -quiet`, `bcdedit /set {default} recoveryenabled No`, `bcdedit /set {default} bootstatuspolicy ignoreallfailures`. PowerShell ScriptBlock Event ID 4104 — `Get-WmiObject Win32_ShadowCopy | Remove-WmiObject`. Security log — Event ID 7036 con `ServiceName = VSS` en estado `stopped` de forma no planificada. |
| **Lógica de detección** | Regla Sysmon crítica: `vssadmin.exe` con argumentos `delete shadows` → nivel 12. `wmic shadowcopy delete` → nivel 12. `bcdedit` con `/set recoveryenabled No` → nivel 12. Regla PowerShell: `Win32_ShadowCopy` con método `Delete` → nivel 12. Correlación máxima prioridad: eliminación de Shadow Copies + FIM con modificación masiva de ficheros en 600s → nivel 12 (VSS + cifrado activo — ransomware confirmado). POL.001 + POL.003 → nivel 12 (SentinelOne parado + VSS eliminado — preparación completa para ransomware sin rollback). |
| **MITRE ATT&CK** | T1490 — Inhibit System Recovery / T1562.001 — Impair Defenses |
| **Severidad** | Crítica |
| **Esfuerzo** | Muy bajo — comandos de eliminación de VSS extremadamente específicos y prácticamente nunca legítimos en endpoints de producción. Una de las detecciones de mayor relación señal/ruido del catálogo. |
| **Falsos positivos** | Prácticamente nulos. `vssadmin delete shadows /all` fuera de procesos de administración de almacenamiento documentados es siempre malicioso o un error grave de administración. |
| **Nota operativa** | **ACCIÓN INMEDIATA requerida. Tiempo de respuesta objetivo: menos de 5 minutos.** (1) Aislar el endpoint de la red inmediatamente. (2) Verificar si el cifrado ya ha comenzado (FIM). (3) Notificar al cliente de forma urgente. (4) No reiniciar — preservar estado de memoria para forense. (5) Si SentinelOne sigue activo, verificar disponibilidad de rollback antes de la eliminación de VSS. Sin SentinelOne activo y sin VSS, la única recuperación posible es desde backups externos — verificar su estado inmediatamente. |
| **Estado** | Pendiente de validación. |

---

###### EP.09.WIN.POL.004 — Software prohibido instalado o ejecutado

| Campo | Detalle |
|---|---|
| **Descripción** | Se instala o ejecuta software explícitamente prohibido por la política de seguridad del cliente: clientes P2P (uTorrent, eMule), software de acceso remoto no autorizado (AnyDesk personal, TeamViewer no corporativo, UltraVNC), herramientas de tunelización (ngrok, frp, Cloudflared), o cualquier software en la lista negra del cliente. |
| **Clasificación GrayHats** | 8.1 Uso no autorizado de recursos / 2.1 Sistema infectado |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Sysmon Event ID 1 — `Image` conteniendo nombre de software prohibido. Event ID 11 — instalación en `Program Files` o `AppData` con nombre de aplicación prohibida. Sysmon Event ID 3 — conexión saliente desde software de acceso remoto no autorizado a servidores de relay conocidos. |
| **Lógica de detección** | Regla Sysmon: `Image` conteniendo nombres de CDB list de software prohibido (`utorrent.exe`, `bittorrent.exe`, `anydesk.exe` en ruta no corporativa, `ngrok.exe`, `frpc.exe`, `cloudflared.exe`) → nivel 8. Alta confianza: `ngrok.exe` o `frpc.exe` ejecutados desde cualquier ruta → nivel 12. Regla Event ID 3: conexión desde AnyDesk o TeamViewer no corporativo a relay servers → nivel 8. |
| **MITRE ATT&CK** | T1219 — Remote Access Software / T1572 — Protocol Tunneling / T1090 — Proxy |
| **Severidad** | Media / Alta (ngrok y herramientas de túnel → Alta) |
| **Esfuerzo** | Medio — requiere CDB list de software prohibido por cliente. `ngrok` y herramientas de túnel son detección directa sin lista. |
| **Falsos positivos** | Medios para software de acceso remoto. Muy bajos para ngrok y herramientas de tunelización. |
| **Nota operativa** | `ngrok` y herramientas similares crean túneles desde el interior de la red hacia Internet, exponiendo servicios internos sin pasar por el firewall perimetral. Tratar con urgencia independientemente de si el uso es malicioso o por negligencia. |
| **Estado** | Pendiente de validación. |

---

###### EP.09.WIN.POL.005 — Macros de Office habilitadas o ejecutadas desde documento externo

| Campo | Detalle |
|---|---|
| **Descripción** | Se habilitan o ejecutan macros de Microsoft Office en un documento procedente de fuente externa. Las macros de Office son uno de los vectores de entrada más frecuentes en ataques de phishing — el documento malicioso solicita habilitar las macros para mostrar el contenido, y al hacerlo ejecuta el payload. |
| **Clasificación GrayHats** | 4.1 Explotación de vulnerabilidades conocidas / 2.1 Sistema infectado |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — modificación del registro para habilitar macros (`HKCU\Software\Microsoft\Office\*\Security\VBAWarnings = 1`). Sysmon Event ID 1 — proceso Office spawneando proceso hijo (cubierto en EP.02.WIN.EXPLOIT.001). FIM — creación de fichero ejecutable en `%TEMP%` por proceso Office. |
| **Lógica de detección** | Regla Sysmon: Event ID 13 con `TargetObject` conteniendo `\Office\*\Security\VBAWarnings` con `Details = 1` → nivel 8. Alta confianza: `VBAWarnings = 1` modificado por proceso no de administración + apertura de fichero Office externo (Zone.Identifier = 3) en 60s → nivel 10. FIM: creación de `.exe` en `%TEMP%` por `WINWORD.EXE` → nivel 12. |
| **MITRE ATT&CK** | T1566.001 — Phishing: Spearphishing Attachment / T1059.005 — VBScript / T1204.002 — User Execution: Malicious File |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — cambio de registro VBAWarnings es directo. Correlación con Mark of the Web (Zone.Identifier) requiere FIM sobre streams ADS. |
| **Falsos positivos** | Medios para cambio de VBAWarnings. Muy bajos para correlación cambio de registro + fichero externo + proceso hijo. |
| **Recomendación de hardening** | GPO `VBAWarnings = 4` (deshabilitar todas las macros) o `= 3` (solo macros firmadas). Activar reglas ASR de Microsoft Defender para bloquear Office de crear procesos hijo. |
| **Estado** | Pendiente de validación. |

---

###### EP.09.WIN.POL.006 — Software obsoleto o sin parches ejecutándose

| Campo | Detalle |
|---|---|
| **Descripción** | Se detecta la ejecución de software con versiones conocidas como vulnerables: navegadores sin actualizar, Java con versiones antiguas, Adobe Reader con CVEs activos, aplicaciones de negocio sin parches. La detección no es sobre un ataque activo sino sobre una postura de riesgo — el software obsoleto amplía la superficie de ataque del endpoint. |
| **Clasificación GrayHats** | 9.5 Sistema vulnerable |
| **Peligrosidad** | MEDIO |
| **Telemetría** | Wazuh módulo `vulnerability-detector` — escaneo periódico de software instalado contra base de datos de CVEs (NVD, OSV). Sysmon Event ID 1 — `Image` con `FileVersion` de versión vulnerable (CDB list de versiones vulnerables por aplicación). |
| **Lógica de detección** | Regla Wazuh vulnerability-detector: CVE de severidad CRITICAL o HIGH en software instalado activo → nivel 10. Regla: CVE con exploit público conocido (CISA KEV) en software activo → nivel 12. Regla Sysmon: navegadores o aplicaciones con `FileVersion` más antigua que umbral de días → nivel 6. Correlación: software vulnerable activo + intento de explotación (EXPLOIT.001) en mismo endpoint → nivel 12. |
| **MITRE ATT&CK** | T1203 — Exploitation for Client Execution / T1190 — Exploit Public-Facing Application |
| **Severidad** | Media (detección de riesgo) / Crítica (si correlaciona con explotación) |
| **Esfuerzo** | Medio — vulnerability-detector requiere configuración y acceso a feeds de CVE actualizados. |
| **Falsos positivos** | Medios. Software sin actualizar por ciclo de actualización lento o software legacy. Proceso de gestión de excepciones con justificación de negocio necesario. |
| **Nota operativa** | Esta ficha es más una herramienta de gestión de postura de seguridad que de detección de incidentes activos. Recomendado generar informe periódico (semanal) de software vulnerable por cliente para priorizar actualizaciones. |
| **Estado** | Pendiente de validación. |

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

##### Fichas detalladas — EP-10 (Evasión defensiva avanzada)

---

###### EP.10.WIN.DEF.001 — Parada de servicios de seguridad

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante detiene o deshabilita servicios de seguridad instalados en el endpoint más allá de SentinelOne: otros productos AV/EDR (Bitdefender GravityZone, CrowdStrike, Cylance), el agente Wazuh, servicios de monitorización, o servicios de backup. La parada sistemática de múltiples servicios de seguridad es señal de alta confianza de evasión activa de defensas. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Security log — Event ID 7036 con `ServiceName` de productos de seguridad conocidos en estado `stopped`: `WazuhSvc`, `bdagent` (Bitdefender), `CSFalconService` (CrowdStrike), `CylanceSvc`, `MsMpEng` (Defender), `WinDefend`. Event ID 7040 con tipo de inicio a `disabled`. Sysmon Event ID 1 — `sc.exe stop` o `net stop` con nombre de servicio de seguridad. PowerShell ScriptBlock Event ID 4104 — `Stop-Service` con nombre de servicio de seguridad. |
| **Lógica de detección** | Regla Security log: Event ID 7036 con `ServiceName` en CDB list de servicios de seguridad en estado `stopped` → nivel 10. Crítica: mismo patrón + proceso que lo detiene no es el instalador oficial → nivel 12. Regla Sysmon: `sc.exe stop` o `net stop` con servicio de seguridad desde proceso interactivo → nivel 12. Correlación: parada de 2+ servicios de seguridad distintos en 300s → nivel 12 (desmantelamiento sistemático de defensas). |
| **MITRE ATT&CK** | T1562.001 — Impair Defenses: Disable or Modify Tools |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — CDB list de servicios de seguridad conocidos es estática y bien definida. |
| **Falsos positivos** | Bajos. Servicios de seguridad se detienen legítimamente solo en actualizaciones o mantenimiento autorizado. |
| **Nota operativa** | La parada del agente Wazuh (`WazuhSvc`) elimina la visibilidad del SOC sobre el endpoint. Si se detecta parada de Wazuh + pérdida de heartbeat, tratar como endpoint comprometido e iniciar respuesta proactiva. |
| **Estado** | Pendiente de validación. |

---

###### EP.10.WIN.DEF.002 — Cambios en exclusiones de AV/Defender

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante añade exclusiones al antivirus o EDR para que su malware no sea escaneado: exclusiones de ruta, proceso o extensión en Microsoft Defender. La adición de exclusiones en rutas temporales o para procesos desconocidos es un indicador claro de evasión. |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 5.1 Compromiso de cuenta con privilegios |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 13 — escritura en `HKLM\SOFTWARE\Microsoft\Windows Defender\Exclusions\Paths\`, `\Exclusions\Processes\`, `\Exclusions\Extensions\`. Event ID 5007 del canal `Windows Defender/Operational` (configuración cambiada). PowerShell ScriptBlock Event ID 4104 — `Add-MpPreference -ExclusionPath`, `Add-MpPreference -ExclusionProcess`. |
| **Lógica de detección** | Regla Sysmon: Event ID 13 con `TargetObject` conteniendo `\Windows Defender\Exclusions\Paths\` con `Details` apuntando a ruta temporal o de usuario → nivel 12. Regla: exclusión de proceso añadida para proceso en ruta anómala → nivel 12. Regla PowerShell: `Add-MpPreference -ExclusionPath` o `-ExclusionProcess` desde proceso no de gestión → nivel 12. Correlación: exclusión añadida + creación de fichero en la ruta excluida en 60s → nivel 12. |
| **MITRE ATT&CK** | T1562.001 — Impair Defenses: Disable or Modify Tools |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — claves de registro de exclusiones de Defender muy específicas. |
| **Falsos positivos** | Medios. Administradores añaden exclusiones legítimas para aplicaciones con FP. Whitelist de cuentas autorizadas para gestión de exclusiones. |
| **Nota operativa** | Revisar periódicamente las exclusiones de Defender en todos los endpoints. Si se detecta exclusión hacia ruta temporal, revisar el contenido de esa ruta inmediatamente antes de eliminarlo. |
| **Estado** | Pendiente de validación. |

---

###### EP.10.WIN.DEF.003 — Borrado de logs de Windows (todos los canales)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante borra los logs de eventos de Windows para eliminar rastros de su actividad. Más allá del Security log (cubierto en AUDIT.001), esta ficha cubre el borrado de cualquier otro canal: System, Application, PowerShell, Sysmon, Task Scheduler, WMI. El borrado selectivo de canales específicos revela qué técnicas usó el atacante. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.2 Modificación no autorizada de información |
| **Peligrosidad** | ALTO |
| **Telemetría** | System log — Event ID 104 (System log cleared). Sysmon Event ID 1 — `wevtutil.exe cl` con nombre de canal. PowerShell ScriptBlock Event ID 4104 — `Clear-EventLog`, `Remove-EventLog`, `wevtutil cl`. Sysmon Event ID 1 — `wevtutil.exe el` seguido de `cl` en múltiples canales. |
| **Lógica de detección** | Regla Sysmon: `wevtutil.exe` con argumento `cl` → nivel 12. Regla: `wevtutil.exe el` + `cl` en múltiples canales en 120s → nivel 12 (borrado sistemático). Regla PowerShell: `Clear-EventLog` desde proceso no de mantenimiento → nivel 12. Regla System log: Event ID 104 → nivel 10. Correlación: borrado de canal PowerShell/Operational + canal Sysmon en 60s → nivel 12. |
| **MITRE ATT&CK** | T1070.001 — Indicator Removal: Clear Windows Event Logs |
| **Severidad** | Crítica |
| **Esfuerzo** | Bajo — `wevtutil cl` es comando específico de baja ambigüedad. Borrado de canales como PowerShell/Operational o Sysmon es prácticamente siempre malicioso. |
| **Falsos positivos** | Muy bajos. Whitelist de procesos y cuentas de mantenimiento autorizados. |
| **Nota operativa** | El borrado selectivo de canales revela las técnicas usadas: solo PowerShell/Operational borrado → el atacante usó PowerShell; solo Sysmon borrado → usó técnicas que Sysmon detecta. Documentar qué canales se borraron como evidencia forense. |
| **Estado** | Pendiente de validación. |

---

###### EP.10.WIN.DEF.004 — Herramientas anti-forense (SDelete, timestomping, Eraser)

| Campo | Detalle |
|---|---|
| **Descripción** | Un atacante usa herramientas diseñadas para dificultar el análisis forense: `SDelete` (sobrescritura segura de ficheros), `cipher /w` (sobrescritura del espacio libre), `Eraser`, `BleachBit`, modificación de timestamps de ficheros (timestomping), o limpieza del historial de PowerShell. El objetivo es dificultar la reconstrucción de la cadena de ataque. |
| **Clasificación GrayHats** | 5.1 Compromiso de cuenta con privilegios / 7.2 Modificación no autorizada de información |
| **Peligrosidad** | ALTO |
| **Telemetría** | Sysmon Event ID 1 — `sdelete.exe`, `sdelete64.exe`, `eraser.exe`, `bleachbit.exe` con argumentos de borrado seguro. `cipher.exe /w`. PowerShell ScriptBlock Event ID 4104 — `[System.IO.File]::SetCreationTime`, `SetLastWriteTime`, `SetLastAccessTime` (timestomping). Sysmon Event ID 2 (File creation time changed) — modificación de timestamp de fichero por proceso no de backup. |
| **Lógica de detección** | Regla Sysmon: `sdelete.exe` ejecutado desde endpoint de producción → nivel 10. `cipher.exe /w` desde proceso interactivo → nivel 8. `eraser.exe` o `bleachbit.exe` → nivel 8. Regla Event ID 2: modificación de timestamp de fichero `.exe`, `.dll`, `.ps1` por proceso distinto al creador → nivel 10 (timestomping). Regla PowerShell: `SetCreationTime` o `SetLastWriteTime` sobre fichero ejecutable → nivel 10. Correlación: SDelete + borrado de logs (DEF.003) en 300s → nivel 12. |
| **MITRE ATT&CK** | T1070.004 — Indicator Removal: File Deletion / T1070.006 — Indicator Removal: Timestomp / T1485 — Data Destruction |
| **Severidad** | Alta |
| **Esfuerzo** | Medio — SDelete y herramientas de borrado seguro directas. Timestomping vía Event ID 2 requiere Sysmon configurado para capturar cambios de timestamp. |
| **Falsos positivos** | Medios para herramientas de borrado seguro (uso legítimo en equipos con datos sensibles). Bajos para timestomping. |
| **Nota operativa** | El timestomping distorsiona la línea temporal del incidente. El Event ID 2 de Sysmon registra el timestamp anterior y el nuevo — usar estos datos para reconstruir la línea temporal real del ataque. |
| **Estado** | Pendiente de validación. |

---

###### EP.10.WIN.DEF.005 — Correlación: perfil completo de evasión defensiva

| Campo | Detalle |
|---|---|
| **Descripción** | Detección de la combinación de múltiples técnicas de evasión defensiva en el mismo endpoint en ventana temporal — patrón de atacante avanzado en fase de preparación para la acción principal (ransomware, exfiltración, persistencia de larga duración). |
| **Clasificación GrayHats** | 2.1 Sistema infectado / 10.1 APT |
| **Peligrosidad** | ALTO |
| **Telemetría** | Correlación de alertas generadas por EP.10.WIN.DEF.001-004, EP.10.WIN.AUDIT.001-002, EP.10.WIN.AV.001, EP.09.WIN.POL.001-003 en el mismo `hostname` en ventana temporal. |
| **Lógica de detección** | Regla custom de segundo nivel: 2+ alertas de distintas fichas DEF.00*, AUDIT.00* o POL.00* en mismo hostname en 600s → nivel 12. Máxima prioridad: POL.001 (SentinelOne parado) + POL.003 (VSS eliminado) + DEF.003 (logs borrados) en 900s → nivel 12 (preparación completa para ransomware). Correlación extendida: cualquier DEF.00* + EP.06.WIN.EXFIL.00* en mismo hostname en 3600s → nivel 12 (evasión + exfiltración activa). |
| **MITRE ATT&CK** | T1562 — Impair Defenses / T1070 — Indicator Removal / T1490 — Inhibit System Recovery |
| **Severidad** | Crítica |
| **Esfuerzo** | Alto — detección de tercer nivel dependiente de que fichas DEF.001-004 y EP-09/EP-10 relacionadas estén operativas. |
| **Falsos positivos** | Prácticamente nulos. Combinación de múltiples técnicas de evasión en ventana corta es siempre ataque avanzado en curso. |
| **Nota operativa** | Combinación POL.001 + POL.003 + DEF.003 indica ransomware a minutos — tiempo de respuesta objetivo inferior a 5 minutos: (1) aislar endpoint de la red, (2) verificar estado de backups del cliente, (3) notificar al cliente de forma urgente, (4) preservar evidencias forenses. |
| **Prerequisito** | Fichas EP.10.WIN.DEF.001-004, EP.09.WIN.POL.001-003 y EP.10.WIN.AUDIT.001-002 operativas. |
| **Estado** | Pendiente de validación. |

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

