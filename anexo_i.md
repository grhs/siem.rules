# Catálogo SOC GrayHats — Anexo I: Tablas de clasificación

---

## Anexo I — Tablas para clasificación de incidentes

---

### Tabla I: Taxonomía de amenazas

*Cuando una amenaza se materializa sobre un activo se produce un incidente cuyo tipo suele asociarse con el tipo de amenaza que lo ha producido.*

| Fuente de Amenaza | Evento de Amenaza | Descripción y ejemplos prácticos |
|---|---|---|
| **1. Contenido abusivo** | 1.1. Spam | Correo electrónico masivo no solicitado. El receptor del contenido no ha otorgado autorización válida para recibir un mensaje colectivo. |
| | 1.2. Delito de odio | Contenido difamatorio o discriminatorio. Ej: ciberacoso, racismo, amenazas a una persona o dirigidas contra colectivos. |
| | 1.3. Pornografía infantil, contenido sexual o violento inadecuado | Material que represente de manera visual contenido relacionado con pornografía infantil, apología de la violencia, etc. |
| **2. Contenido dañino** | 2.1. Sistema infectado | Sistema infectado con malware. Ej: sistema, computadora o teléfono móvil infectado con malware. |
| | 2.2. Servidor C&C (Mando y Control) | Conexión con servidor de Mando y Control (C&C) mediante malware o sistemas infectados. |
| | 2.3. Distribución de malware | Recurso usado para distribución de malware. Ej: recurso de una organización empleado para distribuir malware. |
| | 2.4. Configuración de malware | Recurso que aloje ficheros de configuración de malware. Ej: ataque de webinjects para troyano. |
| **3. Obtención de información** | 3.1. Escaneo de redes (scanning) | Envío de peticiones a un sistema para descubrir posibles debilidades. Ej: peticiones DNS, ICMP, SMTP, escaneo de puertos. |
| | 3.2. Análisis de paquetes (sniffing) | Observación y grabación del tráfico de redes. |
| | 3.3. Ingeniería social | Recopilación de información personal sin el uso de la tecnología. Ej: mentiras, trucos, sobornos, amenazas. |
| **4. Intento de intrusión** | 4.1. Explotación de vulnerabilidades conocidas | Intento de compromiso mediante la explotación de vulnerabilidades con identificador estandarizado (CVE). Ej: desbordamiento de buffer, XSS. |
| | 4.2. Intento de acceso con vulneración de credenciales | Múltiples intentos de vulnerar credenciales. Ej: intentos de ruptura de contraseñas, ataque por fuerza bruta. |
| | 4.3. Ataque desconocido | Ataque empleando exploit desconocido. |
| **5. Intrusión** | 5.1. Compromiso de cuenta con privilegios | Compromiso de un sistema en el que el atacante ha adquirido privilegios. Ej: secuestro de cuentas, robo de sesiones de administrador, EAC. |
| | 5.2. Intento de acceso con vulneración de credenciales | Múltiples intentos de vulnerar credenciales. Ej: intentos de ruptura de contraseñas, ataque por fuerza bruta. |
| | 5.3. Compromiso de aplicaciones | Compromiso de una aplicación mediante la explotación de vulnerabilidades de software. Ej: inyección SQL. |
| | 5.4. Robo | Intrusión física. Ej: acceso no autorizado a Centro de Proceso de Datos. |
| **6. Fallo de Disponibilidad** | 6.1. DoS (Denegación de servicio) | Ataque de denegación de servicio. Ej: peticiones a una aplicación web que provocan interrupción o ralentización del servicio. |
| | 6.2. DDoS (Denegación distribuida de servicio) | Ataque de denegación distribuida de servicio. Ej: inundación de paquetes SYN, ataques de reflexión y amplificación. |
| | 6.3. Mala configuración | Configuración incorrecta de infraestructura o software que provoca problemas de disponibilidad. |
| | 6.4. Sabotaje | Sabotaje físico o lógico. Ej: cortes de cableados o incendios provocados. |
| | 6.5. Interrupciones | Interrupciones por causas ajenas. Ej: fallo estructural, desastre natural, falta de pago de un servicio. |
| | 6.6. Agotamiento de recursos | Problemas de disponibilidad por agotamiento de algún recurso de la infraestructura. Ej: espacio en disco, IOPS, créditos de CPU. |
| | 6.7. Denegación Económica de Sostenibilidad (EDoS) | Ataques dirigidos a aumentar los costos de uso. Ej: minado de criptomonedas, cómputo distribuido. |
| **7. Compromiso de la información** | 7.1. Acceso no autorizado a información | Acceso no autorizado a información. Ej: robo de credenciales mediante interceptación de tráfico. |
| | 7.2. Modificación no autorizada de información | Modificación no autorizada de información. Ej: modificación con credenciales sustraídas o cifrado mediante ransomware. |
| | 7.4. Pérdida de datos | Pérdida de información. Ej: pérdida por fallo de disco duro o robo físico. |
| **8. Fraude** | 8.1. Uso no autorizado de recursos | Uso de recursos para propósitos inadecuados, incluyendo acciones con ánimo de lucro. |
| | 8.2. Derechos de autor | Ofrecimiento o instalación de software carente de licencia u otro material protegido por derechos de autor. |
| | 8.3. Suplantación | Tipo de ataque en el que una persona o entidad suplanta a otra para obtener beneficios ilegítimos. |
| | 8.4. Phishing | Suplantación de una entidad o persona para convencer al usuario para que revele sus credenciales privadas. |
| **9. Sistema Vulnerable** | 9.1. Criptografía débil | Servicios accesibles públicamente que puedan presentar criptografía débil. Ej: servidores web susceptibles de ataques POODLE/FREAK. |
| | 9.2. Amplificador DDoS | Servicios accesibles públicamente que puedan ser empleados para reflexión o amplificación de ataques DDoS. |
| | 9.3. Servicios con acceso potencial no deseado | Ej: Telnet, RDP o VNC. |
| | 9.4. Revelación de información | Acceso público a servicios en los que potencialmente pueda revelarse información sensible. Ej: SNMP o Redis. |
| | 9.5. Sistema vulnerable | Sistema vulnerable. Ej: mala configuración, versiones desfasadas de sistema. |
| **10. Otros** | 10.1. APT | Ataques dirigidos contra organizaciones concretas, sustentados en mecanismos sofisticados de ocultación, anonimato y persistencia. |
| | 10.2. Otros | Todo aquel incidente que no tenga cabida en ninguna categoría anterior. |

