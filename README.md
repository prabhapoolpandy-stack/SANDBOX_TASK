# SANDBOX_TASK
My individual contributions and tasks undertaken as part of the AI for Climate Sandbox team presentation.

**Tasks Overview**

As part of the AI for Climate Sandbox work, my focus was on achieving quicker mask generation using the Segment Anything Model (SAM) by Meta.

**Objective**

To perform automated segmentation on geospatial .tif imagery and generate masks that can support training prediction models and environment/climate-related analysis.

**Approach & Experiments**
_1. Initial SAM Implementation_

Implemented SAM using the vit_h (default) checkpoint.

The output masks were not properly generated — only single-colored overlays (green/blue/red/pink).

Attempted visualization of the raw .tif files using:

Google Earth Engine (GEE): Images appeared completely black.

Python visualization: Displayed blank outputs.

_2. Data Preparation & Visualization_

The provided .tif images were all optical datasets.

Successfully mosaicked smaller sets of .tif files in ArcGIS and using Python.

Small mosaics produced images of limited spatial extent — SAM failed to detect meaningful objects from these.

Attempted to mosaic a larger dataset (300+ images) for improved input coverage - still no improvement in object detection.

_3. Model & System Constraints_

Encountered CUDA Out-of-Memory errors:

SAM with vit_h/vit_b required ~24.75 GiB GPU memory.

Local NVIDIA GPU had only 8 GiB total (≈5 GiB free).

Tried both CPU and GPU execution — both led to memory crashes or failed runs.

Downsampling images reduced file size but produced no valid masks (verified via QGIS).

Larger mosaics (e.g., Ireland1_mosaic.tif, ~103.8 MB) failed due to memory constraints — both locally and in Google Colab.

_4. Alternate Experiments
_
Tested the official SAM implementation from Meta’s GitHub repo on Google Colab.

Successfully generated and visualized masks for .jpg files (example-based runs worked).

When using .tif files, outputs were still inaccurate — likely due to the data’s spectral complexity and large pixel range.

_5. Performance Optimization_

Collected biodiversity images (≈1000) and performed mosaicking in python.

Exported the result to .png in QGIS, then converted to .jpg using Python for SAM compatibility.

Applied lower-resolution scaling and memory clearing before SAM execution.

Result: SAM successfully produced reasonable segmentation masks on smaller, simplified .jpg images.

**Key Observations**

SAM struggles with raw geospatial .tif data, especially multi-band or large raster mosaics.

GPU memory is the key bottleneck — even small .jpg images (4 MB) can trigger OOM errors depending on resolution.

Semantic labeling is not performed by SAM — all mask labeling needs to be done manually.

Google Colab proved useful for iterative testing and GPU-based experimentation.

**Summary**

This phase of the project focused on:

Evaluating SAM’s applicability to large .tif satellite imagery.

Understanding model and hardware constraints (especially GPU memory).

Testing preprocessing strategies (mosaicking, conversion, downsampling).

Successfully generating meaningful segmentation masks on optimized .jpg biodiversity data.

All experiments, preprocessing, and model runs were conducted in Google Colab and VS Code environments.
