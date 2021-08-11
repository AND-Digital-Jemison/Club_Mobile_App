# Jemison App setup

Requirements:

- nodeJS
- npm
- AWS account - personal or AND's
- AmplifyCLI
- Android Studio / Xcode - to run emulators of Android or iOS phones

## Amplify

[](https://docs.amplify.aws/cli/start/install)

**amplify install:**
```zsh
$ npm install -g @aws-amplify/cli
```
**amplify setup:**
```zsh
$ amplify configure
```

- asks u to log into your AWS account in your browser
- specify the AWS region → **eu-west-2** Europe (London)
- asks u to create username → **amplify-user**

  - then redirects u to your AWS console in the browser to finish the user creation process

  in the AWS console

  - keep the default **Pragmatic Access**
  - keep the default permissions **AdministratorAccess** - we need admin because we will be adding other AWS services cognito, dynamoDB ...
  - in the **Tag** creation we set the KEY=name,id? VALUE to **GCMobileApp**- ask John
  - once you've created the user next page contains your **ONE TIME visible access keys** so make sure you export these as .csv or copy them somewhere so you don't loose them, you will need them to finish the Amplify config

- now continue in terminal with providing the user's **ACCESS KEY**
- next provide a **SECRET ACCESS KEY**
- choose a amplify profile name i called mine **jemison-amplify-profile**

done

**amplify initialization** - in your app root dir
```zsh
$ amplify init
```
- set things until the FRAMEWORK we are using after that is everything default except the last question
- choose the profile you want to use is your amplify profile with the admin user and AWS access credentials we have created in previous section → choose that profile

![Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled.png](Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled.png)

when this is finished we have initialized our project in cloud, where we can use resources which we add later

![Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%201.png](Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%201.png)

do 
```zsh
$ amplify status
```
 and you will see we haven't setup any other AWS resources to our app

## React Native

[How to Install React Native on Mac? Step by Step Guide](https://rlogicaltech.medium.com/how-to-install-react-native-on-mac-step-by-step-guide-1ac822aedd4f)

**Install RN**
```zsh
$ npm install -g react-native-cli
```

**initialize the project - in a folder of your choice**
```zsh
$ react-native init JemisonMobileApp
```

Open the folder in your VS Code

you need 2 terminal windows in VS Code

in 1st - run your app
```zsh
$ react-native start
```

in 2nd - run one of the the emulators
```zsh
$ react-native run-android
$ react-native run-ios
```

at this point we should be able to at least show some default window in the emulator , but here is where problems usually starts :D google the errors, add them in here if you get something new.

we have the basic setup we can build upon

# Troubleshooting ANDROID

- if you get error message about **error with android SDK** and you have Android studio installed
  - you need to create file inside **/android/** directory called **local.properties**
    - add this inside **sdk.dir = /Users/USERNAME/Library/Android/sdk**

[SDK location not found. Define location with sdk.dir in the local.properties file or with an ANDROID_HOME environment variable](https://stackoverflow.com/questions/27620262/sdk-location-not-found-define-location-with-sdk-dir-in-the-local-properties-fil)

---

## **before you use run-android** in your terminal you need to start the android studio and turn on the emulator first

![Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%202.png](Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%202.png)

![Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%203.png](Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%203.png)

I might have some extras but you can pick any or create your own with your required Android API on the bottom + CREATE VIRTUAL DEVICES

---

Failed

**could not find tool.jar**

follow this guide to add **JAVA** path to your terminal **global PATH in zshrc**

[Could not find tools.jar. Please check that /Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home contains a valid JDK installation](https://stackoverflow.com/questions/64968851/could-not-find-tools-jar-please-check-that-library-internet-plug-ins-javaapple)

follow this guide to add ANDROID SDK path to your terminal **global PATH in zshrc**

[React Native adb reverse ENOENT](https://stackoverflow.com/questions/38835931/react-native-adb-reverse-enoent)

---

# Troubleshooting iOS

- You have a Xcode installed and trying to run ios with error

**fatal error: 'React/RCTBridgeDelegate.h' file not found**

- go to your **/ios/** dir in terminal and run commands
    ```zsh
    $ pod init
    ```
    ```zsh
    $ pod install
    ```
  - if you get error during install you might need to update the existing pods
  ```zsh
  $ pod repo update
  ```

  i had to update and after that i did pod install again

  **pods** - cocoapods dependency manager.

  [React/RCTBridgeDelegate.h' file not found](https://stackoverflow.com/questions/56916798/react-rctbridgedelegate-h-file-not-found)

  ***

  if you need to first install cocoapods manager
  ```zsh
  $ sudo gem install cocoapods --pre
  ```

  then install pods
  ```zsh
  $ pod install
  ```

  after these steps I was able to run both android and ios emulators.

  ![Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%204.png](Jemison%20App%20setup%20f57bb89a2abe46dd9fc900bd0742374b/Untitled%204.png)