---

### Tabla II: Criterios de determinación del nivel de peligrosidad

| Nivel | Clasificación | Tipo de incidente |
|---|---|---|
| **CRÍTICO** | Otros | APT |
| **MUY ALTO** | Código dañino | Distribución de malware |
| | | Configuración de malware |
| | Intrusión | Robo de sesiones o cuentas |
| | Disponibilidad | Sabotaje |
| | | Interrupciones que afectan a servicios de negocio de manera generalizada |
| **ALTO** | Contenido abusivo | Pornografía infantil, contenido sexual o violento inadecuado |
| | Código dañino | Sistema infectado |
| | | Servidor C&C (Mando y Control) |
| | Intrusión | Compromiso de aplicaciones |
| | | Compromiso de cuentas con privilegios |
| | Intento de intrusión | Ataque desconocido |
| | Disponibilidad | DoS (Denegación de servicio) |
| | | DDoS (Denegación distribuida de servicio) |
| | Compromiso de la información | Acceso no autorizado a información |
| | | Modificación no autorizada de información |
| | | Pérdida de datos |
| | Fraude | Phishing |
| **MEDIO** | Contenido abusivo | Discurso de odio |
| | Obtención de información | Ingeniería social |
| | Intento de intrusión | Explotación de vulnerabilidades conocidas |
| | | Intento de acceso con vulneración de credenciales |
| | Intrusión | Compromiso de cuentas sin privilegios |
| | Disponibilidad | Mala configuración |
| | Fraude | Uso no autorizado de recursos |
| | | Derechos de autor |
| | | Suplantación |
| | Vulnerabilidad | Criptografía débil |
| | | Amplificador DDoS |
| | | Servicios con acceso potencial no deseado |
| | | Revelación de información |
| | | Sistema vulnerable |
| **BAJO** | Contenido abusivo | Spam |
| | Obtención de información | Escaneo de redes (scanning) |
| | | Análisis de paquetes (sniffing) |
| | Otros | Otros |
