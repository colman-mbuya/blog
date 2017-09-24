Recently, I have started looking into the Xamarin mobile platform, which is becoming increasingly popular among mobile application developers. Specifically, I was interested in seeing how different Xamarin apps are from native applications we normally test, and what these diferences mean in terms of our testing methodology. So far I have mainly looked at Xamarin Android and the purpose of this post is to share what I have learned.

# Platform Overview

The Xamarin mobile platform allows developers to develop Android, iOS and Windows phone applications in C# using the mono framework. The main advantage of developing applications in Xamarin is the potential for significant code reuse between the platforms. For example, code that would make up the data and data access layer; business layer; and service access layer could be shared. Application UI is developed separately for each platform - $$$XML, Storyboards and XAML$$$ are used to write UI code for Android, iOS and Windows phone respectively. However, with Xamarin.Forms, it is possible to develop one UI for all three platforms.

## Code Reuse

Code in Xamarin mobile applications can be shared using either a portable class library (PCL) or a shared project.

<DIAGRAM>

A PCL is a essentially a library that can be referenced by different project types. It is compiled into a DLL $$$and, in Android, bundled into the APK.$$$ A shared project is a project type itself and can be copied to any referencing projects. Shared projects typically contain precompiler statements that define which code can be included in which types of projects.

# Xamarin Android

Xamarin.Android provides developers access to typical .NET libraries such as System.Xml, System.IO and System.Net using the Mono framework, an open source version of the .NET framework. Developers also have access to native android components such as sensors and the camera in C# though the Mono.Android $$$library$$$. Mono.Android is essentially a C# wrapper of the Android APIs.

Syntax-wise, Xamarin Android code is very similar to native Java Android code. Below is a code snippet to illustrate this.

```
[Activity(Label = "Take a picture with Ray")]
    public class TakePictureActivity : Activity
    {
        private ImageView rayPictureImageView;
        private Button takePictureButton;
        private File imageDirectory;
        private File imageFile;
        private Bitmap imageBitmap;

        protected override void OnCreate(Bundle savedInstanceState)
        {
            base.OnCreate(savedInstanceState);
            SetContentView(Resource.Layout.TakePictureView);
            .
            .
            .
        }

        private void TakePictureButton_Click(object sender, EventArgs e)
        {
            Intent intent = new Intent(MediaStore.ActionImageCapture);
            imageFile = new File(imageDirectory, String.Format("PhotoWithRay_{0}.jpg", Guid.NewGuid()));
            intent.PutExtra(MediaStore.ExtraOutput, Android.Net.Uri.FromFile(imageFile));
            StartActivityForResult(intent, 0);
        }

        protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
        {
            int height = rayPictureImageView.Height;
            int width = rayPictureImageView.Width;
            imageBitmap = ImageHelper.GetImageBitmapFromFilePath(imageFile.Path, width, height);

            if (imageBitmap != null)
            {
                rayPictureImageView.SetImageBitmap(imageBitmap);
                imageBitmap = null;
            }

            // required to avoid memory leaks!
            GC.Collect();
        }
    }
```

<MAYBE TALK ABOUT NATIVE LIBRARIES HERE AND WHETHER IT WOULD BE POSSIBLE TO INCLUDE THEM IN XAMARIN>

## Reversing and Tampering

As Xamarin Android apps are compiled into apks, standard reversing tools such apktool, enjarify or dex2jar can be used to reverse Xamarin Android apps. Tampering with code written in Java remeains the same
<TALK ABOUT WHAT THE RESULTING APK LOOKS LIKE HERE>

<TALK ABOUT WHAT THIS MEANS IN TERMS OF TAMPERING>

## Code Obfsucation
<TALK ABOUT WHAT AVENUES EXIST FOR CODE OBFSUCATION>

## Instrumentation

<TALK ABOUT WHAT WORKS WHEN IT COMES TO INSTRUMENTING XAMARIN APPS>
