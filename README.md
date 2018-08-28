# OpenGoogle 
(Based from openFB by https://github.com/ccoenraets/openFB)

openGoogle is a Micro-Library for Google integration in JavaScript apps running in the browser and in Cordova.

openGoogle has no dependency: You don't need the Google plugin when running in Cordova. (just for share function)

openGoogle allows you to login to Google and execute any Google Api API request.

Here are a few code examples...

Login using Google:

```
openGoogle.login(callback, {scope: https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email'});
```

Get the user profile:

```
openGoogle.api({path: '/plus/v1/people/me', success: successHandler, error: errorHandler});
```


The approach used in openGoogle (plain OAuth + direct requests to API endpoints) is simple and lightweight, but it is definitely not perfect.

Pros:
- No plugin dependency and no uncertainties when new versions of Cordova or the Google SDK are released.
- Works for all platforms, including platforms for which a version of the Google plugin doesn't exist. 
- Works for both browser-based apps and Cordova apps.

Cons:
- Not full-fledged, less out-of-the box features.
- Integration not as tight. For example, no native dialogs, etc.

## Browser and Cordova Apps
The library works for both browser-based apps and Cordova/PhoneGap apps. When running in a browser, the OAuth URL redirection workflow happens in a popup window. When running in Cordova, it happens inside an "In-App Browser".

## Getting Started

### Creating a Facebook application

1. Login to Google

1. Access [https://console.developers.google.com](https://console.developers.google.com), select a project (or create before)

1. Select **Credentials** as the platform

1. Create a new **OAuth ID Client** 

1. Click in the **EDIT ICON** on the new Client Generated

1. In the **Authorized redirect URIs** section, add the following URLs in the **URI Field** field:
    - [http://localhost:8100/oauthcallback.html](http://localhost:8100/oauthcallback.html) (for access using ionic serve)
    - [http://<yourdomain>/oauthcallback.html](http://<yourdomain>/oauthcallback.html) (for access from Cordova)

1. Click **Save button**  

1. In the end copy Client ID like [tokenGeneratedByGoogle].apps.googleusercontent.com 

### Running the Sample in the Browser

1. Copy the Google OAuth Client ID for the app you just created and paste it as the first argument of the openGoogle.init() method invocation in index.html.
1. Load index.html, from a location that matches the redirect URI you defined above. For example: http://localhost:8100

### Running the Sample in Cordova

1. Create a Cordova project

    ```
    cordova create sample com.openGoogle.sample sample
    ```

1. Add the InAppBrowser Plugin

    ```
    cd sample
    cordova plugins add cordova-plugin-inappbrowser
    ```

1. Delete the contents of the ```www``` directory 
1. Copy ```index.html``` and ```openGoogle.js``` from the openGoogle project to the ```www``` directory of your Cordova project

    > Make sure your index.html includes ```<script src="cordova.js"></script>```. cordova.js does not need to (and shouldn't be) present in your ```www``` folder: it is automatically injected by the cordova build process.

1. Make sure you are in your Cordova project's root directory, add a platform, and build the project. For example: 

    ```
    cordova platform add ios
    cordova build ios
    ```
    
1. Run the project on device or in the emulator    


## AngularJS Wrapper [UNDER RECONSTRUCTION]

If you are using AngularJS, you can use ngopenGoogle which provides a wrapper around the openGoogle library and allows you to use openGoogle "the Angular way":
- As an Angular service instead of a global object
- Using promises instead of callbacks
 
indexng.html provides an AngularJS sample. 

Check out the [Ionic Tutorial](https://ccoenraets.github.io/ionic-tutorial/) for a complete example.

## Angular 2-6

1. Open angular.json file, put on Scripts block the path of your openGoogle.js
2. put in the same file your oauthcallback.html on block assets and save
3. On typings.d.ts, put the code and save: 
```
declare var openGoogle: any;
```
## Summary

The Google Plugin is still the best technical solution to integrate your Cordova app with Google because it provides a tighter integration (using native dialogs, etc). However, if you are looking for a lightweight and easy-to-set-up solution with no dependencies, or if you are targeting mobile platforms for which an implementation of the plugin is not available, you may find this library useful as well.

