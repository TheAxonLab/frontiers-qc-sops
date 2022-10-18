The following lists the pre-defined exclusion criteria for a whole-brain, voxel-wise analyses of spatially standardized task and resting-state BOLD fMRI. Note that by “whole brain” we mean cortex and subcortical structures but not cerebellum.Our exclusion criteria are all based on the visual inspection of the individual MRIQC and fMRIPrep reports, so they are all qualitative criteria. Exclusion criteria are defined in reference to specific artifacts and qualitative aspects of BOLD and T1w images. Furthermore, we do not differentiate criteria for task and resting-state scans, because our defined scope was not specific enough (e.g., lacking in objectives to determine whether some regions are of particular interest), except for the hyperintensity of single slices criterion.

**Exclusion criteria for unprocessed BOLD data based on the individual MRIQC visual report**

Summary
1. Artifactual structures in the background
1. Susceptibility distortion artifacts
    1. Signal drop-out
    1. Brain distortion
1. Aliasing ghosts
1. Wrap-around that overlaps with the brain 
1. Structured crown region in the carpet plot
    1. due to motion peaks
    1. due to periodic motion
    1. due to coil failure
    1. drift of unknown source
1. Artifacts detected with independent components analysis
1. Hyperintensities of single slice
1. Vertical strikes in the sagittal plane of the standard deviation map
1. Data formatting issues

Details
1. **Artifactual structures in the background (A)**

    Because no BOLD signal originates from the air surrounding the head, the background should not contain visible structures. However, signals sourcing from the object of interest can spill into the background through a number of imaging processes, e.g., aliasing ghosts, spill-over originating from moving and blinking eyes, or bulk head motion. Structures in the background are most clearly noticeable in MRIQC’s “background noise panel” view, but they frequently are also detectable in the standard deviation map view. Structure in the background is not a problem in itself as it is situated outside of the brain; the issue is that the latter artifact is likely overflowing on the brain, thus compromising brain signal. The aliasing ghost is a particular case of structure in the background, discussed in further detail in criterion C below. We classify under exclusion criteria A all other structures that do not correspond to an aliasing artifact.

1. **Susceptibility distortion artifacts (B)**

    Susceptibility distortions are caused by B0 field non-uniformity (Hutton et al. 2002). Indeed, inserting an object in the scanner bore perturbs the nominal B0 field, which should be constant all across the FoV. Specifically, tissue boundaries produce steps of deviation from the nominal B0 field, which are larger where the air is close to tissues. Because of these deviations, the signal is recorded at locations slightly displaced from the sampling grid along the phase encoding axis leading to susceptibility distortions (Esteban et al. 2021). Susceptibility distortions manifest in two different ways on the BOLD average panel of the MRIQC visual report (Figure S2): as signal drop-out, that is a region where the signal vanishes (criterion BA), or as brain distortions (criterion BB). Signal drop-outs often appear close to brain-air interfaces as explained below; these include ventro-medial prefrontal cortex, the anterior part of the prefrontal cortex and the region next to the ear cavities. Susceptibility distortion artifacts can be corrected by the susceptibility distortion correction implemented in fMRIPrep, provided that a fieldmap associated to the BOLD image has been acquired and is correctly referenced in the dataset. This means that the presence of susceptibility distortions does not necessarily constitute an exclusion criterion. However, given the application scope of this paper, since no fieldmaps were shared with the dataset and because we did not identify regions of little interest where these artifacts may be less detrimental, any signal drop-out observed results in exclusion of the scan. In practice, legacy datasets without fieldmaps can still be usable if researchers take adequate mitigation approaches (which also require rigorous QA/QC).

1. **Aliasing ghost (C)**

    A ghost is a type of structured noise that appears as shifted and faint repeated versions of the main object, usually in the phase encoding direction. They occur for several reasons, such as signal instability between pulse cycle repetitions, or the particular strategy of echo-planar imaging to record the k-space during acquisition, and is often exacerbated by within-volume head motion. Sometimes it can be spotted in the BOLD average view of the MRIQC visual report, but it is most clear in the background noise visualization. We exclude the scans for which the ghost was approximately the same intensity as the interior of the brain in the background noise visualization.

