# Hyperlapse for GoPro Hero 5 Session
Tutorial on how to modify Microsoft Hyperlapse so it can work with GoPro Hero 5 Session. It can also be adapted to other cameras, provided you can calculate their calibration parameters, as described in this article.

Found any issues or need help adding a custom camera? Just open an issue or send me a message and I'll try to help you!

# Disclaimer
Doing this modification probably goes against Microsoft licensing terms. However, I'm not distributing any binary or resource owned by Microsoft, only basic information on how to improve the list of supported cameras. This software that hasn't been updated in at least 4 years, [and their respective cloud services have been discontinued](https://azure.microsoft.com/en-us/blog/announcing-hyperlapse-for-azure-media-services/). There are even some other repositories in Github that host decompiled copies of the application code (and they have been up for many years!).

# Using provided calibration files (for GoPro Hero 5 Session)

- Make a backup of the `Microsoft.Research.Hyperlapse.dll` found in the installation folder (typically `C:\Program Files\Microsoft Hyperlapse\`).
- Download [DnSpy](https://github.com/dnSpy/dnSpy).
- Open the `Microsoft.Research.Hyperlapse.dll` file and go to the `Resources` section.
- Right click on `Microsoft.Research.Hyperlapse.Calibrations.GoPro_HERO4_Session_extended.txt` and delete it.
- Right click on the `Resources` section and select `Create File Resource`.
- Choose the calibration file that you want to install. Files are provided in the `calibrations/cameraName_cameraMode` folder.
- Save the DLL to a temporary folder, using `File` then `Save module`.
- Copy the file from the temporary folder to the installation folder (the software can't be running, or it will fail).
- Open the software, use it normally, the new model and mode should appear within the list.

**2.7K Linear mode has some issues, as the toolkit is optimized for fish-eye cameras and it fails to converge for cameras without much distortion. The stabilization works but it has some blurring effect near the center of the image. I'm trying to find a workaround that preserves image quality.**

# Creating your own calibration

- Requires Matlab (I'm using R2015a).
- Download [OCamCalib](https://sites.google.com/site/scarabotix/ocamcalib-toolbox).
- Print the calibration pattern (100% scale), attach it to a rigid board.
- Record a video with your desired camera configuration, showing the pattern in different positions (trying to keep the whole pattern in view, not cropping it). Use lots of light to avoid motion blur, and make sure the pattern is seen at least once in each corner of the camera.
- Extract 6 to 10 frames from the video, showing the pattern in different positions.
- Copy the images to the OCamCalib folder and follow the calibration steps, then export the parameters.
- Create a new calibration file based on one of the given in the `calibrations/template` folder. Make sure to replace all required parameters between `<>` with the parameters from the step before.
- Use the steps from the previous list to add the new calibration file to the Hyperlapse software.
