# 🤖 Sistema de Selección Inteligente de Candidatos

Proyecto final — Automatización con IA | CoderHouse

## 📋 Descripción
Flujo automatizado que recibe CVs por email, los evalúa con IA comparándolos contra 
un perfil de puesto (RAG), notifica a RRHH para una decisión humana y responde 
automáticamente al candidato según el resultado.

## 🛠️ Tecnologías integradas
| Tecnología | Uso |
|------------|-----|
| **n8n** | Orquestador principal del flujo |
| **Airtable** | Base de datos y registro de candidatos |
| **OpenAI GPT-4.1-mini** | Evaluación y análisis de CVs |
| **Pinecone** | Vector store para RAG (perfil del puesto) |
| **Gmail** | Canal de entrada y salida de comunicaciones |

## 🔄 Flujo del sistema
1. Candidato envía CV por email con asunto "CV"
2. n8n detecta el email y registra al candidato en Airtable con `Estado: Pendiente`
3. IA extrae datos del CV y lo evalúa contra el perfil del puesto via RAG
4. Airtable se actualiza con puntaje y justificación (`Estado: Procesado por IA`)
5. RRHH recibe email con resumen del candidato y botones **Aprobar / Rechazar**
6. El flujo espera la decisión humana (Human in the Loop)
7. Según la decisión:
   - ✅ **Aprobado** → email de citación a entrevista + Airtable `Estado: Aprobado`
   - ❌ **Rechazado** → email de agradecimiento + Airtable `Estado: Rechazado`
8. En caso de error → se registra en Airtable y se notifica a RRHH por email

## 🗄️ Base de datos Airtable
(https://airtable.com/invite/l?inviteId=invwCiFQTayjLgkRR&inviteToken=92c090939176cf259fb88b1aa48c9f7fd49e68e9d25ce8c4e3b0dec90263cc9b&utm_medium=email&utm_source=product_team&utm_content=transactional-alerts)

## 🎥 Video demo
https://drive.google.com/file/d/15NVEyDFaiE6b7zk0ad-PlpePMdx5zv0A/view?usp=sharing

## 📁 Archivos del repositorio
- `flujo-n8n.json` — Workflow completo para importar en n8n
- `diagrama-arquitectura.pdf` — Diagrama de arquitectura del sistema
- `capturas/` — Screenshots del flujo en acción

## ⚙️ Cómo importar el flujo
1. Abrí n8n
2. Hacé clic en **+** → **Import from file**
3. Seleccioná `flujo-n8n.json`
4. Configurá tus propias credenciales en cada nodo

## 🔐 Credenciales necesarias
- Gmail OAuth2
- Airtable Personal Access Token
- OpenAI API Key
- Pinecone API Key
- OpenRouter API Key
