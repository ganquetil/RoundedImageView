RoundedImageView
================

A fast ImageView (and Drawable) that supports rounded corners based on the original [example from Romain Guy](http://www.curious-creature.org/2012/12/11/android-recipe-1-image-with-rounded-corners/)

![RoundedImageView screenshot](https://raw.github.com/makeramen/RoundedImageView/master/screenshot.png)

There are many ways to create rounded corners in android, but this is the fastest and best one that I know of because it:
* does **not** create a copy of the original bitmap
* does **not** use a clipPath which is not hardware accelerated and not anti-aliased.
* does **not** use setXfermode to clip the bitmap and draw twice to the canvas.

If you know of a better method, let me know and I'll implement it!

Also has proper support for:
* Borders (with Colors and ColorStateLists)
* All `ScaleType`s
  * Borders are drawn at view edge, not bitmap edge.
  * Except on edges where the bitmap is smaller than the view
  * Borders are **not** scaled up/down with the image (correct width and radius are maintained)
* Anti-aliasing
* Transparent backgrounds
* Hardware acceleration
* Support for TransitionDrawables (XML attrs only)


Gradle
----
RoundedImageView is available on [Ark](https://github.com/ark/ark).

Add the following to your `build.gradle` to use:
```
repositories {
    maven {
        url 'https://raw.github.com/ark/ark/master/releases/'
    }
}

dependencies {
    compile 'com.makeramen:roundedimageview:1.0.0'
}
```

Maven
----

Make sure you installed Android 4.2 from the [Android Maven Deployer](https://github.com/mosabua/maven-android-sdk-deployer)

Build the apk:
```
git clone https://github.com/vinc3m1/RoundedImageView.git
cd ./RoundedImageView/
mvn clean install
```
Install and run:
````
cd ./example
mvn android:deploy android:run
````
If you want to use the library, add this dependency:
```
<dependency>
    <groupId>com.makeramen.rounded</groupId>
    <artifactId>library</artifactId>
    <version>0.1</version>
    <type>apklib</type>
</dependency>
```

Use Library
----
Define in xml:

```xml
<com.makeramen.RoundedImageView
        xmlns:makeramen="http://schemas.android.com/apk/res/com.makeramen.rounded.RoundedImageView"
        android:id="@+id/imageView1"
        android:src="@drawable/photo1"
        android:scaleType="centerCrop"
        makeramen:corner_radius="30dip"
        makeramen:border="2dip"
        makeramen:border_color="#333333"
        makeramen:round_background="true" />
```

Or in code:

```java
RoundedImageView iv = new RoundedImageView(context);
iv.setScaleType(ScaleType.CENTER_CROP);
iv.setCornerRadius(10);
iv.setBorderWidth(2);
iv.setBorderColor(Color.DKGRAY);
iv.setRoundedBackground(true);
iv.setImageDrawable(drawable);
iv.setBackground(backgroundDrawable);
```

Known Issues
--------------------------------------
* Programmatically setting attributes with TransitionDrawables not yet supported.
* Only tested support for BitmapDrawables and TransitionDrawables (with BitmapDrawables in them). Other types might work but may have unexpected behavior.
