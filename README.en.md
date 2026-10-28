<div align="center">

<img src="assets/hero.png" width="100%" alt="AIHelper PCB/AOI vision workbench concept illustration">

# AIHelper

### A PCB/AOI vision development and evaluation workbench

Model debugging, browser annotation, interactive visualization, quality scoring, and version comparison — with tools for annotation handoff and data collection.

<p>
  <img alt="Python" src="https://img.shields.io/badge/Python-3.11%20%7C%203.12-3776AB?logo=python&logoColor=white">
  <img alt="Computer Vision" src="https://img.shields.io/badge/Computer%20Vision-AOI-00A6A6">
  <img alt="Inference" src="https://img.shields.io/badge/Inference-ONNX%20%7C%20TensorRT-76B900">
  <img alt="Source" src="https://img.shields.io/badge/Source-Private-7C3AED">
</p>

[中文](README.md) · [Annotation & visualization](#browser-annotation-and-visualization) · [Scoring & comparison](#quality-reports-and-version-comparison) · [Full feature catalog (中文)](docs/features.md)

</div>

> [!IMPORTANT]
> This is the public showcase for AIHelper. Business source code, model weights, production data, and internal configuration remain in a private repository.

## Overview

AIHelper supports algorithm development, evaluation, annotation, and data collection. The desktop workbench runs and inspects models; browser tools maintain ground truth and review predictions and scores; standalone reporting scripts aggregate existing evaluations into HTML dashboards and Excel workbooks.

| Area | What users can do |
| :--- | :--- |
| Inference and debugging | Inspect detection, classification, orientation, substructure, and OCR across board, region, and standalone tasks |
| HTML annotation | Edit rotated boxes, parent-child annotations, OCR text and reading direction, and evaluation exclusions |
| HTML visualization | Toggle result layers, compare predictions with GT, and locate missed, extra, or misclassified objects |
| Quality scoring | Evaluate detection, classification, substructure, and OCR separately; inspect geometric quality |
| Version comparison | Compare programs and versions, inspect component categories, prioritize issues, and export HTML and Excel |
| Data delivery | Hand off portable annotation packages, reuse Result v2, integrate headless inference, and collect image crops |

![Conceptual flow from inference and human annotation to evaluation and version reports](assets/workflow.svg)

This is a capability diagram. Human annotation maintains ground truth (GT); evaluation reads it without changing it. Saved results can also be reviewed or evaluated directly.

## Browser annotation and visualization

### HTML annotation workbench

Switch between board views and component crops to annotate Stage1 components, Stage2 substructures, and OCR. Edit rotated boxes by drawing, moving, resizing, or changing angles; use multiple selection, copy, cut, paste, delete, and undo. OCR annotations support a primary transcription, alternative acceptable text, and reading direction. Exclusion regions define the evaluation scope.

The local annotation service validates parent-child references and document revisions, with backups and transactional saving across the three annotation documents. Portable packages bundle image sources, GT, frozen predictions, and a Windows annotation runtime for handoff to another computer. Saving requires the local service; the package uses sequential handoff, without concurrent editing or automatic merging.

### Interactive HTML result review

The prediction viewer provides board zoom and pan, stage layer toggles, category counts, and linked component lists. Evaluation reports overlay GT and predictions, filter missed detections, false positives, classification errors, or box quality, and navigate to the corresponding image location. CLS and OCR have dedicated result and evaluation views.

The desktop software-semantics workspace additionally offers synchronized views before and after box completion, plus a program detection tree. These tools connect individual image evidence with the reported metrics.

## Quality reports and version comparison

| Analysis level | Report content |
| :--- | :--- |
| Object | IoU, GT coverage, prediction coverage, center displacement, width/height error, and angle error |
| Program | Separate Stage1 detection, CLS classification, Stage2 substructure, and OCR detection/recognition/direction results |
| Program batch | Aggregate metrics, component categories, worst programs, and geometric error distributions |
| Version | Stage-specific comparisons, metric deltas, issue prioritization, and links to source reports |

Detection and classification are scored separately. A stage with available results and the required GT can be evaluated without rerunning the full pipeline. DIR differences against Stage1 GT angles remain diagnostic; they are not a standalone DIR accuracy score.

### Aggregate scoring tools

`综合评分.py` reads existing score records from one output directory or multiple version directories and produces:

- **An Excel workbook** with stage, program, category, and version comparison metrics.
- **A summary or version-comparison dashboard** for stage and program performance.
- **A development diagnostics page** with version/stage/program/component filters, risk ordering, geometric error distributions, and links back to individual reports.

Original run records are retained; comparisons select the corresponding latest batches by default. Scores stay separate by task. HTML can be generated with `--html-only`; Excel generation requires Node.js and `@oai/artifact-tool`.

The companion tools are `生成版本对比驾驶舱.py`, `生成开发调试指标.py`, and `生成工作簿.mjs`. A separate `benchmark_aggregate_report.py` generates batch summaries. Their roles are documented in the [feature catalog (中文)](docs/features.md); scripts and production reports remain in the private repository.

## Data delivery and specialized tools

| Tool | Purpose |
| :--- | :--- |
| Portable annotation packages | Continue annotation on another Windows computer and return the GT directory |
| Data collection interface | Invoke board detection plus classification or image OBB through subprocesses and a JSON contract |
| Image batch processing | Recursive discovery, resume, segmented runs, per-image persistence, and progress events |
| DIP crop collection | Save native image crops by predicted category, together with a manifest |
| Standalone AI detection plans | Run OCR, solder-bridge detection, or segmentation in rotated regions |
| Native solder-bridge integration reference | C ABI, C++/C# examples, build tools, and runtime checks |
| Environment and regression tools | Startup checks, backend checks, cache preparation, input fingerprints, checkpoint comparison, and semantic replay |

SMT, THT, and DIP have different supported stage combinations. Crop collection is a data preparation capability; the native SDK is an integration reference, with model quality and device acceptance assessed separately.

## Demo

These recordings show desktop inference and batch execution. Browser annotation, scoring, and version dashboards are described above and in the feature catalog.

### Single-program inference

<div align="center">
  <img src="assets/smt-workflow.gif" width="92%" alt="AIHelper single-program workflow demo">
</div>

### Multi-program batch execution

<div align="center">
  <img src="assets/multi-program.gif" width="92%" alt="AIHelper multi-program batch demo">
</div>

## Architecture

<div align="center">
  <img src="assets/architecture.svg" width="96%" alt="AIHelper public architecture overview">
</div>

Inference interfaces share the application pipeline. Browser annotation uses a local service to maintain GT. Viewers and evaluators consume structured results; standalone aggregation scripts read saved score records. Stable data contracts connect these tools. See [Architecture (中文)](docs/architecture.md).

## Inference pipeline

<div align="center">
  <img src="assets/pipeline.svg" width="100%" alt="AIHelper inference pipeline">
</div>

The SMT baseline uses Input → SMT → CLS → DIR → IC → OCR. DIR corrects production parent boxes; Stage2 GT mode uses GT parents instead. THT and DIP use their supported stage combinations, with results restored to board coordinates.

## Core engineering work

- Consolidated desktop, batch, and standalone inference behind one request and execution contract.
- Established coordinate and evidence lineage for rotated geometry and parent-child results.
- Kept inference work in background tasks while UI updates remain on the main thread.
- Built regression gates around immutable golden baselines and preserved difference reports.
- Connected stable annotation identities with object-level diagnostics, program scores, category summaries, and version reports.
- Defined lifecycles for model preparation, session pools, concurrency, and GPU-heavy stages.

## Technology

```text
Application     Python · Qt Desktop GUI · Batch CLI
Browser tools   HTML · JavaScript · Canvas · Local annotation service
Vision          OpenCV · ONNX Runtime · TensorRT
Pipeline        Event-driven orchestration · Typed requests
Validation      Pytest · Golden baseline · Structured reports
Reporting       Interactive HTML · Version dashboards · Excel
Data            DZI · SQLite · JSON · Image tiles
```

Historical validation record: 1,984 pytest cases collected in the private codebase on 2026-10-23. This is a dated collection count; source regression, model quality, and device acceptance are tracked separately. See [Engineering (中文)](docs/engineering.md).

---

<div align="center">
  <sub>Engineering portfolio · Proprietary source code is not publicly distributed</sub>
</div>