1. **Wrap-around (D)**

    Wrap-around occurs whenever the dimensions of the object exceed the defined field-of-view (FOV). It is visible as a piece of the head being folded over on the opposite extreme of the image. We exclude subjects based on the observation of a wrap-around, only if the folded region contains or overlaps the cortex. In the MRIQC visual report, the wrap-around can be spotted on the BOLD average, on the standard deviation map and on the background noise visualization. However, we found that the background noise visualization is the most clear to assess whether the folded region overlaps the brain. Note that increasing your screen brightness helps when looking for both aliasing ghosts and wrap-around overlapping the brain, as low brightness makes the artifacts harder to see.

1. **Assessment of time-series with the carpet plot (E)**

    The carpet plot is a tool to visualize changes in voxel intensity throughout an fMRI scan. It works by plotting voxel time-series in close spatial proximity so that the eye notes temporal coincidence (Power 2017). Both MRIQC and fMRIPrep generate carpet plots segmented in relevant regions. One particular innovation of these carpet plots is that they contain a “crown” area corresponding to voxels located on a closed-band around the brain’s outer edge. As those voxels are outside the brain, we do not expect signal there, meaning that if some signal is observed, we can interpret it as artifactual. Therefore, a strongly structured crown region in the carpet plot is a sign that artifacts are compromising the fMRI scan (Provins, Markiewicz, et al. 2022). For example, motion peaks are generally paired with prolonged dark deflections derived from spin-history effects (criterion EA). Periodic modulations on the carpet plot are indicative of regular, slow motion, e.g., caused by respiration, which may also compromise the signal of interest (criterion EB). Furthermore, coil failures may be identifiable as a sudden change in overall signal intensity on the carpet plot and generally sustained through the end of the scan (criterion EC). In addition, sorting the rows (i.e., the time-series) of each segment of the carpet plot such that voxels with similar BOLD dynamics appear close to one another reveals non-global structure in the signal, that is obscured when voxels are ordered randomly (Aquino et al. 2020). Thus, strongly polarized structure in the carpet plot also suggests artifact influence (criterion ED). Finding clear temporal patterns that are similar in gray matter areas and simultaneously in regions of no interest (for instance, cerebrospinal fluid or the crown) indicates the presence of artifacts, typically derived from head motion. If the planned analysis specifies noise regression techniques based on information picked up from these regions of no interest (which is standard and recommended, (Ciric et al. 2017)), the risk of removing signals with neural origin is then high, and affected scans should be excluded.

1. **Artifacts detected with independent components analysis (F)**

    MRIQC was run with the --ica argument, which generates an independent component decomposition using FSL MELODIC (version 5.0.11; Beckmann and Smith 2004). Such techniques have been thoroughly described elsewhere (Griffanti et al. 2017). Components are easily screened with the specific visualization “ICA components” in the corresponding BOLD report, and each component is mapped on a glass brain with an indication of their frequency spectrum and their corresponding weight over time. One recurring artifactual family of components emerges when motion interacts with interleaved acquisition giving rise to the so-called spin-history effects. The spin-history effects appear as parallel stripes covering the whole brain in one direction and are a consequence of the repetition time not being much larger than the T1 relaxation time in typical fMRI designs. This implies that the spins will not relax back completely by the time the next acquisition starts (Cusack 2006). In addition, specific movements (e.g., rotation around one imaging axis, such as nodding) will exacerbate spin-history effects as slices will cut through the brain at different locations between consecutive BOLD time points. These two considerations combined mean that motion will produce spins with different excitation history and thus the signal intensity will be different. Components showcasing parallel stripes concurring with slices in extreme poles of the brain, or even across the whole brain are likely to capture these effects.

