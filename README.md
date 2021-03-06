![Icon](https://github.com/mikescandy/Xamarin-Cropper/raw/master/art/web_art.png) Xamarin Android Image Cropper
=======

A Xamarin Android binding library for [Android Image Cropper](https://github.com/ArthurHub/Android-Image-Cropper)

**Powerful** (Zoom, Rotation, Multi-Source), **customizable** (Shape, Limits, Style), **optimized** (Async, Sampling, Matrix) and **simple** image cropping library for Android.

![Crop](https://github.com/ArthurHub/Android-Image-Cropper/blob/master/art/demo.gif?raw=true)

## Usage
*For a working implementation, please have a look at the Sample Project*

[See GitHub Wiki for more info.](https://github.com/ArthurHub/Android-Image-Cropper/wiki)

1. Include the library

[Download from NuGet](https://www.nuget.org/packages/XamarinAndroidImageCropper/)

```
Install-Package XamarinAndroidImageCropper
```

Add permissions to manifest

 ```
 <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
 ```

### Using Activity

1. Start `CropImageActivity` using builder pattern from your activity
 ```java
 // start picker to get image for cropping and then use the image in cropping activity
 CropImage.Builder()
   .SetGuidelines(CropImageView.Guidelines.On)
   .Start(this);

 // start cropping activity for pre-acquired image saved on the device
 CropImage.Builder(imageUri)
  .Start(this);

 // for fragment (DO NOT use `getActivity()`)
 CropImage.Builder()
   .Start(Context, this);
 ```

2. Override `OnActivityResult` method in your activity to get crop result
 ```csharp
protected override void OnActivityResult(int requestCode, [GeneratedEnum] Result resultCode, Intent data)
 {
   if (requestCode == CropImage.PickImageChooserRequestCode) {
     CropImage.ActivityResult result = CropImage.GetActivityResult(data);
     if (resultCode == Result.Ok) {
       Uri resultUri = result.Uri;
     } else if (resultCode == CropImage.CropImageActivityResultErrorCode) {
       Exception error = result.Error;
     }
   }
 }
 ```

### Using View
1. Add `CropImageView` into your activity
 ```xml
 <!-- Image Cropper fill the remaining available height -->
 <com.theartofdev.edmodo.cropper.CropImageView
   xmlns:custom="http://schemas.android.com/apk/res-auto"
   android:id="@+id/cropImageView"
   android:layout_width="match_parent"
   android:layout_height="0dp"
   android:layout_weight="1"/>
 ```

2. Set image to crop
 ```csharp
 cropImageView.SetImageUriAsync(uri);
 // or (prefer using uri for performance and better user experience)
 cropImageView.SetImageBitmap(bitmap);
 ```

3. Get cropped image
 ```csharp
 // subscribe to async event using cropImageView.setOnCropImageCompleteListener(listener)
 cropImageView.GetCroppedImageAsync();
 // or
 Bitmap cropped = cropImageView.GetCroppedImage();
 ```

## Features
- Built-in `CropImageActivity`.
- Set cropping image as Bitmap, Resource or Android URI (Gallery, Camera, Dropbox, etc.).
- Image rotation/flipping during cropping.
- Auto zoom-in/out to relevant cropping area.
- Auto rotate bitmap by image Exif data.
- Set result image min/max limits in pixels.
- Set initial crop window size/location.
- Request cropped image resize to specific size.
- Bitmap memory optimization, OOM handling (should never occur)!
- API Level 14.
- More..
 
## Customizations
- Cropping window shape: Rectangular or Oval (cube/circle by fixing aspect ratio).
- Cropping window aspect ratio: Free, 1:1, 4:3, 16:9 or Custom.
- Guidelines appearance: Off / Always On / Show on Toch.
- Cropping window Border line, border corner and guidelines thickness and color.
- Cropping background color.

For more information, see the [GitHub Wiki](https://github.com/ArthurHub/Android-Image-Cropper/wiki). 

## Posts
 - [Android cropping image from camera or gallery](http://theartofdev.com/2015/02/15/android-cropping-image-from-camera-or-gallery/)
 - [Android Image Cropper async support and custom progress UI](http://theartofdev.com/2016/01/15/android-image-cropper-async-support-and-custom-progress-ui/)
 - [Adding auto-zoom feature to Android-Image-Cropper](https://theartofdev.com/2016/04/25/adding-auto-zoom-feature-to-android-image-cropper/)

## Change log
*2.5.1* (in-dev)
- Try solve manifest merger issue by adding `transitive` flag #405 (thx @j-garin)
- Use thread pool executors for async image loading and cropping operations to prevent app hang if default executor is busy (thx @ruifcardoso)
- Fix image rotation breaking min/max crop result restrictions #401
- Propagate all extra data set on start crop activity intent back in crop result intent #352

*2.5.0*
- Update to sdk v26
- Update gradle plugin to 2.0
- Update min sdk version to 14
- Fix NPE in `getWholeImageRect`
- Remove `crop_image_menu_crop` drawable support, replace with `setCropMenuCropButtonIcon` builder api.
- Support setting crop button title via builder api.
- Add string resource for "no permissions" toast.

*2.4.7*
- Fix toolbar menu crop icon sometimes appears with random icon (#305)
- Use CharSequence instead of string for activity title (thx @KentHawkings) (#297)
- Fix class not found exception on some Samsung devices (Huge thanks to @Vantablack) (#332)
- Add original image dimensions to CropResult (Thanks @gazialankus) (#327)
- Making the library JitPack-friendly (Thanks @gazialankus) (#325)
- Allow a Fragment to call the startPickImageActivity help method in CropImage (Thanks @cdavietei) (#315)

See [full change log](https://github.com/ArthurHub/Android-Image-Cropper/wiki/Change-Log).

## Android Image Cropper License
Originally forked from [edmodo/cropper](https://github.com/edmodo/cropper).

Copyright 2016, Arthur Teplitzki, 2013, Edmodo, Inc.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this work except in compliance with the   License.
You may obtain a copy of the License in the LICENSE file, or at:

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS   IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

## Binding License

Copyright 2016, Michele Scandura.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this work except in compliance with the   License.
You may obtain a copy of the License in the LICENSE file, or at:

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS   IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
