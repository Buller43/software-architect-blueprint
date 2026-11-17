# ðŸ“ SOFTWARE ARCHITECT BLUEPRINT
### *Enterprise Zero-Trust Architecture & Terrastruct D2 Vector Synthesis Agent Skill for Google Antigravity*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Antigravity Skill](https://img.shields.io/badge/Antigravity-Agent%20Skill-0052CC.svg)](https://deepmind.google/technologies/gemini/)
[![Terrastruct D2](https://img.shields.io/badge/D2-Terrastruct%20v0.9+-7B2CBF.svg)](https://d2lang.com/)
[![Zero Trust](https://img.shields.io/badge/Security-Zero%20Trust%20(6%20Layers)-2E7D32.svg)](references/security_6_layers.md)

**`software-architect-blueprint`** es una habilidad profesional (*Agent Skill*) de grado empresarial para **Google Antigravity**. Convierte a tu asistente de IA en un **Arquitecto de Software Principal y Especialista en Ciberseguridad de Infraestructura**, capaz de diseÃ±ar planos de arquitectura tÃ©cnica de grado bancario (Zero Trust, 6 capas de defensa en profundidad, hardening CIS de contenedores, auto-crÃ­tica ARB) y compilarlos automÃ¡ticamente a **diagramas vectoriales (PNG/SVG) en Terrastruct D2** con proporciÃ³n vertical ejecutiva (tipo hoja A4) y sus correspondientes archivos **`docker-compose.yml` listos para producciÃ³n**.

---

## ðŸŒŸ CAPACIDADES Y ESTÃNDARES INCORPORADOS

- **SegmentaciÃ³n Estricta Zero Trust:** Impide la creaciÃ³n de redes planas. Fuerza el aislamiento en 5 subredes Docker independientes: `frontend_net`, `backend_net`, `security_net`, `media_net` y `observability_net`.
- **Defensa en Profundidad en 6 Capas:**
  1. *PerÃ­metro:* TLS 1.3 forzado, HSTS, Rate Limiting (Token Bucket) y mitigaciÃ³n Fail2Ban.
  2. *WAF:* ModSecurity v3 con OWASP Core Rule Set v4 en modo anÃ³malo y cabeceras estrictas (CSP, X-Frame-Options: DENY, nosniff).
  3. *IAM / RBAC:* Keycloak OIDC/OAuth 2.0 con tokens JWT de 15 min, refresh tokens rotativos y motor de polÃ­ticas OPA.
  4. *Hardening de Contenedores:* EjecuciÃ³n non-root (`uid:1000`), filesystem inmutable (`read_only: true`), `CAP_DROP=ALL`, `no-new-privileges` y temporales en memoria RAM (`tmpfs`).
  5. *GestiÃ³n DinÃ¡mica de Secretos:* ProhibiciÃ³n absoluta de archivos `.env`. IntegraciÃ³n con HashiCorp Vault KV v2 con credenciales efÃ­meras y mTLS.
  6. *Persistencia Segura:* PostgreSQL con SSL verify-full, `pg_hba.conf` restrictivo, Row-Level Security (RLS) para aislamiento multi-tenant y auditorÃ­a `pgaudit`.
- **Reglas Visuales y ProporciÃ³n A4 en Terrastruct D2:**
  - ConfiguraciÃ³n nativa con `direction: down`, `layout-engine: elk`, `theme-id: 0`, `sketch: false`.
  - CuadrÃ­cula compacta de mÃ¡ximo 4 columnas por fila (`grid-columns: 4`).
  - Tarjetas con dimensiones fijas de **`width: 235`** y **`height: 120`**, con 4 lÃ­neas centradas de mÃ¡ximo 26 caracteres.
  - Paleta pastel semÃ¡ntica exacta (Verde Menta, Azul Cielo, Lavanda, Ãmbar, Rosa).
  - **4 Barras Transversales Inferiores (`width: 1020`):** VolÃºmenes Persistentes, GestiÃ³n de Secretos, SegmentaciÃ³n de Redes y Resiliencia/Health Checks. Cero cruces caÃ³ticos de flechas.
- **Auto-CrÃ­tica Obligatoria (Architecture Review Board - ARB):** Idempotencia en Redis (`SETNX`), Circuit Breakers + DLQ, separaciÃ³n de workers pesados vs transaccionales, cifrado de envolvente en `tmpfs` y esquemas de Alta Disponibilidad (HA).

---

## ðŸ“ ESTRUCTURA DE LA SKILL

```text
software-architect-blueprint/
â”œâ”€â”€ SKILL.md                               # Manifiesto principal, directrices visuales D2 y reglas operativas
â”œâ”€â”€ README.md                              # DocumentaciÃ³n completa y guÃ­a de instalaciÃ³n
â”œâ”€â”€ references/
â”‚   â””â”€â”€ security_6_layers.md               # GuÃ­a tÃ©cnica profunda de las 6 capas + Matriz RBAC
â””â”€â”€ templates/
    â”œâ”€â”€ docker_stack_blueprint.d2          # Plantilla D2 de microservicios en cuadrÃ­cula 3x4 + 4 barras
    â”œâ”€â”€ docker_stack_blueprint.png         # Renderizado PNG compilado con layout ELK
    â”œâ”€â”€ docker_stack_blueprint.svg         # Vectorial SVG
    â”œâ”€â”€ security_layers_blueprint.d2       # Plantilla D2 vertical de 6 capas de seguridad + RBAC
    â”œâ”€â”€ security_layers_blueprint.png      # Renderizado PNG compilado con layout ELK
    â””â”€â”€ security_layers_blueprint.svg      # Vectorial SVG
```

---

## ðŸš€ INSTALACIÃ“N EN ANTIGRAVITY

Puedes instalar esta Skill de forma **global** (disponible para todos tus proyectos y conversaciones) o de forma **local** (especÃ­fica para un repositorio o workspace).

### OpciÃ³n A: InstalaciÃ³n Global (Recomendada)

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

### OpciÃ³n B: InstalaciÃ³n Local por Proyecto

Si deseas que esta habilidad forme parte del repositorio de un proyecto especÃ­fico:
```bash
mkdir -p .gemini/skills
cp -r software-architect-blueprint .gemini/skills/software-architect-blueprint
```

---

## ðŸ› ï¸ INSTALACIÃ“N DEL CLI DE D2 (TERRASTRUCT)

Para compilar automÃ¡ticamente los diagramas `.d2` a imÃ¡genes PNG de alta nitidez y archivos vectoriales `.svg` con el motor **ELK**:

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

### Comando EstÃ¡ndar de CompilaciÃ³n:
```bash
d2 --layout=elk --scale=1.5 --pad=32 templates/docker_stack_blueprint.d2 templates/docker_stack_blueprint.png
d2 --layout=elk templates/docker_stack_blueprint.d2 templates/docker_stack_blueprint.svg
```

---

## ðŸŽ¨ PALETA SEMÃNTICA PASTEL OFICIAL EN D2

| Estilo | CÃ³digo Fill | CÃ³digo Borde | CÃ³digo Texto | AsignaciÃ³n ArquitectÃ³nica |
| :--- | :--- | :--- | :--- | :--- |
| **Verde Menta (`mint`)** | `#EBF7EE` | `#43A047` | `#1B5E20` | Proxy, Firewall, Persistencia PostgreSQL, Health Checks |
| **Azul Cielo (`sky`)** | `#E8F1FA` | `#4A89DC` | `#1A237E` | Backend Core, Monitoreo, Redes y TelemetrÃ­a |
| **Lavanda (`lavender`)** | `#EFEBF9` | `#7E57C2` | `#311B92` | Frontend UI / BFF, Audit & Compliance |
| **Ãmbar (`amber`)** | `#FDF3E7` | `#E68A00` | `#4E342E` | CachÃ© Redis, AutenticaciÃ³n Keycloak, OPA, Secretos |
| **Rosa (`rose`)** | `#FCECEF` | `#D85C72` | `#4A151B` | HashiCorp Vault, Storage MinIO, Workers AsÃ­ncronos |

---

## ðŸ“„ LICENCIA Y AUTORÃA

Distribuido bajo la licencia **MIT**.
Desarrollado para arquitectos de software, equipos de SecOps y lÃ­deres de ingenierÃ­a que buscan diseÃ±ar infraestructura visualmente impecable y tÃ©cnicamente inexpugnable.
