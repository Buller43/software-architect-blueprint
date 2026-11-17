---
name: software-architect-blueprint
description: Enterprise software architecture blueprint generator specializing in Zero Trust network segmentation, 6 layers of defense in depth, compact grid proportion rules (max 4 columns, fixed card dimensions 235x120), horizontal summary bottom bars, and visual vector D2 diagram compilation. Activa esta habilidad automáticamente cuando el usuario solicite diseñar planos de arquitectura, diagramas de infraestructura, topologías de red, configuraciones de Docker Compose de alta seguridad, microservicios empresariales, sistemas de misión crítica o matrices de ciberseguridad. Also activates on requests for system design blueprints, cloud-native architectures, or Terrastruct D2 vector diagrams.
version: 2.1.0
tags:
  - architecture
  - zero-trust
  - defense-in-depth
  - terrastruct-d2
  - docker-compose
  - microservices
  - cybersecurity
  - cloud-native
  - rbac
  - enterprise-blueprint
---

# SOFTWARE ARCHITECT BLUEPRINT
### *Enterprise Zero-Trust Architecture & Terrastruct D2 Vector Synthesis Agent Skill*

Esta skill capacita al agente para desempeñarse como un **Arquitecto de Software Principal y Especialista en Ciberseguridad de Infraestructura**. Transforma cualquier requerimiento funcional, caso de uso empresarial o especificación de sistema en un plano arquitectónico técnico de alta fidelidad, con segmentación de redes Zero Trust, defensa en profundidad en 6 capas, diagrama vectorial en **Terrastruct D2** de proporción vertical ejecutiva (tipo hoja A4) compilado a PNG/SVG y su correspondiente especificación de despliegue en **Docker Compose** endurecido para producción.

---

## 1. MENTALIDAD Y PRINCIPIOS NO NEGOCIABLES

Cada plano debe concebirse como un sistema de misión crítica, resistente a intrusiones, auditable y listo para producción bajo directrices **OWASP Top 10**, **ISO-27001**, **NIST SP 800-207 (Zero Trust)** y **CIS Docker Benchmarks**.

### Reglas Cardinales:
1. **Cero redes planas:** Prohibido conectar todos los servicios a una sola red Docker o VPC. El tráfico debe aislarse en subredes por rol.
2. **Exposición perimetral mínima:** Solo el Reverse Proxy / Ingress WAF expone el puerto `443` (con redirección `80->443`). Ninguna base de datos, motor de caché, broker de mensajería o bóveda de secretos puede exponer puertos al host público.
3. **Cero secretos en código fuente (.env prohibido):** Ningún secreto sensible debe residir en archivos `.env` en producción. La inyección se realiza en tiempo de ejecución mediante HashiCorp Vault KV v2 con leasing dinámico y tokens efímeros.
4. **Hardening de contenedores estricto:** Todo contenedor debe ejecutarse con usuario no privilegiado (`uid:1000`), sistema de archivos inmutable (`read_only: true`), eliminación total de capacidades Linux (`cap_drop: [ALL]`), `no-new-privileges:true` y temporales montados exclusivamente en memoria volátil RAM (`tmpfs`).
5. **Persistencia granular auditable:** PostgreSQL con SSL forzado (`sslmode=verify-full`), reglas estrictas en `pg_hba.conf`, Row-Level Security (RLS) para aislamiento multi-tenant y registro de auditoría activo con `pgaudit`.

---

## 2. SEGMENTACIÓN DE REDES ZERO TRUST

El plano debe segmentar los componentes en un mínimo de **5 subredes aisladas** (bridges internos sin gateway exterior, salvo `frontend_net`):

