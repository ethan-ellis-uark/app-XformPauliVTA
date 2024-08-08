# app-XformPauliVTA
This app transforms Pauli Atlas VTA ROI from MNI space into subject space.

A template MNI brain and brain mask, along with the Pauli atlas VTA ROI in MNI space, is included in the app itself. The user supplies a subject-specific acpc-aligned T1 file, which will be used to compute affine and warp transform files from acpc to MNI space using ANTs and ITK. the Pauli atlas VTA ROI is then back-transformed into subject acpc space using these transform files.

Users have the option to threshold, binarize, and split the resulting VTA ROI by hemisphere.

The transformed VTA ROIs can then be used as seed ROIs in probabilistic tractography.
