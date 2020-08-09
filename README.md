# Single Pass Stereo with OpenVR

## What this project is
The focus of this project is to show that Single Pass Stereo is not producing the correct projected image for the right eye when used with a Head Mounted Display (HMD) that is using asymmetric projections for the eyes.

This project is a one file project that implements the [Single Pass Stereo](https://developer.nvidia.com/vrworks/graphics/singlepassstereo) functionality in the [OpenVR (SteamVR)](https://github.com/ValveSoftware/openvr) OpenGL sample.

It is complementary to my posts [Is Single Pass Stereo worth it?](https://iliaskapouranis.com/2020/07/13/is-single-pass-stereo-worth-it/) and [TBP](https://iliaskapouranis.com/).

## Functionality
There are keyboard bindings that allow the user to change on-the-fly how the scene is rendered with three keys:

1. **Key S:** Render the scene using *Single Pass Stereo*
2. **Key D:** Render the scene using the *default* method
3. **Key A:** Render the scene by overlapping *both* methods

When rendering with the *default* method, the scene is rendered exactly as supplied with the SDK as if no changes were done.

When rendering with the *Single Pass Stereo* method, the scene is rendered only with SPS.

When rendering with both methods, first the *SPS* method is done and then the *default* method is rendered on top of it. In this mode, the output of *SPS* is given a red tint in order to differentiate between the pixels produced by the two methods.

## What to expect
If you are using an HMD that is having co-planar screens and/or using symmetric projections, then you will observe nothing; the images in all modes will be exactly the same. (Except for the red tint in *both* methods.)

If you are using an HMD that is using asymmetric projections, then you can observe the difference in the images. By changing between *SPS* and *default* (keys **S** and **D**) you will see that the objects in the right eye move a bit. This can be observed by placing the HMD on a desk too and changing modes.

Entering the *both* method, the left eye is fully covered in red or is fully covered in white but the right eye contains pixels with both tints. This happens because the objects in the right eye are not in the exact same location when calculated with Single Pass Stereo.

Below is a capture from a Valve Index showing both eyes side by side. You can observe that the right side is slightly moving up and down by switching modes with keys **S** and **D**.

![Diff between SPS and default rendering for the right eye](https://github.com/ikapoura/Single-Pass-Stereo-with-SteamVR/blob/master/sps_right_eye_diff.gif "Diff between SPS and default rendering for the right eye")

## Prebuilt binary for Windows 10
I have added a prebuilt binary in order to execute the program without building it.

1. Download the repository.
2. Run SteamVR.
3. Run the executable single-pass-stereo-with-openvr/sps_with_openvr_prebuilt/bin/hellovr_opengl.exe.


## How to build

1. Download the [OpenVR SDK](https://github.com/ValveSoftware/openvr).
2. Open the [hello_opengl sample](https://github.com/ValveSoftware/openvr/tree/master/samples/hellovr_opengl) in Visual Studio.
3. Replace the file **hellovr_opengl_main.cpp** with the [same file in this project](https://github.com/ikapoura/Single-Pass-Stereo-with-SteamVR/blob/master/hellovr_opengl_main.cpp).
4. Build and run the application in either Debug or Release.

