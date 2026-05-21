# Catálogo de Casos de Uso — SOC GrayHats

**Documento técnico para el equipo de operaciones de seguridad**  
Versión 2.0 — Mayo 2026

---

# Catálogo de Casos de Uso — SOC GrayHats

**Documento técnico para el equipo de operaciones de seguridad**  
Superficies: Endpoints · Red · Cloud IaaS · Microsoft 365 · WAF  
Versión 2.0 — Mayo 2026

---

## Introducción

Este catálogo define los casos de uso de detección del SOC GrayHats, organizados por superficie de detección y, cuando las detecciones están desarrolladas, por plataforma específica. La estructura es jerárquica:

- **Nivel 1 — Superficie:** Endpoints, Red, Cloud IaaS, Microsoft 365, WAF.
- **Nivel 2 — Plataforma:** Windows, Linux, macOS (dentro de Endpoints); AWS, Azure (dentro de Cloud); etc.
- **Nivel 3 — Caso de uso genérico:** Categoría funcional de detección (ej. EP-01 Malware, EP-03 Persistencia).
- **Nivel 4 — Caso de uso concreto:** Ficha técnica con detección específica, telemetría, lógica, MITRE ATT&CK y severidad (ej. EP.02.WIN.AUTH.001).

Las superficies que aún no tienen fichas detalladas mantienen el inventario de casos de uso genéricos como referencia para su desarrollo futuro.

---

