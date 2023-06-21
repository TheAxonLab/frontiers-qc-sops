The following lists the steps in a quality assessment/quality control (QA/QC) procedure on functional MRI data using MRIQC and fMRIPrep:


## Before starting QA/QC
- [ ] Create a standard operating procedures (SOPs) document for the study. The template https://github.com/nipreps/mriqc-sops has been design to facilitate this step.
- [ ] Narrow down the scope of the planned analysis. Here, the planned analysis correponds to whole-brain, voxel-wise analyses of spatially standardized task and resting-state BOLD fMRI. Note that by “whole-brain” we mean cortex and subcortical structures but not cerebellum, because we expected those regions to fall outside of the field of view in a number of the BOLD datasets.
- [ ] Pre-define the exclusion criteria according to the scope of the planned analysis, the placement of the QA/QC checkpoint along the neuroimaging workflow and what type of data are available in the datasets.
- [ ] Write a clear description of each exclusion criteria in the SOPs (including how to deal with borderline cases).
- [ ] Make a *snapshot* of the current state of your SOPs and assign them a new *version* label (cf (here)[./index.md])
- [ ] Download the data locally using DataLad for version control.
    ```
    cd /data/datasets/
    datalad clone <url-to-data>
    ```
- [ ] Retrieve file content
    ```
    cd /data/datasets/
    datalad get <url-to-data>
    ```


## Image processing
- [ ] Image processing was carried out according to our protocol (Esteban et al. 2020)
- [ ] Run MRIQC with a Docker container of its latest version 22.0.1. MRIQC generates one visual report per T1w image and per BOLD scan.
- [ ] Once all the visual reports had been evaluated as indicated below (QC of the unprocessed data), run fMRIPrep with a Docker container of its latest version 22.0.0 only the data that survived the first QC checkpoint with MRIQC. fMRIPrep is executed with default settings, therefore, data are spatially standardized into the MNI152NLin2009cAsym space (Fonov et al. 2009) accessed with TemplateFlow (Ciric et al. 2022). fMRIPrep yielded preprocessed data and one individual QA/QC report per subject.


## QC of unprocessed data
- [ ] Inspect one-by-one the individual MRIQC visual reports of each BOLD scan first, following the reports’ ordering of visualizations. Once the full report had been visualized, return to specific sections of the report when a second assessment was necessary.
- [ ] Report QC assessment on a spreadsheet table indicating which criteria led to exclusion.
- [ ] Exclude the scans meeting the pre-defined exclusion criteria on unprocessed data.
- [ ] Apply the same protocol to T1w images. Note that we do not impose exclusion criterion on the unprocessed T1w images, but we annotate subjects with visible artifacts in the T1w images in order to ensure rigorous scrutinizing of spatial normalization and surface reconstruction outputs from fMRIPrep (if both modalities passed the first QC checkpoint with MRIQC). We do this, because given the planned analysis, the T1w image will be used solely to guide the spatial alignment to the standard MNI152NLin2009cAsym template and to guide the co-registration of structural and functional (BOLD) images in fMRIPrep via the surface reconstructions. Besides, the latter preprocessing steps are relatively robust to structural images with mild artifacts.


## QC of minimally preprocessed data
- [ ] Inspect one-by-one the individual reports from fMRIPrep for each participant,following the reports’ ordering of visualizations.
- [ ] Report QC assessment on a spreadsheet table indicating which criteria led to exclusion.
- [ ] Exclude the scans meeting the pre-defined exclusion criteria on minimally preprocessed data.


## References
* Ciric, Rastko, William H. Thompson, Romy Lorenz, Mathias Goncalves, Eilidh MacNicol, Christopher J. Markiewicz, Yaroslav O. Halchenko, et al. 2022. “TemplateFlow: FAIR-Sharing of Multi-Scale, Multi-Species Brain Models.” bioRxiv. <https://doi.org/10.1101/2021.02.10.430678>.

* Esteban, Oscar, Rastko Ciric, Karolina Finc, Ross W. Blair, Christopher J. Markiewicz, Craig A. Moodie, James D. Kent, et al. 2020. “Analysis of Task-Based Functional MRI Data Preprocessed with FMRIPrep.” Nature Protocols 15 (7): 2186–2202. <https://doi.org/10.1038/s41596-020-0327-3>.

* Fonov, VS, AC Evans, RC McKinstry, CR Almli, and DL Collins. 2009. “Unbiased Nonlinear Average Age-Appropriate Brain Templates from Birth to Adulthood.” NeuroImage, Organization for Human Brain Mapping 2009 Annual Meeting, 47 (July): S102. <https://doi.org/10.1016/S1053-8119(09)70884-5>.