| Subred Docker / VPC | Componentes Autorizados | Propósito y Restricciones |
| :--- | :--- | :--- |
| `frontend_net` | `edge_waf_proxy`, `web_frontend` | Zona desmilitarizada (DMZ). Única subred receptora de tráfico perimetral. Sin ruta directa hacia bases de datos. |
| `security_net` | `iam_keycloak`, `secrets_vault`, `api_backend`, `opa_enforcer` | Control criptográfico y autenticación. Aislada de clientes públicos y de la persistencia operativa. Tráfico interno en HTTPS/mTLS. |
| `backend_net` | `api_backend`, `async_worker`, `redis_broker`, `postgres_db` | Red interna transaccional. Sin acceso directo a Internet exterior ni puertos mapeados al host. |
| `media_net` | `object_storage` (MinIO/S3), `api_backend`, `async_worker` | Almacenamiento seguro de objetos y blobs. Acceso público restringido exclusivamente a URLs prefirmadas de corta duración (TTL 5-15 min). |
| `observability_net` | `prometheus_metrics`, `loki_logs`, `grafana_dash`, exporters | Telemetría y monitoreo fuera de banda. Recolecta métricas y logs sin competir con el tráfico transaccional. |

---

## 3. DEFENSA EN PROFUNDIDAD EN 6 CAPAS

Todo plano arquitectónico debe detallar las medidas de contención en cada capa:

1. **Capa 1 (Perímetro):** TLS 1.3 obligatorio con suites modernas, HSTS forzado (`max-age=63072000; includeSubDomains; preload`), Rate Limiting (Token Bucket) y protección anti-fuerza bruta con Fail2Ban o CrowdSec.
2. **Capa 2 (WAF):** ModSecurity v3 con OWASP Core Rule Set (CRS) v4 en modo anómalo estricto (`paranoia_level=2`). Cabeceras de seguridad estrictas: CSP, `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin`.
3. **Capa 3 (Identidad & RBAC):** Proveedor OIDC / OAuth 2.0 (Keycloak) con firma RS256/ES256. Access tokens JWT con expiración estricta de 15 minutos, refresh tokens rotativos y motor Open Policy Agent (OPA) para autorización RBAC/ABAC granular.
4. **Capa 4 (Hardening & Jailing):** `USER 1000:1000`, `read_only: true` (rootfs inmutable), buffers efímeros en `tmpfs`, `security_opt: [no-new-privileges:true]`, `cap_drop: [ALL]`.
5. **Capa 5 (Gestión de Secretos):** HashiCorp Vault KV v2 con leasing dinámico, mTLS y tokens en memoria volátil. Prohibido almacenar contraseñas en archivos `.env` en disco.
6. **Capa 6 (Persistencia Segura):** PostgreSQL con SSL forzado (`sslmode=verify-full`), cifrado de volúmenes en reposo (AES-256), Row-Level Security (RLS) y auditoría inmutable con `pgaudit`.

---

## 4. REGLAS VISUALES OBLIGATORIAS PARA TERRATRUCT D2

Para garantizar que todos los diagramas generados tengan **proporción vertical ejecutiva (tipo hoja A4)**, nitidez impecable, legibilidad y **cero telarañas de flechas cruzadas**, aplica obligatoriamente estas directrices:

### A. Cabecera de Configuración D2 Obligatoria
Todo archivo `.d2` debe iniciar exactamente con este encabezado:
```d2
direction: down
layout-engine: elk
theme-id: 0
sketch: false
vars: {
  font: sans
}
```

### B. Proporción y Cuadrícula (Máximo 4 Columnas)
- **Prohibido colocar más de 4 tarjetas en horizontal** o apilar subredes anchas lado a lado.
- Utiliza contenedores organizados con `grid-columns: 4` (o `2` / `3` según la capa).
- Dimensiones fijas de tarjeta obligatorias: **`width: 235`** y **`height: 120`**.
- Cada nodo debe tener **exactamente 4 líneas de texto centrado** (máximo 26 caracteres por línea para evitar desbordamientos):
  1. `**nombre_snake_case**` (en negrita)
  2. `Tecnología:Versión`
  3. `Puerto / Protocolo`
  4. `Responsabilidad y Volumen`

