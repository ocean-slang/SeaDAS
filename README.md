# SeaDAS processing
straight-forward, step by step guide to using NASA SeaDAS 8.2 (on the command line) to process Landsat-8 and Sentinel-2 data. No prior experience needed. written for Mac

Please note: OCSSW (processing components) can only be installed on mac or linux. to use windows, you'll need to use a client/server model: https://seadas.gsfc.nasa.gov/client_server/

By Sarah Lang (URI-GSO) and Olivia Cronin-Golomb (UVA)

for questions, concerns, or feedback, please email slang@uri.edu

**some possible problems and solutions:**
If you run into an error that states that the operation is not permitted, make sure Terminal has full disk access.
Apple Menu > Preferences > Security and Privacy > Privacy > Full Disk Access > Terminal

Error regarding git operation: make sure you have command line developer tools installed

if something is not found... check your path! depending on how you initialized SeaDAS, some components (eg. OCSSW_bash.env) may not be located in same place as mine. change your cd to point to folder where whatever you need is located.

if all else fails, try quitting Terminal and run through the procedure of setting your working directory, executing gpt.command (and possibly installing processors again).

You may receive the following error message if you’ve tried to download the processors previously on your system and the download failed: “Another git process seems to be running in this repository, e.g. an editor opened by 'git commit'. Please make sure all processes are terminated then try again. If it still fails, a git process may have crashed in this repository earlier: remove the file manually to continue.”
one way:
rm -f /Users/username/.cocoapods/repos/master/.git/index.lock
