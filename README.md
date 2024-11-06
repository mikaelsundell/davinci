# Photographic DCTLs #

[![License](https://img.shields.io/badge/license-BSD%203--Clause-blue.svg?style=flat-square)](https://github.com/mikaelsundell/icloud-snapshot/blob/master/license.md)

Table of Contents
=================

- [DCTL](#dctl)
- [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Installation and utils](#installation-and-utils)
- [DCTL reference](#dctlreference)
  - [Cineon color processing](#cineon-color-processing)
    - [MS-Cineon-Exposure.dctl](#ms-cineon-exposuredctl)
    - [MS-Cineon-Invert.dctl](#ms-cineon-invertdctl)
      - [Cineon inversion](#cineon-inversion)
      - [ACES scene-linear and calibration curves](#aces-scene-linear-and-calibration-curves)
    - [MS-Cineon-Exposure.dctl](#ms-cineon-exposuredctl-1)
    - [MS-Cineon-Transform.dctl](#ms-cineon-transformdctl)
    - [MS-Cineon-Transform.dctl](#ms-cineon-transformdctl-1)
  - [Gen5 color processing](#gen5-color-processing)
    - [MS-Gen5-Transform.dctl](#ms-gen5-transformdctl)
  - [LogC3 color processing](#logc3-color-processing)
    - [MS-LogC3-Print.dctl](#ms-logc3-printdctl)
    - [MS-LogC3-Exposure.dctl](#ms-logc3-exposuredctl)
    - [MS-LogC3-Temperature.dctl](#ms-logc3-temperaturedctl)
    - [MS-LogC3-Transform.dctl](#ms-logc3-transformdctl)
  - [Utility DCTLs](#utility-dctls)
    - [MS-Grade.dctl](#ms-gradedctl)
    - [MS-Stripify.dctl](#ms-stripifydctl)
    - [MS-Saturation.dctl](#ms-saturationdctl)
  - [DCTLs from other projects](#dctls-from-other-projects)
    - [Printer Lights.dctl](#printer-lightsdctl)
    - [TetraInterp.dctl](#tetrainterpdctl)
    - [TetraInterpHSV.dctl](#tetrainterphsvdctl)
  - [Reference charts](#reference-charts)
  - [References](#references)
  - [Web Resources](#web-resources)

Introduction
---------

<img src="resources/dctl.jpg" width="100%" style="padding-bottom: 20px;" />

This is a growing collection of DCTLs (DaVinci Color Transform Language) created to understand workflows with ARRI LogC3, Gen5 and Cineon in DaVinci Resolve. These DCTLs take a photographic approach to color correction and grading from log and film negatives, focusing on look adjustments and traditional print techniques rather than rigid technical processes. The project is continually updated to implement new insights and techniques.
  
Installation and utils
---------

To use these tools into your DaVinci Resolve setup, begin by cloning the git repository or download the release package, which contains the DCTLs and headers.

Run `python(.exe) run.py install` in your terminal to copy the `*.dctl` and `*.h` files to the DaVinci Resolve LUT DCTL folder, ensuring they're accessible within your Resolve environment. The files can also be manually copied to `/Library/Application Support/Blackmagic Design/DaVinci Resolve/LUT/DCTL` on Mac and `C:\ProgramData\Blackmagic Design\DaVinci Resolve\Support\LUT\DCTL`on Windows.

For added convenience, the run.py script is provided, enabling easy access to various resources:

### To open the DCTL readme documentation, use:

```shell
./run.py readme
````

**For exploring DCTL examples, execute:**

```shell
./run.py examples
````

**To access the DaVinci Resolve log file and initiate a trace, input:**

```shell
./run.py install
````

**To install *.dctl and *.h into DCTL directory:**

```shell
./run.py log
````

**To make a snapshot of hte DaVinvi Resolve DCTL folder, input:**

```shell
./run.py snapshot
````

### Quick install for Windows users

```shell
./install.bat
````

### DCTL Compatibility

All DCTLs are tested and confirmed to work with Metal, CUDA, and OpenCL on both Mac and Windows platforms.

# DCTL reference

## Cineon color processing

### MS-Cineon-Exposure.dctl

![MS-Cineon-Exposure figure](resources/MS-Cineon-Exposure.png "MS-Cineon-Exposure.dctl")

Cineon exposure from photographic stops, incorporating a zone based false color to aid in achieving correct exposure levels.

- https://github.com/mikaelsundell/dctl/blob/master/MS-Cineon-Exposure.dctl

### MS-Cineon-Invert.dctl

#### Cineon inversion

![MS-Cineon-Invert.dctl figure](resources/MS-Cineon-Invert.png "MS-Cineon-Invert.dctl")

Cineon negative inversion with precise control over the dmin ratio based inversion process using adjustable parameters such as density, bit depth, offset, and density scale. You can specify dmin base values manually as floating-point numbers (obtained from tools like Pixel Analyzer in Nuke or similar software) or sample them using a rectangular sampler from the border or other dmin base areas.

#### ACES scene-linear and calibration curves

To account for the variations of film stock and the use of ECN-2 chemicals, developer time and temperature, camera and lightbox settings - calibration curves are applied to match ideal cineon code values. In this example, photoscanning was used along with the rawtoaces tool to convert the Camera RAW CR2 file to scene-linear ACES, starting with as much information as possible. However, because the science is not exact, manual tweaking using density scaling and calibration curves is needed depending on the setup.

![MS-Cineon-Invert.dctl figure](resources/MS-LogC3-Invert_calibration.png "MS-Cineon-Invert.dctl")

Figure: Color calibration curves and macbeth charts at different exposures for adjustments.

- https://github.com/mikaelsundell/dctl/blob/master/MS-Cineon-Invert.dctl
- https://github.com/AcademySoftwareFoundation/rawtoaces

### MS-Cineon-Exposure.dctl

Cineon exposure from photographic stops, incorporating a zone based false color to aid in achieving correct exposure levels.

- https://github.com/mikaelsundell/dctl/blob/master/MS-Cineon-Exposure.dctl

### MS-Cineon-Transform.dctl

Cineon conversion to and from linear. 

- https://github.com/mikaelsundell/dctl/blob/master/MS-Cineon-Transform.dctl

## Gen5 color processing

### MS-Gen5-Transform.dctl

Gen5 conversion to and from linear. 

- https://github.com/mikaelsundell/dctl/blob/master/MS-Gen5-Transform.dctl

## LogC3 color processing

### MS-LogC3-Print.dctl

![MS-LogC3-Print.dctl figure](resources/MS-LogC3-Print.png "MS-LogC3-Print.dctl")

Made for print emulation, this DCTL applies DaVinci Resolve's built-in film looks to ARRI LogC3 and Cineon footage with adjustable controls for luminosity and color blending.

- https://github.com/mikaelsundell/dctl/blob/master/MS-LogC3-Print.dctl

### MS-LogC3-Exposure.dctl

![MS-LogC3-Exposure.dctl figure](resources/MS-LogC3-Exposure.png "MS-LogC3-Exposure.dctl")

LogC3 exposure from photographic stops, incorporating a zone based false color to aid in achieving correct exposure levels.

- https://github.com/mikaelsundell/dctl/blob/master/MS-LogC3-Exposure.dctl

### MS-LogC3-Temperature.dctl

LogC3 CAT02 color temperature adjustments.

- https://github.com/mikaelsundell/dctl/blob/master/MS-LogC3-Temperature.dctl

### MS-LogC3-Transform.dctl

LogC3 conversion to and from linear. 

- https://github.com/mikaelsundell/dctl/blob/master/MS-LogC3-Transform.dctl

## Utility DCTLs

### MS-Grade.dctl

Grade adjustments, this DCTL is experimental code for lift, gamma, gain and log controls.

- https://github.com/mikaelsundell/dctl/blob/master/MS-Grade.dctl

### MS-Stripify.dctl

Matrix adjustments, this DCTL simplifies the color palette by pushing colors into a warm and cool strip.

- https://github.com/mikaelsundell/dctl/blob/master/MS-Stripify.dctl

### MS-Saturation.dctl

HSV-based adjustments, this DCTL provides a tool for fine-tuning saturation using saturation in HSV.

- https://github.com/mikaelsundell/dctl/blob/master/MS-Saturation.dctl

## DCTLs from other projects

### Printer Lights.dctl

- https://github.com/thatcherfreeman/utility-dctls/blob/main/Utilities/Printer%20Lights.dctl

### TetraInterp.dctl

-  https://github.com/hotgluebanjo/TetraInterp-DCTL/blob/master/TetraInterp.dctl

### TetraInterpHSV.dctl

- https://github.com/hotgluebanjo/TetraInterp-DCTL/blob/master/TetraInterpHSV.dctl

## Reference charts

### Reference charts for testing and verifying DCTLs. Additional formats are available in the Logctool project README:

- https://github.com/mikaelsundell/logctool

### ACES Macbeth 50D 5203 EXR from rawtoaces

![logctool_LogC3_DCI_2K figure](resources/macbeth_50D_5203.png "Macbeth 50D 5203 EXR")

- Download: [macbeth_50D_5203.exr](resources/macbeth_50D_5203.exr)

### ARRI LogC3 stepchart - EXR 2K LogC3 encoding 

![llogctool_LogC3_stepchart_DCI_2K figure](resources/logctool_LogC3_stepchart_DCI_2K.png "ARRI LogC3 10-bit DPX")

- Download: [logctool_LogC3_stepchart_DCI_2K.exr](https://mikaelsundell.s3.eu-west-1.amazonaws.com/github/logctool/logctool_LogC3_stepchart_DCI_2K.exr)

### ARRI LogC3 colorchecker - EXR 2K LogC3 encoding 

![logctool_LogC3_colorchecker_DCI_2K figure](resources/logctool_LogC3_colorchecker_DCI_2K.png "Cineon 10-bit DPX")

- Download: [logctool_LogC3_colorchecker_DCI_2K.exr](https://mikaelsundell.s3.eu-west-1.amazonaws.com/github/logctool/logctool_LogC3_colorchecker_DCI_2K.exr)


References
---------

ARRI Companion to DI
* https://dicomp.arri.de/digital/digital_systems/DIcompanion/index.html
  
Blend modes:
* https://skia.googlesource.com/skia/+/70e432e72745/gm/hsl.cpp

Cineon conversion in RV:
* https://github.com/AcademySoftwareFoundation/OpenRV/blob/main/src/plugins/rv-packages/additional_nodes/LinearToCineonLog.glsl
* https://github.com/AcademySoftwareFoundation/OpenRV/blob/main/src/plugins/rv-packages/additional_nodes/CineonLogToLinear.glsl

Grayscale legacy luma:
* https://en.wikipedia.org/wiki/Grayscale

Tonal curves in Desmos graph calculator:
* https://www.desmos.com/calculator/3zhzwbfrxd

 Web Resources
-------------

* GitHub page:        https://github.com/mikaelsundell/dctl
* Issues              https://github.com/mikaelsundell/dctl/issues
