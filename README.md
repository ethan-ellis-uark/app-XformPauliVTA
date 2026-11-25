# app-XformPauliVTA

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Transforms the Pauli atlas ventral tegmental area (VTA) probability map from MNI space into subject space with ANTs, then optionally thresholds, binarises and splits it into left and right ROIs.**

Optionally brain-extracts the ACPC-aligned T1 with FSL bet, computes an ANTs affine and warp between the subject and the bundled MNI152 1 mm template, applies the inverse to the Pauli VTA probabilistic map, thresholds it at maskThreshold, binarises it with FSL and splits it by hemisphere with AFNI. Use the resulting VTA ROIs as seeds for tractography.

| | |
|---|---|
| 📥 **Inputs** | `neuro/anat/t1w` |
| 📤 **Outputs** | `neuro/rois` · `neuro/transform/nifti` |
| 🐳 **Container** | `brainlife/fsl:5.0.9` |
| ⚙️ **Resources** | 1 CPUs |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.828](https://doi.org/10.25663/brainlife.app.828) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `t1` | `neuro/anat/t1w` (acpc_aligned) | yes | Subject T1 is used to compute transform files for Pauli VTA ROI. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `ROIs` | `neuro/rois` | Output directory for ROI nifti files |
| `xform` | `neuro/transform/nifti` | Output directory for ANTs xform files |

<details>
<summary><b>⚙️ Parameters</b> (4)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `brainMask` | boolean | `true` | Toggles script to run BET brain mask extraction. |
| `binarize` | boolean | `true` | Performs binarization of thresholded VTA ROI. |
| `split` | boolean | `true` | Splits thresholded and binarized VTA ROI into left and right hemispheres. |
| `maskThreshold` | number | `0.3` | Threshold value for voxel inclusion in xformed VTA ROI. |

</details>

<!-- brainlife-app:end -->

This app transforms Pauli Atlas VTA ROI from MNI space into subject space.

A template MNI brain and brain mask, along with the Pauli atlas VTA ROI in MNI space, is included in the app itself. The user supplies a subject-specific acpc-aligned T1 file, which will be used to compute affine and warp transform files from acpc to MNI space using ANTs and ITK. the Pauli atlas VTA ROI is then back-transformed into subject acpc space using these transform files.

Users have the option to threshold, binarize, and split the resulting VTA ROI by hemisphere.

The transformed VTA ROIs can then be used as seed ROIs in probabilistic tractography.
