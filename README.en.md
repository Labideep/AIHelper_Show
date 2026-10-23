<div align="center">

<img src="assets/hero.png" width="100%" alt="AIHelper — AOI vision workflow validation platform">

# AIHelper

### An AOI vision pipeline validation and debugging workbench

A traceable workflow for image input, detection, classification, orientation correction, substructure analysis, OCR, and baseline validation.

<p>
  <img alt="Python" src="https://img.shields.io/badge/Python-3.11%20%7C%203.12-3776AB?logo=python&logoColor=white">
  <img alt="Computer Vision" src="https://img.shields.io/badge/Computer%20Vision-AOI-00A6A6">
  <img alt="Inference" src="https://img.shields.io/badge/Inference-ONNX%20%7C%20TensorRT-76B900">
  <img alt="Source" src="https://img.shields.io/badge/Source-Private-7C3AED">
</p>

[中文](README.md) · [Architecture](docs/architecture.md) · [Engineering](docs/engineering.md)

</div>

> [!IMPORTANT]
> This is the public showcase for AIHelper. Business source code, model weights, production data, and internal configuration remain in a private repository.

## Overview

AIHelper turns fragmented AOI model-debugging activities into a consistent engineering workflow. It provides a shared execution contract for interactive debugging and batch regression while preserving enough evidence to identify the first stage at which two runs diverge.

| Area | Capability |
| :--- | :--- |
| Pipeline | Input → SMT → CLS → DIR → IC → OCR |
| Interfaces | Desktop GUI, batch jobs, standalone inference |
| Traceability | Stage events, structured results, visual reports, run identity |
| Validation | Read-only baselines, explicit failures, preserved diff reports |
| Engineering | Unified orchestration, coordinate integrity, thread safety, GPU lifecycle |

## Demo

<div align="center">
  <img src="assets/smt-workflow.gif" width="92%" alt="AIHelper single-program workflow demo">
</div>

<br>

<div align="center">
  <img src="assets/multi-program.gif" width="92%" alt="AIHelper multi-program batch demo">
</div>

## Architecture

<div align="center">
  <img src="assets/architecture.svg" width="96%" alt="AIHelper public architecture overview">
</div>

The application layer provides one execution contract across interfaces. Domain modules focus on vision stages, while infrastructure owns image sources, state, configuration, and published outputs.

## Engineering highlights

- One request and pipeline contract across GUI and batch entry points.
- Explicit coordinate and evidence lineage for rotated geometry and parent-child results.
- Background workers publish events; UI updates remain on the main thread.
- Golden baselines are immutable during validation, and every difference produces a report.
- Model preparation, session pools, concurrency, and GPU-heavy stages have defined lifecycles.

## Private-source policy

This repository intentionally excludes source code, private Git history, model files, customer programs, production images, credentials, and deployment configuration. A live product demonstration and private code walkthrough can be arranged during a technical interview.

---

<div align="center">
  <sub>Engineering portfolio · Proprietary source code is not publicly distributed</sub>
</div>