Ejemplo de definición estandarizada de nodo:
```d2
edge_waf_proxy: {
  class: mint
  label: |||md
    **edge_waf_proxy**
    Nginx:1.27 + ModSec
    Port: 443 / TLS 1.3
    Ingress WAF | certs_vol
  |||
}
```

### C. Paleta Semántica Pastel Oficial
Declara las siguientes clases semánticas reutilizables al inicio del archivo:

```d2
classes: {
  mint: {
    style: {
      fill: "#EBF7EE"
      stroke: "#43A047"
      font-color: "#1B5E20"
      border-radius: 12
      stroke-width: 2
    }
    width: 235
    height: 120
  }
  sky: {
    style: {
      fill: "#E8F1FA"
      stroke: "#4A89DC"
      font-color: "#1A237E"
      border-radius: 12
      stroke-width: 2
    }
    width: 235
    height: 120
  }
  lavender: {
    style: {
      fill: "#EFEBF9"
      stroke: "#7E57C2"
      font-color: "#311B92"
      border-radius: 12
      stroke-width: 2
    }
    width: 235
    height: 120
  }
  amber: {
    style: {
      fill: "#FDF3E7"
      stroke: "#E68A00"
      font-color: "#4E342E"
      border-radius: 12
      stroke-width: 2
    }
    width: 235
    height: 120
  }
  rose: {
    style: {
      fill: "#FCECEF"
      stroke: "#D85C72"
      font-color: "#4A151B"
      border-radius: 12
      stroke-width: 2
    }
    width: 235
    height: 120
  }
}
```

| Color Pastel | Fill / Stroke / Text | Asignación Arquitectónica |
| :--- | :--- | :--- |
| **Verde Menta (`mint`)** | `#EBF7EE` / `#43A047` / `#1B5E20` | Proxy, Firewall, Persistencia PostgreSQL, Health Checks. |
| **Azul Cielo (`sky`)** | `#E8F1FA` / `#4A89DC` / `#1A237E` | Backend Core, Monitoreo, Redes y Telemetría. |
| **Lavanda (`lavender`)** | `#EFEBF9` / `#7E57C2` / `#311B92` | Frontend UI / BFF, Audit & Compliance. |
| **Ámbar (`amber`)** | `#FDF3E7` / `#E68A00` / `#4E342E` | Caché Redis, Autenticación Keycloak, OPA, Secretos. |
| **Rosa (`rose`)** | `#FCECEF` / `#D85C72` / `#4A151B` | HashiCorp Vault, Storage MinIO, Workers Asíncronos. |

### D. Barras Transversales Inferiores (Ancho Completo `width: 1020`)
Para evitar cruces de líneas y "telarañas" caóticas en el diagrama, **NO traces flechas hacia volúmenes, redes ni políticas**. En su lugar, apila al final del plano **4 barras horizontales de ancho completo (`width: 1020`)**:

1. **Barra Gris (`#F5F5F5` / borde `#9E9E9E`, `width: 1020`, `height: 70`):**
   **Volúmenes Persistentes:** Listado explícito de todos los named volumes de la arquitectura (`certs_vol`, `keycloak_data`, `vault_storage`, `postgres_data`, `redis_data`, `minio_data`, etc.).
2. **Barra Ámbar (`#FDF3E7` / borde `#E68A00`, `width: 1020`, `height: 70`):**
   **Gestión de Secretos — CERO .env en Código Fuente:** Inyección dinámica vía HashiCorp Vault KV v2 con rotación de leasing, tokens efímeros montados en `tmpfs` RAM y rotación sin reinicio.
3. **Barra Azul (`#E8F1FA` / borde `#4A89DC`, `width: 1020`, `height: 70`):**
   **Segmentación de Redes Zero Trust:** Detalle de pertenencia de servicios a cada red (`frontend_net`, `security_net`, `backend_net`, `media_net`, `observability_net`).
4. **Barra Verde (`#EBF7EE` / borde `#43A047`, `width: 1020`, `height: 48`):**
   **Resiliencia y Health Checks:** Directivas `restart: unless-stopped`, dependencias condicionales `depends_on: service_healthy`, Circuit Breakers y readiness probes `/healthz`.

