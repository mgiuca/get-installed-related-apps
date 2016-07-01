# Get Installed Related Apps API

# Abstract
As the capabilities of the web grow, the functionality of web apps begins to
match that of corresponding native apps. The situation of users having a web
app and the corresponding native app both installed on the same device will
become more common, and the feature sets of these apps will converge.

It is important to allow apps to detect this situation to allow them to disable 
functionality that should be provided by the other app.

The GetInstalledRelatedApps API allows web apps to detect if related native apps
are installed on the current device.

# Querying the installed local apps that specify the website.
```js
navigator.getInstalledRelatedApps().then(function(listOfInstalledApps) {
    // success
    for (var app of listOfInstalledApps) {
        // These fields are specified by the Web App Manifest spec.
        console.log(app.platform);
        console.log(app.url);
        console.log(app.id);
    }
}, function() {
    // failure
});
```

# Describing a relationship from native application to website (and vice versa)
This API is being developed with the assumption that a system exists to create
associations from applications to web applications.

We can define relationships between a web application and other applications by
using the "related_applications" member of the web application manifest.

Each platform has its own method of verifying a relationship. In Android, the
[Digital Asset Links](https://developers.google.com/digital-asset-links/v1/create-statement)
system can be used to define an association between a website and an application.
If the application is installed locally and defines an association with the
requesting web application, we return the app as defined in the
"related_applications" member.

# Privacy Considerations
This feature only works with sites using HTTPS. This ensures that the website
cannot be spoofed, and that the association between the site and application is
valid.

The User Agent should return no installed applications when running in a privacy
preserving mode, for example Incognito in Chrome or Private Browsing in Firefox.
