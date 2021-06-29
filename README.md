Reporter: Kornpob Bhirombhakdi (kbhirombhakdi@stsci.edu)

# Contents:
- Files (Proposal ID 15974)
- Astrometry of AT2018COW on images taken on 20200529
- Correlation between Halpha region and AT2018COW

# Files (Proposal ID 15974)
- F336W: ie4502z6q, ie4502z8q, ie4502zaq
- F225W: ie4502z5q, ie4502z7q, ie4502z9q
- F665N: ie4501yyq, ie4501z0q, ie4501z2q
- F657N: ie4501yzq, ie4501z1q, ie4501z3q
- F555W: ie4503zcq, ie4503zfq, ie4503zjq
- F814W: ie4503zdq, ie4503zhq, ie4503zlq

These files were drizzled (see 02_drizzle.ipynb for code), and output drc files were kept in /ASSETS/DRC_FXXXX/. Both EXP and IVM were created for different 'final_wht_type'.

For other images, we used F336W drc image as the 'final_refimage'.

# Astrometry of AT2018COW on images taken on 20200529

- Apply F336W drc image as the 'final_refimage' during drizzle.

- Use additional files from proposal ID 15600 in:
  - F336W: idu301cnq, idu301crq
  - F225W: idu301cpq, idu301ctq
  
  These were taken on 20180806, when the object is still bright. Drizzle this dataset using F336W drc image on 20200529 as the 'final_refimage'. The drc output files were kept in /ASSETS/DRC_FXXXX/ as well.

- For F225W, we located AT2018COW by using image subtraction. See 03_astrometry.ipynb for code. Output files were kept in /ASSETS/SHIFT/ including:
  - F225W_20180806_shifted_to_20200529_drc.fits = Best of F225W on 20180806 aligned to 20200529
  - F225W_20180806_sub_drz.fits = subtraction of the best aligned images
  - F225W_20180806_to_20200529.txt = a text file recording xy_shift value.
  
- From F225W_20180806_sub_drz.fits, we found the centroid of AT2018COW. The file /ASSETS/REGION/F225W_20180806_AT2018cow_xy.reg is the DS9 region file for initial xy pixel of the object. Output files include:
  - /ASSETS/REGION/AT2018cow_F225W_20200529_refimage_20200529_xy.dat = record of the centroid
  - /ASSETS/IMAGES/AT2018COW_F225W_20200529.pdf = figure of the centroid on F225W 20200529.
  
  We note that the centroid is on a center of a small bright region seen in F225W 20200529.
  
- For F336W, we performed similarly as did with F225W. Output files were produced similarly as well.

- Besides F336W, for other filters (including F225W, F665N, F657N, F555W, F814W), we computed xy_shift between drc images by aligning multiple objects in the FoVs. See 03_astrometry.ipynb for code. Outputs include:
  - /ASSETS/DRC_FXXXX/sources_FXXXX_20200529.csv = source catalogue
  - /ASSETS/DRC_FXXXX/offset_FXXXX_20200529_to_F336W_20200529.txt = record of the xy_shift value, and metadata. Note that every filter excepts F336W has this file.
  
- For F225W, we performed a quality check between two different astrometric methods, i.e., locating AT2018COW through image subtraction, and aligning the FoVs. See 03_astrometry.ipynb for the code. The discrepancy between two methods is dx = -0.24 and dy = -0.04, implying good quality of astrometry through aligning FoVs as through image subtraction. Therefore, we can use the centroid found in F336W with the xy_shift from image alignment to locate AT2018COW in other filters.

# Correlation between Halpha region and AT2018COW

- We performed subtraction between F665N (as continuum + Halpha) and F657N (as continuum). First, we checked that both images are well aligned (i.e., dx = 0.09 and dy = -0.06; see 04_Halpha.ipynb for code). Then, we scaled F657N with a factor K to makes its equivalent to the continuum as if it was observed in F665N. K was computed by using the filter properties, and its formula is presented with the code in 04_Halpha.ipynb. Additionally, we also created images of errors (including Poisson noise and readnoise) and SNRs. Outputs were kept in /ASSETS/Halpha/ which includes:
  - F665N_20200529_sub_F657N_ScaleFormula_drc.fits = subtracted image
  - F665N_20200529_sub_F657N_ErrTotal_drc.fits = error image
  - F665N_20200529_sub_F657N_SNRTotal_drc.fits = SNR image
  - /ASSETS/IMAGES/AT2018COW_Halpha.pdf = a figure showing the subtracted image zoomed at the AT2018COW's location.
  
  Note that we see very faint (SNR < ~2-3) residuals left in the subtracted image at the object's location, implying the correlation between Halpha region and the object.
  
- We performed source detection and created a segmentation using a Gaussian filter with routine from astropy. See 04_Halpha.ipynb for the code. We chose the best case to be presented here as using nsigma = 2 (above sky). Outputs include:
  - /ASSETS/Halpha/halpha_segmentation_nsigma2_drc.fits = segmentation image
  - /ASSETS/IMAGES/Halpha_segmentation.pdf = figure zoomed at the object's location
  
  Note, AT2018COW located on a non-detection pixel, but the adjacent pixel (to its right) was a detection.


```python

```
