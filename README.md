
# Exporting TurboWarp Projects to Android - A Guide

## Prerequisites
- Android Studio

## Creating the Project
### Step 1
Begin by launching Android Studio and initiating a new project. Ensure you select "No Activity" as your project template and proceed by clicking "Next."

![Project Creation Step 1](https://github.com/SuperTavor/TWAndroid/assets/111663937/6b95098e-196f-451b-93c5-ca1e3410efc4)

### Step 2
Upon clicking "Next," you will be directed to the following screen:

![Project Creation Step 2](https://github.com/SuperTavor/TWAndroid/assets/111663937/de818876-05f6-4336-a638-f82c882084f7)

Here's a brief overview of the elements on this screen:
- **Name**: Enter your app's display name in this field.
- **Package Name**: This serves as a unique identifier for your app. Use the following format: com.YourName.GameName.
- **Save Location**: Specify where your project will be saved.

Fill in your game name, desired package name, and make sure to select Java as your programming language. Then, click "Finish."

## Creating MainActivity
### Step 1
Start by displaying the contents of the Java directory.

![Java Directory](https://github.com/SuperTavor/TWAndroid/assets/111663937/28658659-7130-4140-9e5b-ef7c7de2bfb8)

Next, right-click on the folder named after your package name (excluding those with "(test)" or "(androidTest)" in their names).

![Right-Click on Package Folder](https://github.com/SuperTavor/TWAndroid/assets/111663937/0f42f9dc-b898-4ee1-a92c-279f8b3e6e01)

Select "New" and then choose "Java class."

![Create Java Class](https://github.com/SuperTavor/TWAndroid/assets/111663937/30c92330-04c1-43f2-b090-027beb6d9cb3)

Name it "MainActivity."

![Name MainActivity](https://github.com/SuperTavor/TWAndroid/assets/111663937/6913c88f-e4dd-4edd-ae12-700c0cb83c59)

### Step 2
Paste in the following code, but don't forget to replace the sample package name at the top with your actual package name. Don't worry about compilation errors; we will resolve them in the next step.

```java
package your.package.name;

import android.app.Activity;
import android.os.Bundle;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;

public class MainActivity extends Activity {

    private WebView webView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        webView = findViewById(R.id.webView);
        setupWebView();
    }

    private void setupWebView() {
        webView.setWebViewClient(new WebViewClient());
        WebSettings webSettings = webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webSettings.setDomStorageEnabled(true);
        webView.loadUrl("file:///android_asset/game.html");
    }
}
```

## Adding Our Layout
### Step 1
First, right-click the `res` folder and select "Android Resource Directory."

![Create Android Resource Directory](https://github.com/SuperTavor/TWAndroid/assets/111663937/a815e992-2a93-4707-9b4f-5a22d2f69c1e)

You will be directed to the following screen:

![Resource Directory Settings](https://github.com/SuperTavor/TWAndroid/assets/111663937/a9f40222-f652-4878-8ad2-f84b06e84360)

Set the directory name to "layout" and the resource type to "layout" as well. Now, click "OK." Here's how the final resource directory options should look:

![Resource Directory Options](https://github.com/SuperTavor/TWAndroid/assets/111663937/8326e380-79a3-4a37-bbe1-b7c4a17f76cf)

Right-click on the newly created folder and create a Layout Resource File.

![Create Layout Resource File](https://github.com/SuperTavor/TWAndroid/assets/111663937/a9e4e87b-0794-48cd-947a-0a6a14e6c5d3)

Set the file name to "activity_main" and click "OK."

![Name Layout Resource File](https://github.com/SuperTavor/TWAndroid/assets/111663937/58c7e51e-3219-4a6a-898e-c2f17475489e)

Double-click the newly created file to access the layout screen, then click on the "code" button at the top right corner.

![Access Layout Code](https://github.com/SuperTavor/TWAndroid/assets/111663937/7fa58e6a-9764-4ef9-a206-db99b29c9ca1)

Paste in the following code:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <WebView
        android:id="@+id/webView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</RelativeLayout>
```

## Importing Your TurboWarp Game
### Step 1
Export your TurboWarp project as HTML. If you want your game resolution to fit a vertical mobile screen, I recommend using 360x640. Additionally, it's advisable to enable the option below, as it addresses a sound bug that doesn't affect our app:

![Export TurboWarp Project](https://github.com/SuperTavor/TWAndroid/assets/111663937/099b452a-3a17-4509-a7db-518c48e0494b)

### Step 2
Now, return to Android Studio. In the top left corner of the IDE, right-click the "app" folder and create a new "Assets Folder."

![Create Assets Folder](https://github.com/SuperTavor/TWAndroid/assets/111663937/b7b934d1-edc4-44ef-a339-aa6a6d230a5c)

In this screen, simply click "finish."

![Finish Creating Assets Folder](https://github.com/SuperTavor/TWAndroid/assets/111663937/8ba567a5-14f3-4fa3-af58-67895c8d76d4)

Now, right-click our newly created "assets" folder and open it in Explorer.

![Open Assets Folder in Explorer](https://github.com/SuperTavor/TWAndroid/assets/111663937/7aaf948f-

44ec-486c-b5b4-9734c64c169a)

Place your exported TurboWarp game in there and rename it to "game.html".

**NOTE: NOT RENAMING THE HTML FILE WILL CAUSE THE APP TO CRASH!!**

![Rename Game HTML](https://github.com/SuperTavor/TWAndroid/assets/111663937/5643c381-d6e5-4b8b-ab11-0958b66bc790)

## Setting up AndroidManifest.xml

In your project, open the 'manifests' and double-click "AndroidManifest.xml." Paste this code in, BUT!
- In line 4, replace the sample package name with your app's package name.
- In line 14, replace the sample app name with your app's name (not package name, just the name).
- In line 17, replace `your.package.name.MainActivity` with your actual package name followed by `.MainActivity`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="your.package.name">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.YourAppName"
        tools:targetApi="31">
        <activity
            android:name="your.package.name.MainActivity"
            android:label="@string/app_name"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>

</manifest>
```

# Conclusion
That concludes our guide! To further enhance your app with features like icons or advertisements, feel free to follow any Android app tutorials available. Happy game making!
