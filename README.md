# SOFTWARE ARCHITECT BLUEPRINT
### Enterprise Zero-Trust Architecture & Terrastruct D2 Vector Synthesis Agent Skill for Google Antigravity

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Antigravity Skill](https://img.shields.io/badge/Antigravity-Agent%20Skill-0052CC.svg)](https://deepmind.google/technologies/gemini/)
[![Agensi Marketplace](https://img.shields.io/badge/Agensi-Verified%20Skill-7B2CBF.svg)](https://agensi.io)
[![Terrastruct D2](https://img.shields.io/badge/D2-Terrastruct%20v0.9+-FF6B6B.svg)](https://d2lang.com/)
[![Zero Trust](https://img.shields.io/badge/Security-Zero%20Trust%20(6%20Layers)-2E7D32.svg)](references/security_6_layers.md)

**software-architect-blueprint** es una habilidad profesional (*Agent Skill*) de grado empresarial disenada para **Google Antigravity** y compatible con el ecosistema de agentes **Agensi**. Transforma a tu asistente de IA en un **Arquitecto de Software Principal y Especialista en Ciberseguridad de Infraestructura**, capacitado para disenar planos tecnicos de mision critica (Zero Trust, 6 capas de defensa en profundidad, hardening CIS de contenedores, auto-auditoria ARB) y compilarlos automaticamente a **diagramas vectoriales (PNG/SVG) en Terrastruct D2** con proporcion vertical ejecutiva tipo hoja A4 y sus correspondientes archivos **docker-compose.yml listos para produccion**.

---

## CAPACIDADES Y ESTANDARES ARQUITECTONICOS

### 1. Segmentacion Estricta Zero Trust (5 Subredes Aisladas)
Rechaza categoricamente arquitecturas planas de una sola red. Divide la infraestructura en subredes Docker independientes con reglas de acceso minimas:
- **frontend_net:** Zona desmilitarizada (DMZ). Unica subred expuesta al exterior para recibir trafico perimetral (`edge_waf_proxy`, `web_frontend`). Sin ruta hacia bases de datos.
- **security_net:** Red de control de identidad y custodia criptografica (`iam_keycloak`, `secrets_vault`, `opa_enforcer`, `api_backend`). Aislada de clientes publicos; trafico interno HTTPS/mTLS.
- **backend_net:** Red transaccional interna (`api_backend`, `async_worker`, `redis_broker`, `postgres_db`). Sin mapeo de puertos al host ni salida directa no filtrada a Internet.
- **media_net:** Almacen seguro de blobs y objetos (`minio_storage`, `api_backend`, `async_worker`). Acceso publico restringido a URLs prefirmadas de corta duracion (TTL 5-15 min).
- **observability_net:** Telemetria fuera de banda (`prometheus_tsdb`, `loki_logs`, `grafana_dash`, exporters). Recolecta metricas y logs forenses sin competir con el trafico transaccional.

### 2. Defensa en Profundidad en 6 Capas
1. **Capa 1 (Perimetro):** TLS 1.3 estricto, HSTS forzado (`max-age=63072000; includeSubDomains; preload`), Rate Limiting (Token Bucket) y mitigacion Fail2Ban / CrowdSec.
2. **Capa 2 (WAF):** ModSecurity v3 con OWASP Core Rule Set (CRS) v4 en modo anomalo estricto (`paranoia_level=2`) y cabeceras estrictas (CSP, X-Frame-Options: DENY, nosniff).
3. **Capa 3 (Identidad & RBAC):** Keycloak OIDC/OAuth 2.0 con tokens JWT de 15 minutos, Refresh Token Rotation y validacion granular de politicas con Open Policy Agent (OPA).
4. **Capa 4 (Hardening & Jailing):** Ejecucion no-root (`uid:1000`), sistema de archivos inmutable (`read_only: true`), `cap_drop: [ALL]`, `no-new-privileges: true` y buffers efimeros en `tmpfs` RAM.
5. **Capa 5 (Gestion de Secretos):** Prohibicion absoluta de credenciales en archivos `.env`. Integracion nativa con HashiCorp Vault KV v2 con leasing dinamico y tokens efimeros.
6. **Capa 6 (Persistencia Segura):** PostgreSQL 16 con SSL obligatorio (`sslmode=verify-full`), cifrado AES-256 en reposo, Row-Level Security (RLS) multi-tenant y auditoria inmutable con `pgaudit`.

### 3. Auto-Critica Obligatoria (Architecture Review Board - ARB)
Antes de entregar cualquier plano, la skill audita y resuelve activamente los siguientes 5 escenarios criticos:
1. **Idempotencia en Pagos y Webhooks:** Claves `SETNX` en Redis con TTL de 24h para deduplicar eventos y evitar doble cobro o timbrado ante reintentos de red.
2. **Tolerancia a Fallos Tributarios y Externos:** Patron Circuit Breaker, reintentos exponenciales y Dead Letter Queue (DLQ) para aislar caidas de APIs bancarias o fiscales.
3. **Aislamiento de Cargas Pesadas (Bulkhead Pattern):** Separacion estricta de workers pesados (PDF/XML/documentos) vs workers transaccionales de baja latencia para evitar la inanicion de hilos (thread starvation).
4. **Cifrado de Envolvente (Envelope Encryption):** Custodia de claves privadas y certificados `.p12` en Vault Transit KMS y descifrado exclusivamente en memoria volatil (`tmpfs` RAM) sin escribir en disco.
5. **Alta Disponibilidad (HA) sin SPOF:** Replicas de lectura en PostgreSQL con connection pooling balanceado (PgBouncer) y cluster / Sentinel en Redis.

### 4. Directrices Visuales Terrastruct D2 (Proporcion Hoja A4)
- **Cero bloques `vars`:** Prohibido incluir `vars: { ... }` en el codigo D2. El layout y el tema se pasan por CLI: `d2 --layout=elk --theme=0 --pad=24`.
- **Raiz en bandas verticales:** `direction: down`, `grid-columns: 1`, `grid-gap: 16` para apilar bloques ordenadamente.
- **Formateo Markdown limpio:** Cada nodo usa bloques `|md ... |` con encabezados `###`, texto en negrita y vinetas separadas por `·`. Prohibido usar textos largos de una linea con plecas `|`.
- **Anchos fijos alineados:** Bandas completas de `width: 820` o `854`, grillas de 2 columnas con `width: 400` (`grid-gap: 20`), matrices 3x4 con `width: 200` (`grid-columns: 4`, `grid-gap: 18`) y `border-radius: 10`.
- **4 Barras Transversales Inferiores:** Para eliminar telaranas de lineas cruzadas, los volumenes, la gestion de secretos, la segmentacion de redes y las politicas de resiliencia se detallan en 4 barras horizontales al pie del diagrama.

---

## PALETA SEMANTICA PASTEL OFICIAL EN D2

| Estilo / Clase | Codigo Fill | Codigo Borde | Codigo Texto | Asignacion Arquitectonica |
| :--- | :--- | :--- | :--- | :--- |
| **Verde Menta (`mint`)** | `#EBF7EE` | `#43A047` | `#1B5E20` | Proxy, Ingress WAF, Persistencia PostgreSQL, Health Checks |
| **Azul Cielo (`sky`)** | `#E8F1FA` | `#4A89DC` | `#1A237E` | Backend Core API, Monitoreo, Redes y Telemetria |
| **Lavanda (`lavender`)** | `#EFEBF9` | `#7E57C2` | `#311B92` | Frontend UI / BFF, Audit Forensics & Compliance |
| **Ambar (`amber`)** | `#FDF3E7` | `#E68A00` | `#4E342E` | Cache Redis, Autenticacion Keycloak, OPA, Secretos |
| **Rosa (`rose`)** | `#FCECEF` | `#D85C72` | `#4A151B` | HashiCorp Vault, Storage MinIO S3, Workers Asincronos |

---

## ESTRUCTURA DE ARCHIVOS DE LA SKILL

```text
software-architect-blueprint/
├── SKILL.md                               # Manifiesto principal, directrices visuales D2 y reglas de arquitectura
├── README.md                              # Documentacion tecnica, estandares y guia de instalacion
├── LICENSE                                # Licencia MIT
├── references/
│   └── security_6_layers.md               # Guia tecnica profunda de las 6 capas de seguridad + Matriz RBAC
└── templates/
    ├── docker_stack_blueprint.d2          # Plantilla D2 de microservicios en cuadricula 3x4 + 4 barras
    ├── security_layers_blueprint.d2       # Plantilla D2 vertical de 6 capas de seguridad + RBAC
    └── fintech_billing_v2.d2              # Plantilla D2 para plataforma financiera SaaS multi-tenant
```

---

## GUIA DE INSTALACION Y USO

### Metodo 1: Instalacion en Google Antigravity

#### Opcion A: Instalacion Global (Recomendada)
Disponible permanentemente en todos tus proyectos y sesiones de Antigravity:

**En Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.gemini\antigravity\skills"
Copy-Item -Recurse -Force "software-architect-blueprint" "$HOME\.gemini\antigravity\skills\software-architect-blueprint"
```

**En Linux / macOS:**
```bash
mkdir -p ~/.gemini/antigravity/skills
cp -r software-architect-blueprint ~/.gemini/antigravity/skills/software-architect-blueprint
```

#### Opcion B: Instalacion para Otros Agentes Compatibles (~/.agents/skills)
```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.agents\skills"
Copy-Item -Recurse -Force "software-architect-blueprint" "$HOME\.agents\skills\software-architect-blueprint"
```

#### Opcion C: Instalacion Local por Proyecto
Copia la carpeta en la raiz de tu repositorio:
```bash
mkdir -p .gemini/skills
cp -r software-architect-blueprint .gemini/skills/software-architect-blueprint
```

---

### Metodo 2: Instalacion y Carga via Agensi MCP Marketplace

Esta skill esta adaptada para su indexacion y uso mediante el servidor **Agensi MCP**. Los usuarios con acceso al marketplace de Agensi pueden cargar y ejecutar la habilidad en cualquier sesion:

1. **Buscar la skill en Agensi:**
   ```json
   {
     "tool": "agensi_search_skills",
     "arguments": { "query": "software-architect-blueprint" }
   }
   ```
2. **Cargar la skill bajo demanda:**
   ```json
   {
     "tool": "agensi_get_skill",
     "arguments": { "slug": "software-architect-blueprint" }
   }
   ```
3. La skill se ejecuta localmente dentro de la sesion del agente sin enviar codigo fuente ni infraestructura confidencial a servidores externos.

---

### Instalacion del Compilador Terrastruct D2 CLI

Para compilar automaticamente los archivos `.d2` a imagenes PNG y diagramas vectoriales SVG:

#### En Windows (PowerShell):
```powershell
Invoke-WebRequest -Uri "https://github.com/d2lang/d2/releases/download/v0.9.0/d2-v0.9.0-windows-amd64.tar.gz" -OutFile "d2.tar.gz"
tar -xzf d2.tar.gz
Move-Item "d2-v0.9.0/bin/d2.exe" "$HOME/bin/d2.exe"
Remove-Item "d2.tar.gz", "d2-v0.9.0" -Recurse -Force
```

#### En Linux / macOS / WSL:
```bash
curl -fsSL https://d2lang.com/install.sh | sh -s --
d2 --version
```

#### Comando Estandar de Compilacion:
```bash
d2 --layout=elk --theme=0 --pad=24 docs/architecture/<archivo>.d2 docs/architecture/<archivo>.png
d2 --layout=elk --theme=0 --pad=24 docs/architecture/<archivo>.d2 docs/architecture/<archivo>.svg
```

---

## EJEMPLOS DE PROMPTS LISTOS PARA USAR

Una vez instalada, Antigravity activara la skill de forma automatica ante solicitudes de arquitectura, diagramas de infraestructura o disenos seguros:

### En Espanol:
```text
"Usa mi skill software-architect-blueprint para disenar la arquitectura de produccion de una Plataforma SaaS de Facturacion Electronica y Pagos en Tiempo Real con ModSecurity WAF, PostgreSQL con RLS y HashiCorp Vault."
```
```text
"Disena una arquitectura de telemedicina compatible con HIPAA con 6 capas de defensa en profundidad, matriz RBAC y exporta el plano D2 en formato A4 y el docker-compose.yml de produccion."
```
```text
"Genera un plano de microservicios para un e-commerce de alto trafico con cola de mensajeria RabbitMQ, workers Celery separados para pagos vs PDFs y cluster Redis para idempotencia."
```

### En Ingles:
```text
"Apply the software-architect-blueprint skill to design an enterprise Zero Trust core banking API with mutual TLS, Vault dynamic credentials, and compiled Terrastruct D2 ELK diagrams."
```
```text
"Create a hardened Docker Compose deployment and an A4-proportioned D2 architecture blueprint for an event-driven IoT sensor data pipeline."
```

---

## ENTREGABLES PRODUCIDOS EN CADA EJECUCION

1. **Auditoria ARB y Racional Tecnico:** Evaluacion de compromisos (trade-offs), mitigacion de riesgos y justificacion de patrones.
2. **Plano Terrastruct D2 (`docs/architecture/<nombre>.d2`):** Codigo declarativo limpio con cuadricula de maximo 4 columnas y 4 barras inferiores transversales.
3. **Diagramas Compilados:** Archivo rasterizado `.png` (alta resolucion) y vectorial `.svg`.
4. **Matriz de Seguridad & Puertos:** Tabla Markdown con subredes, puertos autorizados y directivas de aislamiento.
5. **Docker Compose de Produccion (`docker-compose.yml`):** Definicion con hardening CIS (`cap_drop: [ALL]`, `read_only: true`, `tmpfs`, `user: 1000:1000`, healthchecks condicionales).

---

## LICENCIA Y AUTORIA

Distribuido bajo la licencia **MIT**. Consulta el archivo `LICENSE` para mas detalles.
Desarrollado para arquitectos de software, ingenieros DevOps/SecOps y lideres tecnicos que buscan elevar la calidad visual y la seguridad de sus sistemas.
