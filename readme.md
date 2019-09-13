# AUTHENTICATE REACT-NATIVE APPLICATION WITH AUTH0

  This is a short and simple application for authenticating users in react native. You'll get token back whic you can pass to the server for authorizing the user. Just follow below steps :

   - signup on auth0

   - create applicaion 
   
   - click on the application created 
   
   - add ${applicationId}://${Domain}/android/${applicationId}/callback to **allowed callback URL's** .
   
        * Here applicationId can be obtained from your react-native project. Just navigate to android/app/build.gradle you'll find something like :
            
            ```build.gradle
                defaultConfig {
                    applicationId "com.something"
                    minSdkVersion rootProject.ext.minSdkVersion
                    targetSdkVersion rootProject.ext.targetSdkVersion
                    versionCode 1
                    versionName "1.0"
                }
            ```
            
        * After adding **allowed callback URL's** scroll up to get **Domain** and **ClientId** as they are needed to be passed to **react-native-auth0** component.
        
   - this is how you **AndroidManifest.xml** should look :
   
            ```AndroidManifest.xml
            
              <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                package="com.authintegration">

                <uses-permission android:name="android.permission.INTERNET" />

                <application
                    android:name=".MainApplication"
                    android:label="@string/app_name"
                    android:icon="@mipmap/ic_launcher"
                    android:roundIcon="@mipmap/ic_launcher_round"
                    android:allowBackup="false"
                    android:theme="@style/AppTheme">
                    <activity
                        android:name=".MainActivity"
                        android:label="@string/app_name"
                        android:launchMode="singleTask"
                        android:configChanges="keyboard|keyboardHidden|orientation|screenSize"
                        android:windowSoftInputMode="adjustResize">
                         <intent-filter>
                            <action android:name="android.intent.action.MAIN" />
                            <category android:name="android.intent.category.LAUNCHER" />
                        </intent-filter>
                        <intent-filter>
                            <action android:name="android.intent.action.VIEW" />
                            <category android:name="android.intent.category.DEFAULT" />
                            <category android:name="android.intent.category.BROWSABLE" />
                            <data
                                android:host=${Domain}     **This is the Domain which you must have grabbed from application you created in auth dashboard**
                                android:pathPrefix="/android/${applicationId}/callback" **applicationId same as you provided above
                                android:scheme=${applicationId} />
                        </intent-filter>
                    </activity>
                    <activity android:name="com.facebook.react.devsupport.DevSettingsActivity" />
                </application>
             </manifest>

            ```
            
  - npm install react-native-auth and pass const auth0 = new Auth0({ domain: ${Domain}, clientId: ${ClientId} }) in **App.js**.
    
  - Go through **App.js** to have a look at code.