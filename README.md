# SeaDAS
straight-forward, step by step guide, to using NASA SeaDAS 8.2 to process Landsat-8 and Sentinel-2 data. No prior experience needed.


**Processing Level-1 (Collection-1) Landsat-8 and Sentinel-2 Imagery in NASA SeaDAS**
By Sarah Lang (URI-GSO) and Olivia Cronin-Golomb (UVA)

NASA SeaDAS 8.2 set up
1.	Download SeaDAS installer here: https://seadas.gsfc.nasa.gov/downloads/
Execute this shell script on command line (Mac: terminal)

Here’s how: 

_cd /Users/username/Documents/  #location of the installer script
chmod 777 ‘seadas_8.2.0_mac_installer.sh’
./seadas_8.2.0_mac_installer.sh_

2.	The SeaDAS installer will pop up. Go through the steps. Make sure you create a new folder as your directory for SeaDAS (I called mine Seadas_8.2 in Documents). The download contains many folders- you want them all in the same place.
3.	On the SeaDAS GUI, navigate to the toolbar. Under SeaDAS-OCSSW, select Configure OCSSW location. Make sure “local” is selected, and select the folder associated with ocssw under your seadas folder (eg. …/Seadas_8.2/ocssw).
4.	SeaDAS-OCSSW  > Install/Update OC processors
a.	Select sensors of interest (OLI for Landsat-8, you will install Sentinel-2 later on the command line)
b.	Hit Apply, then Run

**Processing set up**

_cd /Users/username/Documents/Seadas_8.2/ocssw

/Users/username/Documents/Seadas_8.2/bin/gpt #run gpt command
export OCSSWROOT=/Users/username/Documents/Seadas_8.2/ocssw/
source OCSSW_bash.env; ./bin/install_ocssw -t V2022.0 --msis2a --msis2b --src –oli #msi is sentinel-2 sensor, oli is landsat-8_

**General notes:**
•	Please note: the following processing code removes the landmask in SeaDAS and implements Sentinel-2 gains. Subsetting the region (as done here) may increase the accuracy of atmospheric correction, and it will decrease processing time. Strongly recommended.
•	We set up an “image” folder in the ocssw folder, which contains subfolders corresponding to the sensor and year.
•	Code won’t work if there are spaces in the pathnames. Please revise.

**Sentinel-2A Processing Code**

cd /Users/username/Documents/Seadas_8.2/ocssw/images/S2A/2021 
 
_for f in *.SAFE; do f2=${f%.*}.manifest.safe.L2; l2gen ifile=$f/manifest.safe ofile=/Users/ username /Documents/Seadas_8.2/ocssw/images/S2A/2021/$f2 north=37.729198 south=37.084875 east=-75.595402 west=-76.045972 maskland=0 land=/Users/ username /Documents/Seadas_8.2/ocssw/share/common/landmask_null.dat vcal_opt=1 gain=[0.9841,0.988,1.0079,1.00841,1.0091,1.0201,0.9801,1.0,1.0,1.0,1.0,1.0] ; done _

**Sentinel-2B Processing Code**

_cd /Users/username/Documents/Seadas_8.2/ocssw/images/S2B /2021/ 
 
for f in *.SAFE; do f2=${f%.*}.manifest.safe.L2; l2gen ifile=$f/manifest.safe ofile=/Users/ username /Documents/Seadas_8.2/ocssw/images/S2B /2021/$f2 north=37.729198 south=37.084875 east=-75.595402 west=-76.045972 maskland=0 land=/Users/username/Documents/Seadas_8.2/ocssw/share/common/landmask_null.dat vcal_opt=1 gain=[1.0027,0.9996,1.0143,1.0054,1.0334,1.0406,0.9808,1.0,1.0,1.0,1.0,1.0] ; done _

**Landsat-8 Processing Code**

_cd /Users/username/Documents/Seadas_8.2/ocssw/images/L8 /2021/ 
 
for f in *_MTL.txt; do f2=${f%.*}.L2_LAC_OC; l2gen ifile=$f ofile=/Users/username /Documents/Seadas_8.2/ocssw/images/L8 /2021/$f2 north=37.729198 south=37.084875 east=-75.595402 west=-76.045972 land=/Users/username/Documents/Seadas_8.2/ocssw/share/common/landmask_null.dat maskland=0; done _






















![image](https://user-images.githubusercontent.com/83712030/162807536-2c33e240-958a-434c-86af-dc540ec17438.png)