1. **Hyperintensity of single slices (G)**

    Above the carpet plot, both MRIQC and fMRIPrep represent several time-series to support the interpretation of the carpet. In particular, the slice-wise z-standardized signal average is useful for detecting sudden “spikes” in average intensity of single slices of BOLD scans. When paired with the motion traces, it is possible to determine whether these spikes are caused by motion or by possible problems with the scanner (e.g., white-pixel noise). Spikes caused by motion typically affect several or all slices, while spikes caused by white-pixel noise affect only one slice and are generally more acute. White-pixel noise is generally caused by some small pieces of metal in the scan room or a loose screw on the scanner that accumulates energy and then discharges randomly. This creates broad-band RF noise at some point during the signal read-out, leading to one spot in k-space with an abnormally high intensity. In the image domain, it manifests as an abrupt signal intensity change in one slice at one time-point. The problem is particularly acute for EPI scans because of all the gradient blipping during the read-out. For resting-state data, we discard BOLD scans containing these spikes regardless of their physical origin (motion vs. white-pixel noise), because correlation analyses are likely biased by such peaks. Conversely, task data analyses are typically more robust to this particular artifact, therefore the presence of only one or more relatively small spikes leads to the scan being flagged for careful inspection after the preprocessing.

1. **Vertical strikes in the sagittal plane of the standard deviation map (H)**

    The sagittal view of the standard deviation map might show vertical strike patterns that extend hyperintensities through the whole sagittal plane. We exclude all images showcasing these patterns. Although we did not find an explanation of the mechanism behind this artifact, email conversations dating from 2017 seemed to point at an interaction between physiology and environmental issues in the scanning room that may affect the receiver coils.

1. **Data formatting issues (I)**

    As part of the NIfTI format (R.W. Cox et al. 2004), the file header contains metadata storing several relevant parameters, of which the orientation information is critical for the interpretability of the data. The orientation parameters indicate how the data matrix is stored on disk and enable visualizing rows and slices at the correct locations (Glen et al. 2020). However, mistakes may occur while recording information at the scanner, while converting DICOM to NIFTI format, or during a subsequent processing step. Such mistakes result in the brain image not being correctly visualized and preprocessed, with axes either being flipped (e.g., the anterior part of the brain is labeled as posterior) or switched (e.g., axial slices are interpreted as coronal ones). These issues may render the dataset unusable, e.g., if the orientation information describing whether the data array has been recorded from left to right or right to left is lost.

**Criteria for flagging unprocessed T1w data based on the individual MRIQC visual report**

Given our planned analysis, the T1w image will be used solely to guide the spatial alignment to the standard MNI152NLin2009cAsym template. In addition, surface reconstructions from the T1w image will guide the co-registration of structural and functional (BOLD) images in fMRIPrep. Since the latter preprocessing steps are relatively robust to structural images with mild artifacts, we do not impose exclusion criterion on the unprocessed T1w images. However, we annotate subjects with visible artifacts in the T1w images in order to ensure rigorous scrutinizing of spatial normalization and surface reconstruction outputs from fMRIPrep (if both modalities passed the first QC checkpoint with MRIQC). The explanation and the description of the flagging criteria 1 to 7 are the same as their counterpart in the previous section. 

Summary
1. Artifactual structures in the background
1. Susceptibility distortion artifacts
1. Aliasing ghosts
1. Wrap-around that overlaps with the brain 
1. Data formatting issues
1. Motion-related and Gibbs ringing
1. Extreme intensity non-uniformity
1. Eye spillover

Details

1. **Motion-related and Gibbs ringing (O)** 

    Large head motion during the acquisition of T1w images often expresses itself with the appearance of concentric ripples throughout the scan. In the most subtle cases, motion-related ripples look similar to the fine lines generated by Gibbs ringing. The latter emerges as a consequence of the truncation of the Fourier series approximation and appears as multiple fine lines immediately adjacent and parallel to high-contrast interfaces. While Gibbs ringing is limited to the adjacency of sharp steps in intensity at tissue interfaces, the ripples caused by motion generally span up to the whole brain, and are primarily visible in the sagittal view of MRIQC’s mosaic views.

