<div align="center">

# AIHelper

### A PCB/AOI vision development and evaluation workbench

Connect multiple models, human annotation, and quality evaluation — from full-board images to individual components and version comparisons.

[Demos](#product-demos) · [Features](#what-you-can-do) · [Project depth](#the-problems-the-project-addresses) · [Full feature catalog (中文)](docs/features.md) · [中文](README.md)

</div>

> This is the public showcase for AIHelper. Source code, models, and production data remain private.

PCB automated optical inspection (AOI) involves locating components, identifying their category and orientation, detecting leads and pads, and reading text. Each step can affect later decisions. A model change then needs evaluation across different boards and component categories.

AIHelper brings desktop debugging, browser annotation, interactive reports, and batch evaluation into this workflow. Algorithm developers can trace stage results, testers can compare versions, and annotators can maintain ground truth, with their work linked through the same images and results.

## Product demos

### One program: inspect multiple detection stages

Load program images, run detection, classification, and text recognition, and inspect stage progress, results, and timing in one view.

![Desktop demo: running a program and inspecting detection results](assets/smt-workflow.gif)

### Multiple programs: batch execution and saved results

Process multiple programs, follow their execution status, and save results and reports for subsequent score aggregation and version comparison.

![Desktop demo: multi-program batch execution and progress](assets/multi-program.gif)

## What you can do

### Run detection and inspect each component

Zoom from the full board to an individual component to inspect boxes, categories, internal structures, and recognized text. Run a particular stage or selected region as needed, or process multiple programs in a batch.

The desktop also lets you inspect software-generated detection boxes and compare synchronized views before and after box completion.

### Annotate in the browser

Draw and adjust rotated boxes for components, leads, pads, and text. Use multiple selection, copy and paste, undo, and component navigation. OCR annotations also capture text and reading direction.

The editor saves ground truth through a local service. Portable tasks can be handed to another Windows computer for continued annotation.

### Find problems on the image

Interactive HTML views overlay predictions and human annotations. Filter missed detections, false positives, classification errors, or box positioning issues, then navigate directly to the relevant component.

Detection, classification, and text recognition are evaluated separately, helping distinguish a missed object from an incorrect category, misplaced box, or transcription error.

### Compare versions with quality reports

Aggregate scores across programs into **HTML dashboards and Excel reports**. Compare versions, programs, and component categories.

Development reports prioritize issues, show position, size, and angle error distributions, and link back to individual program reports for image inspection.

[Explore aggregate scoring and its companion tools (中文)](docs/features.md#5-综合评分版本对比与开发诊断)

## The problems the project addresses

### Connecting multiple models around the same component

A component's position, category, orientation, internal structure, and text come from different processing steps. An orientation adjustment can change the images used by subsequent cropping and recognition.

AIHelper connects these steps, retains relationships between components, leads, pads, and text, and lets users compare model results with software-generated detection boxes. When results differ, the processing history helps locate where the difference begins.

### Preserving positions between full boards and small structures

The same board may be viewed under different lighting and at different image sizes, then tiled, resized, or cropped at an angle. Small differences in a local crop can affect lead, pad, or text positions when mapped back to the board.

AIHelper retains image transforms and result positions, restores results to board coordinates, and supports detailed local viewing. Evaluation examines center displacement, size, angle, and coverage to help identify geometric problems.

### Tracing version changes to programs, categories, and objects

A model can perform differently across programs and component categories. Version evaluation needs to reveal both overall changes and local problems.

AIHelper evaluates detection, classification, internal structures, and text recognition separately, then aggregates results by program and component category. Version dashboards, error distributions, and links to source reports let readers follow an unusual metric back to the relevant image.

### Keeping annotation and evaluation grounded in explicit references

Component, internal-structure, and text annotations are related. Editing or handing off annotations requires checking that these relationships remain valid and that an older browser page cannot overwrite newly saved work.

AIHelper checks relationships and revision conflicts when saving, and retains backups. Scoring reads human-maintained ground truth; saved results can be reevaluated and historical scores can be aggregated again, without automatically changing annotations to improve a score.

## Beyond desktop debugging

The same capabilities support other parts of the workflow:

- **Annotation handoff:** package images, existing annotations, and predictions for continued work on another Windows computer, then return the completed annotations.
- **Sample preparation:** process image folders with resume support, or collect component crops by predicted category for review and dataset organization.
- **Standalone algorithms and external calls:** test text recognition, solder-bridge detection, or segmentation in selected regions, and provide results to data collection projects through headless interfaces.

The [full feature catalog (中文)](docs/features.md) also covers `综合评分.py` and its HTML/Excel reporting tools, DIP crop collection, and the native solder-bridge integration reference.

## Project documentation

- [Feature catalog (中文)](docs/features.md): capabilities, standalone tools, and usage boundaries.
- [Project story (中文)](docs/project-story.md): the problems behind the project and a typical workflow.
- [Architecture (中文)](docs/architecture.md) · [Engineering (中文)](docs/engineering.md): implementation, validation, and design decisions.

<sub>Built with Python · Qt · OpenCV · ONNX Runtime · TensorRT · HTML / JavaScript</sub>
