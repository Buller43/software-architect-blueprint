# 📐 SOFTWARE ARCHITECT BLUEPRINT
### *Enterprise Zero-Trust Architecture & Terrastruct D2 Vector Synthesis Agent Skill for Google Antigravity*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Antigravity Skill](https://img.shields.io/badge/Antigravity-Agent%20Skill-0052CC.svg)](https://deepmind.google/technologies/gemini/)
[![Terrastruct D2](https://img.shields.io/badge/D2-Terrastruct%20v0.9+-7B2CBF.svg)](https://d2lang.com/)
[![Zero Trust](https://img.shields.io/badge/Security-Zero%20Trust%20(6%20Layers)-2E7D32.svg)](references/security_6_layers.md)

**`software-architect-blueprint`** es una habilidad profesional (*Agent Skill*) de grado empresarial para **Google Antigravity**. Convierte a tu asistente de IA en un **Arquitecto de Software Principal y Especialista en Ciberseguridad de Infraestructura**, capaz de diseñar planos de arquitectura técnica de grado bancario (Zero Trust, 6 capas de defensa en profundidad, hardening CIS de contenedores, auto-crítica ARB) y compilarlos automáticamente a **diagramas vectoriales (PNG/SVG) en Terrastruct D2** con proporción vertical ejecutiva (tipo hoja A4) y sus correspondientes archivos **`docker-compose.yml` listos para producción**.

---

## 🌟 CAPACIDADES Y ESTÁNDARES INCORPORADOS

- **Segmentación Estricta Zero Trust:** Impide la creación de redes planas. Fuerza el aislamiento en 5 subredes Docker independientes: `frontend_net`, `backend_net`, `security_net`, `media_net` y `observability_net`.
- **Defensa en Profundidad en 6 Capas:**
  1. *Perímetro:* TLS 1.3 forzado, HSTS, Rate Limiting (Token Bucket) y mitigación Fail2Ban.
  2. *WAF:* ModSecurity v3 con OWASP Core Rule Set v4 en modo anómalo y cabeceras estrictas (CSP, X-Frame-Options: DENY, nosniff).
  3. *IAM / RBAC:* Keycloak OIDC/OAuth 2.0 con tokens JWT de 15 min, refresh tokens rotativos y motor de políticas OPA.
  4. *Hardening de Contenedores:* Ejecución non-root (`uid:1000`), filesystem inmutable (`read_only: true`), `CAP_DROP=ALL`, `no-new-privileges` y temporales en memoria RAM (`tmpfs`).
  5. *Gestión Dinámica de Secretos:* Prohibición absoluta de archivos `.env`. Integración con HashiCorp Vault KV v2 con credenciales efímeras y mTLS.
  6. *Persistencia Segura:* PostgreSQL con SSL verify-full, `pg_hba.conf` restrictivo, Row-Level Security (RLS) para aislamiento multi-tenant y auditoría `pgaudit`.
- **Reglas Visuales y Proporción A4 en Terrastruct D2:**
  - Configuración nativa con `direction: down`, `layout-engine: elk`, `theme-id: 0`, `sketch: false`.
  - Cuadrícula compacta de máximo 4 columnas por fila (`grid-columns: 4`).
  - Tarjetas con dimensiones fijas de **`width: 235`** y **`height: 120`**, con 4 líneas centradas de máximo 26 caracteres.
  - Paleta pastel semántica exacta (Verde Menta, Azul Cielo, Lavanda, Ámbar, Rosa).
  - **4 Barras Transversales Inferiores (`width: 1020`):** Volúmenes Persistentes, Gestión de Secretos, Segmentación de Redes y Resiliencia/Health Checks. Cero cruces caóticos de flechas.
- **Auto-Crítica Obligatoria (Architecture Review Board - ARB):** Idempotencia en Redis (`SETNX`), Circuit Breakers + DLQ, separación de workers pesados vs transaccionales, cifrado de envolvente en `tmpfs` y esquemas de Alta Disponibilidad (HA).

---

## 📁 ESTRUCTURA DE LA SKILL

```text
software-architect-blueprint/
├── SKILL.md                               # Manifiesto principal, directrices visuales D2 y reglas operativas
├── README.md                              # Documentación completa y guía de instalación
├── references/
│   └── security_6_layers.md               # Guía técnica profunda de las 6 capas + Matriz RBAC
└── templates/
    ├── docker_stack_blueprint.d2          # Plantilla D2 de microservicios en cuadrícula 3x4 + 4 barras
    ├── docker_stack_blueprint.png         # Renderizado PNG compilado con layout ELK
    ├── docker_stack_blueprint.svg         # Vectorial SVG
    ├── security_layers_blueprint.d2       # Plantilla D2 vertical de 6 capas de seguridad + RBAC
    ├── security_layers_blueprint.png      # Renderizado PNG compilado con layout ELK
    └── security_layers_blueprint.svg      # Vectorial SVG
```

---

## 🚀 INSTALACIÓN EN ANTIGRAVITY

Puedes instalar esta Skill de forma **global** (disponible para todos tus proyectos y conversaciones) o de forma **local** (específica para un repositorio o workspace).

### Opción A: Instalación Global (Recomendada)

#### En Windows (PowerShell):
```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.gemini\antigravity\skills"
Copy-Item -Recurse -Force "software-architect-blueprint" "$HOME\.gemini\antigravity\skills\software-architect-blueprint"
```

#### En Linux / macOS:
```bash
mkdir -p ~/.gemini/antigravity/skills
cp -r software-architect-blueprint ~/.gemini/antigravity/skills/software-architect-blueprint
```

---

### Opción B: Instalación Local por Proyecto

Si deseas que esta habilidad forme parte del repositorio de un proyecto específico:
```bash
mkdir -p .gemini/skills
cp -r software-architect-blueprint .gemini/skills/software-architect-blueprint
```

---

## 🛠️ INSTALACIÓN DEL CLI DE D2 (TERRASTRUCT)

Para compilar automáticamente los diagramas `.d2` a imágenes PNG de alta nitidez y archivos vectoriales `.svg` con el motor **ELK**:

### En Windows (PowerShell):
```powershell
# Descarga e instala directamente el binario oficial
Invoke-WebRequest -Uri "https://github.com/d2lang/d2/releases/download/v0.9.0/d2-v0.9.0-windows-amd64.tar.gz" -OutFile "d2.tar.gz"
tar -xzf d2.tar.gz
Move-Item "d2-v0.9.0/bin/d2.exe" "$HOME/bin/d2.exe"
Remove-Item "d2.tar.gz", "d2-v0.9.0" -Recurse -Force
```

### En Linux / macOS / WSL:
```bash
curl -fsSL https://d2lang.com/install.sh | sh -s --
d2 --version
```

### Comando Estándar de Compilación:
```bash
d2 --layout=elk --scale=1.5 --pad=32 templates/docker_stack_blueprint.d2 templates/docker_stack_blueprint.png
d2 --layout=elk templates/docker_stack_blueprint.d2 templates/docker_stack_blueprint.svg
```

---

## 🎨 PALETA SEMÁNTICA PASTEL OFICIAL EN D2

| Estilo | Código Fill | Código Borde | Código Texto | Asignación Arquitectónica |
| :--- | :--- | :--- | :--- | :--- |
| **Verde Menta (`mint`)** | `#EBF7EE` | `#43A047` | `#1B5E20` | Proxy, Firewall, Persistencia PostgreSQL, Health Checks |
| **Azul Cielo (`sky`)** | `#E8F1FA` | `#4A89DC` | `#1A237E` | Backend Core, Monitoreo, Redes y Telemetría |
| **Lavanda (`lavender`)** | `#EFEBF9` | `#7E57C2` | `#311B92` | Frontend UI / BFF, Audit & Compliance |
| **Ámbar (`amber`)** | `#FDF3E7` | `#E68A00` | `#4E342E` | Caché Redis, Autenticación Keycloak, OPA, Secretos |
| **Rosa (`rose`)** | `#FCECEF` | `#D85C72` | `#4A151B` | HashiCorp Vault, Storage MinIO, Workers Asíncronos |

---

## 📄 LICENCIA Y AUTORÍA

Distribuido bajo la licencia **MIT**.
Desarrollado para arquitectos de software, equipos de SecOps y líderes de ingeniería que buscan diseñar infraestructura visualmente impecable y técnicamente inexpugnable.