1. **Intensity non-uniformity (P)**

    Intensity non-uniformity is characterized by a smooth variation (low spatial frequency) of intensity throughout the brain, caused by the stronger signal sensed in the proximity of coils. It is noticeable on the zoomed-in view on the T1w image. Furthermore, intensity non-uniformity can be a problem for automated processing methods that assume a type of tissue (e.g., white matter (WM)) is represented by voxels of similar intensities across the whole brain. An extreme intensity non-uniformity can also be the sign of a coil failure.

1. **Eye spillover (Q)**

    Eye movements may trigger the leakage of the signal from the eyes through the imaging axis with the lowest bandwidth (i.e., acquired faster) potentially overlapping signal from brain tissue. On data preserving facial features the streak of signal is visible in the background at the levels of the eyes. However, because all the data in this study are openly shared after defacing (for privacy protection reasons), the signal around the face has been zeroed, we thus expect this leakage to not be visible (Provins, Alemán-Gómez, et al. 2022). A strong signal leakage can however be noticeable on the zoomed-in view of the T1w image (see Figure S10G for an example of the latter case).

**Exclusion criteria on minimally pre-processed data based on the fMRIPrep visual report**

Summary
1. Failure in normalization to MNI space
1. Inaccurate brain mask
1. Residual susceptibility distortion
1. Error in brain tissue segmentation of T1w images
1. Surface reconstruction problem
1. Co-registration problem
1. Regions identified for the extraction of nuisance regressors potentially cover neural signal sources

Details
1. **Failure in normalization to MNI space (R)**

    Because the final conclusions of the hypothetical analysis are based on data normalized to a standard template, it is crucial that the normalization is successful. The fMRIPrep report contains a widget to assess the quality of the normalization to MNI space. The widget flickers between the MNI template and the individual’s T1w image normalized to that template. To verify successful normalization, we assessed the correct alignment of the following structures (in order of importance) : 1. ventricles, 2. subcortical regions, 3. corpus callosum, 4. cerebellum and, 5. cortical gray matter (GM). A misalignment of the ventricles, the subcortical regions, or the corpus callosum led to immediate exclusion, however we were more lenient with the misalignment of cortical GM because volumetric (image) registration may not resolve substantial inter-individual differences (e.g., a sulcus missing in an individual’s brain but typically present in the population of the template). Any extreme stretching or distortion of the T1w image also indicates a failed normalization.

1. **Inaccurate brain mask (S)**

    The brain mask computed from the T1w image is shown in the “brain mask and brain tissue segmentation of the T1w” panel under the anatomical section of the fMRIPrep visual report. The latter should follow closely the contour of the brain. An inaccurate brain mask presents “bumps” surrounding high intensity areas of signal outside of the cortex (e.g., a mask including patches of the skull), and/or holes surrounding signal drop-out regions. Having an accurate brain mask makes the downstream preprocessing of an fMRI scan faster (excluding voxels of non-interest) and more accurate (less bias from voxels of non-interest), that is why it is important to discard subjects for which the brain mask is not well defined. Note that the brain mask that is plotted in the “brain mask and (anatomical/temporal) CompCor ROIs” panel under the functional section is not identical to the brain mask mentioned in this paragraph, as it is computed from the BOLD image. The brain mask extracted from the BOLD image is used mostly for confounds extraction, thus it does not follow the same quality criteria.

1. **Residual susceptibility distortion (T)**

    For cases that were not excluded following criterion B, susceptibility distortions were evaluated with the fMRIPrep report after preprocessing.  Any observation of susceptibility distortion artifacts led to the exclusion of the scan.

