The following lists the pre-defined exclusion criteria for a study analyzing whole-brain data, in which the final EPI data will be normalized to a standard template, specifically MNI. Note that by “whole brain” we mean cortex and subcortical structures but not cerebellum.

**Exclusion criteria on unprocessed data based on the individual MRIQC visual report**

Summary
1. Heavy structure in the background
1. Signal drop-out in the brain
1. Heavy aliasing ghost
1. Wrap-around that overlaps with the brain 
1. Heavily structured crown region in the carpet plot
1. Peak in slice-wise noise average on background
1. Ripples caused by head-motion
1. Distortion of anatomy

Details
1. **Heavy structure in the background**

    As the background is just air, it should not contain signals. Hence if it does, the visible structure can be interpreted as an artifact. Non-homogeneous background is not a problem in itself as it is situated outside of the brain; the issue is that the latter artifact is likely overflowing on the brain, thus compromising brain signal. The aliasing ghost is a particular case of structure in the background, because the background displays a copy of the brain. We classified under exclusion criteria A, all other structures that do not correspond to an aliasing.

1. **Signal drop-out in the brain**

    We observed in many subjects a region where the signal vanishes. Those signal drop-out are probably caused by some interference with air or with a metallic object. In one particular data-site, the signal drop out commonly affected the inferior-medial part of the frontal lobe close to the ventricles. We also observed signal vanishing in the anterior part of the prefrontal cortex and next to the ears. Any signal drop-out observed resulted in exclusion of the scan.

1. **Heavy aliasing ghost**

    A ghost is a type of structured noise that appears as repeated versions of the main object, usually in the phase-encoding direction. They occur because of signal instability between pulse cycle repetitions and is most commonly a consequence of motion during imaging. Sometimes it can be spotted in the BOLD average, but it is most clear in the background noise visualization. We excluded the scans for which the ghost was approximately the same intensity as the interior of the brain in the background noise visualization.

1. **Wrap-around that overlaps with the brain**

    A wrap-around occurs whenever the dimensions of the object exceed the defined field-of-view (FOV). It is visible as a piece of the brain being folded over on the other side of the image. Note that we excluded subjects based on the observation of a wrap-around, only if the folded region contained or overlapped the cortex. In the MRIQC report, the wrap-around can be spotted on the bold average, on the std map and on the background noise visualization. We found however that the background noise visualization is most clear to assess whether the folded region overlaps the brain.

1. **Heavily structured crown region in the carpet plot**

    The carpet plot is a tool to visualize fMRI scan and assess its quality. It works by plotting voxel time-series in close spatial proximity so that the eye notes temporal coincidence (Power 2017). The crown corresponds to the voxels located on a closed-band around the brain. As those voxels are outside the brain, we do not expect to observe signal there, and if we do, we can interpret it as artifactual. Therefore, a strongly structured crown region in the carpet plot is a sign that artifacts are compromising the fMRI scan (Provins et al. 2022). For example, motion is often paired with a prolonged dark deflection (criterion EA). Furthermore, coil failure that manifests as a sudden change in overall signal intensity is easily identifiable from the carpet plot (criterion EB). In addition, clustering the carpet plot rows such that voxels with similar BOLD dynamics appear close to one another reveals non-global structure in the signal (Aquino et al. 2020). Thus strongly polarized structure in the carpet plot also suggests artifact influence (criterion EC). The reasoning behind the exclusion criteria based on the carpet plot is that if the signal outside the brain is too strongly modulated by artifacts, the signal of interest inside the brain likely is as well and thus cannot be trusted.

1. **Peak in slice-wise noise average on background**

    The slice-wise noise average on background should not present peaks. A peak corresponds to a high intensity increase in a particular slice and if observed, the subject was excluded. Those spikes can be due to an electric discharge in the scanner or can be related to a high motion event. Any peak observed resulted in exclusion of the scan.

1. **Ripples caused by head-motion**

    Motion is sometimes visible as concentric ripples originating at brain-air interfaces. If the ripples are too strong, it blurs brain structure and destroys contrast. In case the ripples blurs anatomy and stretches to the whole brain, the scan was excluded. However it was often faintly visible on a local spot, in which case we did not exclude the scan.

1. **Distortion of anatomy**

    The anatomy being distorted in a way that is not plausible biologically represents an exclusion criterion. Examples of such distortion found in this dataset were the prefrontal cortex stretching beyond the limit of the skull or abnormally enlarged ventricles.

**Exclusion criteria on minimally pre-processed data based on the fMRIPrep visual report**

Summary
1. Failure in normalization to MNI space
1. Brain mask not well-defined

Details
1. **Failure in normalization to MNI space**

    Because the final conclusions of the hypothetical analysis are based on data normalized to a standard template, it is crucial the normalization is successful. The fMRIPrep report contains a widget to assess the quality of the normalization to MNI space. The widget moves back and forth between the MNI template and the BOLD average normalized onto that template. To verify quality, one needs to verify that the following structures are well aligned (in order of importance) : 1. ventricles, 2. subcortical regions, 3. corpus callosum, 4. cerebellum and, 5.  gray matter cortex (one can be more lenient on this last structure). Moreover, one structure that helped me discard several subjects is the misalignment of the black strike indicating an overly stretched cerebellum and contracted occipital lobe. A misalignment of the ventricles, the subcortical regions, the corpus callosum or the black strike yielded immediate exclusion. Scans were excluded based on the misalignment of the gray matter cortex, only if the gray matter was visibly distorted in a sole direction.

1. **Brain mask not well-defined**

    The brain mask should follow closely the contour of the brain. Many subjects were thus excluded from this dataset because the brain mask forms bumps surrounding high intensity patches of the skull. Moreover, the brain mask should not contain holes, thus if a region affected by signal drop-out created a hole in the brain mask, the subject was excluded.
