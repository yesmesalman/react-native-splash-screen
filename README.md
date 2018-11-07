# React Native Splash Screen


React Native Version "0.57.4"
## Installation
  **Run** => npm i react-native-splash-screen --save
  
**Automatic installation**
  **Run** => react-native link react-native-splash-screen

## Manual installation (Android)

  **android/settings.gradle**
  ```
  include ':react-native-splash-screen'   
  project(':react-native-splash-screen').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-splash-screen/android')
  ```
  **android/app/build.gradle**
  ```
  ...
  dependencies {
      ...
      compile project(':react-native-splash-screen')
  }
  ```
  **MainApplication.java**
  ```
  // react-native-splash-screen >= 0.3.1
import org.devio.rn.splashscreen.SplashScreenReactPackage;
// react-native-splash-screen < 0.3.1
import com.cboy.rn.splashscreen.SplashScreenReactPackage;

public class MainApplication extends Application implements ReactApplication {

    private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
        @Override
        public boolean getUseDeveloperSupport() {
            return BuildConfig.DEBUG;
        }

        @Override
        protected List<ReactPackage> getPackages() {
            return Arrays.<ReactPackage>asList(
                    new MainReactPackage(),
            new SplashScreenReactPackage()  //here
            );
        }
    };

    @Override
    public ReactNativeHost getReactNativeHost() {
        return mReactNativeHost;
    }
}
  ```
  **MainActivity.java**
  ```
  import android.os.Bundle; // here
   import com.facebook.react.ReactActivity;
   // react-native-splash-screen >= 0.3.1
   import org.devio.rn.splashscreen.SplashScreen; // here
   // react-native-splash-screen < 0.3.1
   import com.cboy.rn.splashscreen.SplashScreen; // here

   public class MainActivity extends ReactActivity {
      @Override
       protected void onCreate(Bundle savedInstanceState) {
           SplashScreen.show(this);  // here
           super.onCreate(savedInstanceState);
       }
       // ...other code
   }
  ```
  Create a file called **launch_screen.xml** in **app/src/main/res/layout** (create the **layout-folder** if it doesn't exist). The contents of the file should be the following
  ```
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="vertical" android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:background="@drawable/launch_screen">
  </LinearLayout>
  ```
  Customize your launch screen by creating a **launch_screen.png-file** and placing it in an appropriate **drawable-folder**.
  * drawable-ldpi
  * drawable-mdpi
  * drawable-hdpi
  * drawable-xhdpi
  * drawable-xxhdpi
  * drawable-xxxhdpi
  
  Add a color called **primary_dark** in **app/src/main/res/values/colors.xml**
  ```
  <?xml version="1.0" encoding="utf-8"?>
  <resources>
      <color name="primary_dark">#000000</color>
  </resources>
   ```
   **Optional Step**
   Open **android/app/src/main/res/values/styles.xml** and add :
   ```
   <resources>
       <!-- Base application theme. -->
       <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
           <!-- Customize your theme here. -->
           <!--设置透明背景-->
           <item name="android:windowIsTranslucent">true</item>
       </style>
   </resources>
   ```
   Create **android/app/src/main/res/values/colors.xml** and add
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <resources>
       <color name="status_bar_color"><!-- Colour of your status bar here --></color>
   </resources>
   ```
   Create a style definition for this in **android/app/src/main/res/values/styles.xml** :
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <resources>
       <style name="SplashScreenTheme" parent="SplashScreen_SplashTheme">
           <item name="colorPrimaryDark">@color/status_bar_color</item>
       </style>
   </resources>
   ```
   Change your **show** method in **MainActivity.java** to include your custom style: 
   ```
   SplashScreen.show(this, R.style.SplashScreenTheme);
   ```
   **Usage**
   ```
   import SplashScreen from 'react-native-splash-screen'

    export default class WelcomePage extends Component {

        componentDidMount() {
         // do stuff while splash screen is shown
            // After having done stuff (such as async tasks) hide the splash screen
            SplashScreen.hide();
        }
    }
   ```
  
  
  