1. **Error in brain tissue segmentation of T1w images (U)**

    The panel “brain mask and brain tissue segmentation of the T1w” under the anatomical section of the fMRIPrep report shows contours delineating brain tissue segmentations overlaid on the T1w image. To confirm the good quality of the segmentation, we first verified that the pink contour accurately outlined the ventricles, whereas the blue contour followed the boundary between GM and WM. The first exclusion criteria was thus the inclusion of tissues other than the tissue of interest in the contour delineations. T1w scans showcasing low signal-to-noise ratio because of the presence of thermal noise, will present scattered misclassified voxels within piecewise-smooth regions (generally more identifiable in the WM and inside the ventricles). These scans are excluded except for images where these voxels are only present at subcortical structures (e.g., thalamus) or nearby tissue boundaries. In the latter case, the misclassification is a result of partial volume effects (i.e., indeed such voxels contain varying fractions of two or more tissues).

1. **Surface reconstruction problem (V)**

    The WM surface (blue outline) and the pial surface (red outline) reconstructed with FreeSurfer (version 7.0.1, (Fischl 2012)) are visualized overlaid on the participant’s T1w image, in the panel dedicated to surface reconstruction visualization under the anatomical section of the fMRIPrep report. Since the cerebellum and the brainstem are excluded from the surface reconstruction; the outlines will not include these areas. QC assessment of FreeSurfer outcomes is comprehensively covered elsewhere (e.g., White et al. 2018; Klapwijk et al. 2019), and fMRI studies using vertex-wise (surface) analyses should rigorously assess these surfaces. In this protocol, we only excludedata when the reconstructed surfaces are extremely inaccurate, which typically only happens in the presence of artifacts easily captured previously by MRIQC (section "Criteria for flagging unprocessed T1w data based on the individual MRIQC visual report"). 

1. **Co-registration problem (W)**

    The fMRIPrep report contains a widget to assess the accuracy of the alignment of BOLD runs into the individual’s anatomical reference (co-registration). The widget flickers between the reference T1w image and the BOLD average co-registered onto it. Extracted brain surfaces’ contours are represented as further anatomical cues. Here, we checked the alignment of image intensity edges and the anatomical landmarks (e.g the ventricles and the corpus callosum) between the BOLD and the T1w images.

1. **Regions identified for the extraction of nuisance regressors potentially cover neural signal sources (X)**

    fMRIPrep calculates CompCor (Behzadi et al. 2007) nuisance regression time series for the removal of physiological and head motion artifacts from BOLD scans. Two families of CompCor methodologies are provided within the outputs: temporal CompCor (tCompCor) uses voxels presenting the highest temporal variability, and anatomical CompCor (aCompCor) extracts signal from regions of no interest (e.g., a conservative mask including core areas of the ventricles and the WM). fMRIPrep provides a panel to assess the adequacy of these regions from which CompCor will extract regressors (“brain mask and anatomical/temporal CompCor ROIs”). In addition to the masks corresponding to CompCor, the “crown” mask can also be assessed in this visualization. If the study plan states the use of CompCor or brain-edge regressors, it is critical to exclude BOLD runs where any of these masks substantially overlap regions of interest.

**References**

* Aquino, Kevin M., Ben D. Fulcher, Linden Parkes, Kristina Sabaroedin, and Alex Fornito. 2020. “Identifying and Removing Widespread Signal Deflections from FMRI Data: Rethinking the Global Signal Regression Problem.” NeuroImage 212 (May): 116614. <https://doi.org/10.1016/j.neuroimage.2020.116614>.

* Behzadi, Yashar, Khaled Restom, Joy Liau, and Thomas T. Liu. 2007. “A Component Based Noise Correction Method (CompCor) for BOLD and Perfusion Based FMRI.” NeuroImage 37 (1): 90–101. <https://doi.org/10.1016/j.neuroimage.2007.04.042>.

* Ciric, Rastko, Daniel H. Wolf, Jonathan D. Power, David R. Roalf, Graham L. Baum, Kosha Ruparel, Russell T. Shinohara, et al. 2017. “Benchmarking of Participant-Level Confound Regression Strategies for the Control of Motion Artifact in Studies of Functional Connectivity.” NeuroImage, Cleaning up the fMRI time series: Mitigating noise with advanced acquisition and correction strategies, 154: 174–87. <https://doi.org/10.1016/j.neuroimage.2017.03.020>.

