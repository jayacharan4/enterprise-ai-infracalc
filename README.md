# Enterprise AI InfraCalc

A browser-based infrastructure planning calculator for GenAI workloads — GPU sizing, total cost of ownership, unit economics, and an AI assistant. No backend required; runs entirely client-side and deploys to Netlify as a single HTML file.

**Live demo:** https://eaidemo.netlify.app

---

## What it does

| Module | Description |
|---|---|
| **GenAI GPU Sizing** | Estimates GPU count, memory footprint, throughput, and latency for LLM inference deployments |
| **TCO Calculator** | Compares on-premises vs cloud IaaS total cost of ownership with break-even analysis |
| **Unit Economics** | Computes $/GPU-hour and $/1M tokens for both deployment options |
| **Sensitivity Analysis** | Models impact of power cost changes and GPU utilization on unit economics |
| **Formulas & Assumptions** | Step-by-step reference guide for all 27 calculation formulas |
| **AI Assistant** | Embedded chatbot that explains calculator results using your live numbers |

---

## Key features

- **Multi-turn conversation depth modeling** — KV cache sizing accounts for context accumulation across conversation turns, not just single-turn estimates
- **Hardware comparison mode** — side-by-side GPU sizing across AMD MI300X / MI325X / MI350X and NVIDIA H100 / H200
- **Workload presets** — Customer Chatbot, Code Assistant, RAG/Document QA, Batch Summarization
- **Export** — PDF (browser print), JSON download, shareable URL with state encoded in query params
- **Dark / light theme**
- **Mobile responsive**

---

## Supported hardware

| GPU | VRAM | Memory BW | BF16 TFLOPS | TDP |
|---|---|---|---|---|
| AMD MI300X | 192 GB | 5.3 TB/s | 1,307 | 750 W |
| AMD MI325X | 256 GB | 6.0 TB/s | 1,307 | 750 W |
| AMD MI350X | 288 GB | 8.0 TB/s | 2,614 | 800 W |
| NVIDIA H100 SXM | 80 GB | 3.35 TB/s | 989 | 700 W |
| NVIDIA H200 SXM | 141 GB | 4.8 TB/s | 989 | 700 W |

## Supported models

Llama 3 (8B / 70B / 405B), Mistral 7B, Mixtral 8×7B, DeepSeek-R1 (7B / 67B), Custom / Manual entry

## Cloud providers (TCO)

Azure (ND MI300X v5), DigitalOcean (MI300X on-demand & reserved)

---

## Project structure

```
netlify_deploy/
  index.html                  # Entire app — HTML, CSS, JS in one file
  InfraCalc_Formula_Guide.html  # Formula reference (27 formulas), embedded via iframe
.claude/
  agents/
    infracalc-data-editor.md    # Specialist agent for updating GPU/model/pricing data
    infracalc-feature-builder.md  # Specialist agent for adding new features
```

---

## Running locally

No build step — just open the file:

```bash
open netlify_deploy/index.html
```

Or serve it with any static server:

```bash
npx serve netlify_deploy
```

---

## Deploying to Netlify

```bash
netlify deploy --dir=netlify_deploy --prod
```

---

## Tech stack

- **Frontend:** Vanilla HTML / CSS / JavaScript — no framework
- **Charts:** Chart.js 4.5.0 (CDN)
- **AI assistant:** Cerebras API (`gpt-oss-120b`) — client-side fetch, no backend
- **Deployment:** Netlify (static)

---

## Disclaimer

All calculations are planning estimates based on published hardware specifications and publicly available model parameters. Results are for directional guidance only and do not constitute a binding quote or engineering guarantee.