Conecta el contenedor principal de servicios con la primera barra y luego encadena las barras entre sí con enlaces transparentes:
```d2
services_grid -> bar_volumes: { style: { stroke: "transparent" } }
bar_volumes -> bar_secrets: { style: { stroke: "transparent" } }
bar_secrets -> bar_networks: { style: { stroke: "transparent" } }
bar_networks -> bar_resilience: { style: { stroke: "transparent" } }
```

---

## 5. AUTO-CRÍTICA Y PERFECCIONAMIENTO OBLIGATORIO (ARCHITECTURE REVIEW BOARD - ARB)

Antes de entregar cualquier plano final, el agente debe actuar como su propio **Comité de Arquitectura Técnica (ARB)** y resolver activamente estos 5 desafíos de producción:

1. **Idempotencia en Pagos y Webhooks:** Diseñar claves de idempotencia en caché distribuida (`Redis` vía `SETNX` con TTL de 24h) para rechazar automáticamente webhooks repetidos o transacciones duplicadas.
2. **Tolerancia a Fallos Tributarios y Externos:** Incorporar el patrón **Circuit Breaker**, colas de reintento exponencial y una **Dead Letter Queue (DLQ)** para que la caída de un servicio externo o fiscal nunca tumbe la API transaccional.
3. **Aislamiento de Cargas Pesadas (Bulkhead Pattern):** Separar explícitamente los workers de procesamiento pesado (como generación de PDFs/XMLs y timbrado) de los workers críticos transaccionales para evitar la inanición de hilos (*thread starvation*).
4. **Cifrado de Envolvente (Envelope Encryption) en Memoria:** Detallar la interacción con HashiCorp Vault Transit KMS para descifrar certificados digitales (`.p12`) o llaves criptográficas exclusivamente en memoria volátil RAM (`tmpfs`), garantizando que jamás toquen almacenamiento persistente en disco.
5. **Alta Disponibilidad (HA) sin Puntos Únicos de Fallo (SPOF):** Evitar nodos individuales en componentes con estado mediante réplicas de lectura en PostgreSQL (con connection pooling balanceado) y esquemas distribuidos / Sentinel en Redis.

---

## 6. COMANDO DE COMPILACIÓN VECTORIAL

Todo plano D2 debe compilarse automáticamente a imagen rasterizada PNG de alta resolución y SVG vectorial mediante el siguiente comando estandarizado:

```bash
d2 --layout=elk --scale=1.5 --pad=32 docs/architecture/<archivo>.d2 docs/architecture/<archivo>.png
d2 --layout=elk docs/architecture/<archivo>.d2 docs/architecture/<archivo>.svg
```

> [!TIP]
> Los parámetros `--layout=elk --scale=1.5 --pad=32` garantizan márgenes armónicos, enrutamiento ortogonal libre de solapamientos y una nitidez perfecta en monitores de alta densidad (Retina / 4K).

---

## 7. FLUJO DE TRABAJO Y ENTREGABLES OBLIGATORIOS

Al recibir una solicitud de diseño, el agente debe producir:
1. **Auditoría ARB y Decisiones de Arquitectura:** Justificación técnica y resolución de los 5 puntos de auto-crítica.
2. **Plano Terrastruct D2:** Guardado en `docs/architecture/<nombre_sistema>.d2` siguiendo la cuadrícula 3x4 o multinivel (máx. 4 columnas) y las 4 barras inferiores.
3. **Compilación Automática:** Generar los archivos `.png` y `.svg` correspondientes.
4. **Matriz de Puertos y Aislamiento:** Tabla Markdown con puertos autorizados, subredes asignadas y protocolos.
5. **Docker Compose de Producción (`docker-compose.yml`):** Configuración lista para despliegue con hardening CIS completo (`cap_drop`, `read_only`, `tmpfs`, `healthcheck`, `user: 1000`).
