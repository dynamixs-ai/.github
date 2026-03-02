# Dynamixs.AI

AI-powered Business Process Management for SMEs, built on the proven open source foundation
of [Imixs-Workflow](https://github.com/imixs/imixs-workflow).

---

## Platform

Dynamixs.AI combines a mature BPMN workflow engine with modern AI integration. Run structured
business processes with built-in LLM support, RAG-based document intelligence, and a full
document management stack — all deployable on any Jakarta EE application server or via Docker.

| Component        | Technology                      |
| ---------------- | ------------------------------- |
| Workflow Engine  | Imixs-Workflow (Jakarta EE)     |
| AI Integration   | OpenAI-compatible LLM endpoints |
| RAG Store        | Apache Cassandra                |
| Document Editing | Collabora Online (WOPI)         |
| OCR              | Apache Tika                     |

---

## Low-Code with BPMN

Dynamixs.AI is a **Low-Code platform** — business processes are designed visually using
[Open-BPMN](https://www.open-bpmn.org/), a free and open BPMN 2.0 modeler. No coding required
to define process flows, AI conditions, or document handling rules.

[![Open-BPMN Modeler](https://www.open-bpmn.org/images/imixs-bpmn-001.png)](https://www.open-bpmn.org/)

Open-BPMN runs in **Visual Studio Code**, **Eclipse IDE**, or directly **in the browser** —
no additional tooling setup needed for most partners.

- 🔷 [Open-BPMN Website](https://www.open-bpmn.org/)
- 📦 [Install Open-BPMN](https://www.open-bpmn.org/install.html)
- 🎓 [How to Model](https://www.open-bpmn.org/how_to_model.html)

---

## For Partners

Build and deliver custom workflow solutions on top of the Dynamixs.AI platform.
There are two ways to get started:

**☁️ Hosted by Dynamixs.AI**
No deployment at all — we run and maintain the platform for your customer.
You focus entirely on the BPMN process design and configuration.

**🐳 Quick Start — Docker Compose**
Spin up the full platform stack in minutes using our pre-built Docker image.
No build step required. Ideal for evaluations and standard deployments.

**🔧 Custom Build — WAR Overlay**
Extend the platform with your own UI components, CDI beans, and Java services
using the Maven WAR Overlay mechanism. Built for long-lived partner products.

👉 Get started with the **[Partner Template](https://github.com/dynamixs-ai/partner-template)**
— it covers both approaches with step-by-step instructions.

---

## Resources

- 🌐 [Website](https://www.dynamixs.ai)
- 🔷 [BPMN Model Library](https://github.com/dynamixs-ai/bpmn-library)
- 📖 [Imixs-Office-Workflow](https://doc.office-workflow.com)
- ⚙️ [Imixs-Workflow](https://www.imixs.org)

📬 Partner Onboarding: partner@dynamixs.ai
