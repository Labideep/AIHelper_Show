<div align="center">

# AIHelper

### Run models. Annotate images. Review results. Compare versions.

A PCB/AOI vision toolkit for inspecting and evaluating model results.

[Demo](#see-it-in-action) · [Features](#what-you-can-do) · [Version comparison](#a-typical-version-comparison) · [Full feature catalog (中文)](docs/features.md) · [中文](README.md)

</div>

> This is the public showcase for AIHelper. Source code, models, and production data remain private.

AIHelper supports algorithm development, testing, and annotation for PCB automated optical inspection (AOI). Run detection on the desktop, edit annotations and inspect errors in the browser, then compare model versions through quality reports.

## See it in action

Load a program, run detection, classification, and text recognition, and inspect progress and results in one view.

![Desktop demo: running a program and inspecting detection results](assets/smt-workflow.gif)

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

## A typical version comparison

Suppose you have changed a model and want to understand where it improves or regresses:

1. **Run the same programs** with the same inputs and human annotations, saving results and scores for both versions.
2. **Compare the reports** to find changes in detection, classification, or text recognition for specific programs and categories.
3. **Inspect individual objects** by following a summary link to a program report and locating missed, misclassified, or poorly positioned detections.
4. **Continue debugging with those examples**, using the images, annotations, and predictions to decide what to investigate next.

Saved results can be evaluated directly, and report aggregation does not require another inference run. Scoring reads human annotations without automatically changing them to improve a score.

<details>
<summary><strong>Watch the multi-program batch demo</strong></summary>

Process multiple programs, follow progress, and save results and reports for each one.

![Desktop demo: multi-program batch execution and progress](assets/multi-program.gif)

</details>

## More useful tools

- **Annotation handoff:** package images, existing annotations, and predictions so another computer can continue the task and return the annotations.
- **Sample collection and batches:** process image folders with resume support and organize component crops by predicted category.
- **Local algorithm experiments:** run text recognition, solder-bridge detection, or segmentation in selected regions.
- **External integration:** provide detection results through headless interfaces for data collection and other workflows.

The [full feature catalog (中文)](docs/features.md) also covers standalone tools, including `综合评分.py`, DIP crop collection, and the native solder-bridge integration reference.

## Learn more

- [Feature catalog (中文)](docs/features.md): capabilities, standalone tools, and usage boundaries.
- [Project story (中文)](docs/project-story.md): the problems behind the project and a typical workflow.
- [Architecture (中文)](docs/architecture.md) · [Engineering (中文)](docs/engineering.md): implementation, validation, and design decisions.

<sub>Built with Python · Qt · OpenCV · ONNX Runtime · TensorRT · HTML / JavaScript</sub>
