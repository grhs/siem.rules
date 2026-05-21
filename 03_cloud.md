# Catálogo SOC GrayHats — Sección 3: Cloud IaaS

---

## 3. Cloud IaaS

Monitorización del plano de identidad, plano de control, red cloud, almacenamiento y workloads para detectar abuso, exposición, exfiltración y compromiso en entornos AWS y Azure.

---

### CLD-01 — Compromiso de identidad cloud

> ¿Alguien está usando una identidad cloud de forma sospechosa?

- Uso anómalo de cuentas IAM
- Inicio de sesión desde ubicación no habitual
- Bypass o ausencia de MFA en cuentas privilegiadas

---

### CLD-02 — Escalada de privilegios

> ¿Una identidad está ganando más privilegios?

- Asignación de permisos administrativos
- Modificación de políticas IAM
- Cambios en trust relationships

---

### CLD-03 — Abuso del plano de control cloud

> ¿Se está abusando de las APIs cloud?

- Llamadas API inusuales
- Uso de regiones no habituales
- Automatizaciones sospechosas

---

### CLD-04 — Exposición pública de recursos

> ¿Se ha expuesto un recurso sensible a Internet?

- Buckets públicos
- Bases de datos expuestas
- Reglas 0.0.0.0/0 hacia puertos críticos

---

### CLD-05 — Exfiltración de datos cloud

> ¿Se están extrayendo datos desde el cloud?

- Descarga masiva desde storage
- Replicación no autorizada
- Exportación de snapshots

---

### CLD-06 — Persistencia cloud

> ¿Alguien está creando mecanismos de acceso persistente?

- Creación de nuevos usuarios IAM
- Backdoors en trust policies
- Claves SSH en VMs

---

### CLD-07 — Evasión defensiva cloud

> ¿Alguien está desactivando controles?

- Desactivación de CloudTrail/GuardDuty/Defender
- Borrado de logs
- Eliminación de alertas

---

### CLD-08 — Movimiento lateral cloud

> ¿Un atacante está expandiendo su acceso?

- Salto entre cuentas
- Asunción anómala de roles
- Pivotaje desde workload al plano de control

---

### CLD-09 — Compromiso de workloads cloud

> ¿Algún workload está comprometido?

- Malware en instancias
- Web shells en servidores cloud
- Contenedores comprometidos

---

### CLD-10 — Configuración insegura o drift

> ¿El entorno se desvía de la configuración segura?

- Recursos sin cifrado
- Backups deshabilitados
- Políticas IAM excesivamente amplias

---

### CLD-11 — Uso no autorizado de servicios cloud

> ¿Se usan servicios fuera del marco autorizado?

- Uso de regiones prohibidas
- Creación de cuentas no controladas
- Despliegues fuera de pipeline

---

### CLD-12 — Criptominería y abuso de recursos

> ¿Se están usando recursos para minería?

- Instancias GPU anómalas
- Tráfico hacia pools de minería
- Picos de consumo

---

### CLD-13 — Anomalías de coste

> ¿Hay anomalía económica que indique abuso?

- Incremento brusco de gasto
- Uso inesperado de servicios caros
- Recursos huérfanos

---

### CLD-14 — Amenazas sobre almacenamiento cloud

> ¿El storage está siendo expuesto o manipulado?

- Buckets públicos
- Lectura o eliminación masiva
- Replicación hacia destinos no autorizados

---

### CLD-15 — Amenazas sobre bases de datos gestionadas

> ¿Las BBDD cloud están siendo expuestas?

- BBDD públicas
- Snapshots compartidos
- Consultas masivas

---

### CLD-16 — Ataques sobre Kubernetes y contenedores

> ¿La plataforma de contenedores está comprometida?

- Pods privilegiados
- Imágenes no autorizadas
- Escapes de contenedor

---

### CLD-17 — Serverless sospechoso

> ¿Las funciones cloud están siendo abusadas?

- Funciones con permisos excesivos
- Incremento brusco de invocaciones
- Conexiones salientes sospechosas

---

### CLD-18 — Secretos y credenciales expuestas

> ¿Se están exponiendo secretos críticos?

- Lectura anómala de secretos
- Claves API en variables de entorno
- Rotación deshabilitada

---

### CLD-19 — Cambios en red cloud

> ¿La red cloud está siendo modificada?

- Apertura de puertos críticos
- Peering no autorizado
- Exposición de servicios vía LB

---

### CLD-20 — Destrucción de recursos

> ¿Alguien está destruyendo activos cloud?

- Eliminación masiva de objetos/snapshots
- Cifrado sospechoso
- Borrado de claves KMS

---

