<h1 align="center">XformPauliVTA</h1>

<p align="center">
  Transforms the Pauli atlas ventral tegmental area (VTA) probability map from MNI space into subject space with ANTs, then optionally thresholds, binarises and splits it into left and right ROIs.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.828"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.828-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Transforms the Pauli atlas ventral tegmental area (VTA) probability map from MNI space into subject space with ANTs, then optionally thresholds, binarises and splits it into left and right ROIs.**

Optionally brain-extracts the ACPC-aligned T1 with FSL bet, computes an ANTs affine and warp between the subject and the bundled MNI152 1 mm template, applies the inverse to the Pauli VTA probabilistic map, thresholds it at maskThreshold, binarises it with FSL and splits it by hemisphere with AFNI. Use the resulting VTA ROIs as seeds for tractography.

| | |
|---|---|
| **Inputs** | `neuro/anat/t1w` |
| **Outputs** | `neuro/rois` · `neuro/transform/nifti` |
| **Container** | `brainlife/fsl:5.0.9` |
| **Resources** | 1 CPUs |
| **Run it** | [doi.org/10.25663/brainlife.app.828](https://doi.org/10.25663/brainlife.app.828) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `t1` | `neuro/anat/t1w` (acpc_aligned) | yes | Subject T1 is used to compute transform files for Pauli VTA ROI. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `ROIs` | `neuro/rois` | Output directory for ROI nifti files |
| `xform` | `neuro/transform/nifti` | Output directory for ANTs xform files |

<details>
<summary><b>Parameters</b> (4)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `brainMask` | boolean | `true` | Toggles script to run BET brain mask extraction. |
| `binarize` | boolean | `true` | Performs binarization of thresholded VTA ROI. |
| `split` | boolean | `true` | Splits thresholded and binarized VTA ROI into left and right hemispheres. |
| `maskThreshold` | number | `0.3` | Threshold value for voxel inclusion in xformed VTA ROI. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.828](https://doi.org/10.25663/brainlife.app.828), choose `neuro/anat/t1w` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/rois`, `neuro/transform/nifti`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/fsl:5.0.9`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "t1": "/path/to/t1/t1",
       "brainMask": true,
       "binarize": true,
       "split": true,
       "maskThreshold": 0.3
   }
   ```

3. Run `./main`.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- XformPauliVTA. brainlife.io App. [doi:10.25663/brainlife.app.828](https://doi.org/10.25663/brainlife.app.828)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Avants et al. A reproducible evaluation of ANTs similarity metric performance in brain image registration. *NeuroImage* 54:2033-2044 (2011). [doi:10.1016/j.neuroimage.2010.09.025](https://doi.org/10.1016/j.neuroimage.2010.09.025)
- Cox. AFNI: Software for Analysis and Visualization of Functional Magnetic Resonance Neuroimages. *Computers and Biomedical Research* 29:162-173 (1996). [doi:10.1006/cbmr.1996.0014](https://doi.org/10.1006/cbmr.1996.0014)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

Maintained by [@ethan-ellis-uark](https://github.com/ethan-ellis-uark).
