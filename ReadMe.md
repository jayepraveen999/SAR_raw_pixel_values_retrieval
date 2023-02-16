`Datasets:`


The following are the data products I have used for MT-DInSAR.  


S No	Filename
1	S1A_IW_SLC__1SDV_20180505T052723_20180505T052750_021765_0258EB_7AA2.SAFE
2	S1A_IW_SLC__1SDV_20180517T052723_20180517T052750_021940_025E79_F818.SAFE
3	S1A_IW_SLC__1SDV_20180529T052724_20180529T052751_022115_026419_F53B.SAFE
4	S1A_IW_SLC__1SDV_20180610T052725_20180610T052752_022290_026990_BEE7.SAFE
5	S1A_IW_SLC__1SDV_20180622T052725_20180622T052752_022465_026ED9_C660.SAFE
6	S1A_IW_SLC__1SDV_20180704T052726_20180704T052753_022640_0273F3_DAB6.SAFE
7	S1A_IW_SLC__1SDV_20180716T052727_20180716T052754_022815_02793C_BE0E.SAFE
8	S1A_IW_SLC__1SDV_20180728T052727_20180728T052754_022990_027EC5_4DAE.SAFE
9	S1A_IW_SLC__1SDV_20180809T052728_20180809T052755_023165_02843F_1B64.SAFE

The table lists the filenames of the SAR data which can be downloaded via API or the Copernicus platform.\
Please let me know if you would like to have the displacement maps, I can share them with you maybe via some cloud platform.

`Code files:`

Attached are the two notebooks that I have developed during this project. 

1. Remote_Sensing_Seminar_SAR_script.ipynb: This script is divided into three blocks. 
  `script to download Sentinel 1 SAR data using Sentinelsat API`: Self-explanatory with comments included \
  
  `a function to convert SAR data to geocoded SAR data`: Even though we want to retrieve the raw pixel values at particular lat lon values, we need to geocode the product. To geocode SAR data we need to perform tops split, apply orbit file, deburst and terrain correction. All these are have been implemented using snappy python library which needs SNAP software to be installed on the local machine. \
  
  `a function to retrieve the intensity and phase values`: Once the geocoded product from the above step is created, we open this product using rasterio python library. Intensity, Complex i, and complex q (Phase) for a given lat, lon are returned in a pandas dataframe. Firstly the pandas df is initialized with no rows and when this is function is called multiple times, new records are appended to this df \
  
2. plots_videos_script.ipynb: This script is used to generate videos from a directory of images, add text to images, and create the average displacement plot for the MT-DInSAR data.

`The functions are tested with multiple files and successfully resulted in pixel values for a particular (lat ,lon)`

`More comments on the packages`: I came across packages like pyroSAR, Eoreader, Sarpy, xarray-sentinels and tried to work with our data. However, packages like Eoreader are limited to only GRD datasets. The other packages could just read the image but the major step which is to retrieve the pixel info at given lat lon cannot be performed without geocoding the product. 

Currently, Snappy (python API for SNAP) offers this processing via function calls but requires SNAP software to be installed and limited to specific python versions (2.7,3.4,3.5,3.6). I have used python version 3.6 to perform geocoding. 


