# Single Pass Stereo with OpenVR

## What this project is
The focus of this project is to show that Single Pass Stereo is not producing the correct projected image for the right eye when used with a Head Mounted Display (HMD) that is using asymmetric projections for the eyes. It is important to note that SPS will produce images regardless of the HMD used, but the right eye image will not be exactly correct in some of them (if not most). So, **it may seem that SPS is working, at first glance, because the problem is not obvious**.

This project is a one file project that implements the [Single Pass Stereo](https://developer.nvidia.com/vrworks/graphics/singlepassstereo) functionality in the [OpenVR (SteamVR)](https://github.com/ValveSoftware/openvr) OpenGL sample.

It is complementary to my posts [Single Pass Stereo: is it worth it?](https://iliaskapouranis.com/2020/07/13/is-single-pass-stereo-worth-it/) and [Single Pass Stereo: wrong depth cues, discomfort and potential risks](https://iliaskapouranis.com/2020/08/13/single-pass-stereo-wrong-depth-cues-discomfort-and-potential-risks/).

First, I provide the steps to do when testing an HMD for SPS compatibility and then the details for the more curious.

## Fast way to check if SPS is working with your HMD, without the details
1. Download the **whole repository**.
2. Open the program located at **single-pass-stereo-with-openvr/sps_with_openvr_prebuilt/bin/hellovr_opengl.exe**.
3. When the program has started, a scene with many cubes will be rendered.
4. Press the **key "A"** from the keyboard to activate the test method.
5. If you are not wearing the HMD, go to step 7.
6. Close your left eye.
7. Notice if the right eye image is having **both white and red** cube faces.
8. If all the cube faces have **the same color**, then SPS is working **correctly**.
9. If the cube faces have **both red and white tints**, then SPS result is **not correct**.

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

| ![Difference between SPS and default rendering for the right eye](https://github.com/ikapoura/Single-Pass-Stereo-with-SteamVR/blob/master/sps_right_eye_diff.gif "Difference between SPS and default rendering for the right eye") | 
|:--:| 
| *Difference between SPS and default rendering for the right eye. The right side is moving up and down when changing modes.* |

Below is a capture with both modes enabled, using the key **A**, from a Valve Index showing both eyes side by side. You can observe that the right side contains both red and yellow tints while the left side is only in red. This means that the positions in the right side are not exactly the same; the red tinted cube sides should be where the white ones are.

| ![Diff between SPS and default rendering for the right eye with both methods enabled](https://github.com/ikapoura/Single-Pass-Stereo-with-SteamVR/blob/master/sps_mirror_view_combined.gif "Diff between SPS and default rendering for the right eye with both methods enabled") | 
|:--:| 
| *Difference between SPS and default rendering with both methods enabled. The left eye is correct, but the red tinted cube sides in the right eye should be where the white ones are.* |

## Prebuilt binary for Windows 10
I have added a prebuilt binary in order to execute the program without building it.

1. Download the repository.
2. Run SteamVR.
3. Run the executable **single-pass-stereo-with-openvr/sps_with_openvr_prebuilt/bin/hellovr_opengl.exe**.


## How to build

1. Download the [OpenVR SDK](https://github.com/ValveSoftware/openvr).
2. Open the [hello_opengl sample](https://github.com/ValveSoftware/openvr/tree/master/samples/hellovr_opengl) in Visual Studio.
3. Replace the file **hellovr_opengl_main.cpp** with the [same file in this project](https://github.com/ikapoura/Single-Pass-Stereo-with-SteamVR/blob/master/hellovr_opengl_main.cpp).
4. Build and run the application in either Debug or Release.