* Cox, R.W., J. Ashbruner, H. Breman, K. Fissell, C. Haselgrove, and C. J. Holmes. 2004. “A (Sort of) New Image Data Format Standard: NIfTI-1.” In the 10th Annual Meeting of the Organization for Human Brain Mapping in Budapest.

* Cusack, Rhodri. 2006. “CommonArtefacts - MRC CBU Imaging Wiki.” March 2006. <https://imaging.mrc-cbu.cam.ac.uk/imaging/CommonArtefacts>.

* Esteban, Oscar, Azeez Adebimpe, Christopher J. Markiewicz, Mathias Goncalves, Ross W. Blair, Matthew Cieslak, Mikaël Naveau, et al. 2021. “The Bermuda Triangle of D- and f-MRI Sailors - Software for Susceptibility Distortions (SDCFlows).” OSF Preprints. <https://doi.org/10.31219/osf.io/gy8nt>.

* Fischl, Bruce. 2012. “FreeSurfer.” NeuroImage 62 (2): 774–81. https://doi.org/10.1016/j.neuroimage.2012.01.021.

* Glen, Daniel R., Paul A. Taylor, Bradley R. Buchsbaum, Robert W. Cox, and Richard C. Reynolds. 2020. “Beware (Surprisingly Common) Left-Right Flips in Your MRI Data: An Efficient and Robust Method to Check MRI Dataset Consistency Using AFNI.” Frontiers in Neuroinformatics 14. <https://www.frontiersin.org/articles/10.3389/fninf.2020.00018>.

* Hutton, Chloe, Andreas Bork, Oliver Josephs, Ralf Deichmann, John Ashburner, and Robert Turner. 2002. “Image Distortion Correction in FMRI: A Quantitative Evaluation.” NeuroImage 16 (1): 217–40. <https://doi.org/10.1006/nimg.2001.1054>.

* Klapwijk, Eduard T., Ferdi van de Kamp, Mara van der Meulen, Sabine Peters, and Lara M. Wierenga. 2019. “Qoala-T: A Supervised-Learning Tool for Quality Control of FreeSurfer Segmented MRI Data.” NeuroImage 189 (April): 116–29. <https://doi.org/10.1016/j.neuroimage.2019.01.014>.

* Power, Jonathan D. 2017. “A Simple but Useful Way to Assess FMRI Scan Qualities.” NeuroImage, Cleaning up the fMRI time series: Mitigating noise with advanced acquisition and correction strategies, 154 (July): 150–58. <https://doi.org/10.1016/j.neuroimage.2016.08.009>.

* Provins, Céline, Yasser Alemán-Gómez, Martine Cleusix, Raoul Jenni, Jonas Richiardi, Patric Hagmann, and Oscar Esteban. 2022. “Defacing Biases Manual and Automated Quality Assessments of Structural MRI with MRIQC.” OSF Preprints. <https://doi.org/10.31219/osf.io/8mcyz>.

* Provins, Céline, Christopher J. Markiewicz, Rastko Ciric, Mathias Goncalves, César Caballero-Gaudes, Russell Poldrack, Patric Hagmann, and Oscar Esteban. 2022. “Quality Control and Nuisance Regression of FMRI, Looking out Where Signal Should Not Be Found.” OSF Preprints. <https://doi.org/10.31219/osf.io/hz52v>.

* White, Tonya, Philip R. Jansen, Ryan L. Muetzel, Gustavo Sudre, Hanan El Marroun, Henning Tiemeier, Anqi Qiu, Philip Shaw, Andrew M. Michael, and Frank C. Verhulst. 2018. “Automated Quality Assessment of Structural Magnetic Resonance Images in Children: Comparison with Visual Inspection and Surface-Based Reconstruction.” Human Brain Mapping 39 (3): 1218–31. <https://doi.org/10.1002/hbm.23911>.
