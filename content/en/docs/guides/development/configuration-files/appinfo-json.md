---
title: appinfo.json
date: 2024-01-17
weight: 10
toc: true
---

`appinfo.json` contains various metadata of apps, such as an app ID and type.

webOS device uses `appinfo.json` to identify the app, its icon, and other information that is needed to launch the app. `appinfo.json` is located in the app's root directory and contains a single JSON object.

{{< note >}}
Here are little tips that might help you with JSON syntax:

- Do not include any comments (/* or //) in JSON files.
- Use double quotes around the properties---no single quotes.
{{< /note >}}

## Schema

``` json
{
    "id"                            : String,
    "title"                         : String,
    "main"                          : String,
    "icon"                          : String,
    "type"                          : String,
    "largeIcon"                     : String,
    "vendor"                        : String,
    "version"                       : String,
    "appDescription"                : String,
    "resolution"                    : String,
    "iconColor"                     : String,
    "splashBackground"              : String,
    "transparent"                   : Boolean,
    "requiredMemory"                : Number,
    "requiredPermissions"           : String array
}
```

## Properties

### id

- Type: `String`
- Required: `Yes`

App ID

Every app has a unique ID, in a form of reversed DNS naming conventions. (e.g., `com.domain.app`) Using this ID, the [App Bar]({{< relref "webos-ose-ui-guide#app-bar" >}}) idetifies your app and displays it with the title. Each app ID is unique, sets once, and cannot be changed after publishing the app.

Here are naming rules for the app ID:

- Use lowercase (`a`-`z`), number digits (`0`-`9`), minus sign (`-`), and period (`.`).

    {{< caution >}}
    If you develop a JS service, do not use minus sign (`-`) in your app ID. It causes an unexpected error.
    {{< /caution >}}

- Must be at least two characters long.
- Start with an alphanumeric character.
- Don't start with the following names: `com.palm`, `com.webos`, `com.lge`, `com.palmdts`. Only the platform developers who implement built-in apps and services can use those names.
- (Optional) Start with the reverse domain of company/institution.

### title

- Type: `String`
- Required: `Yes`
	
The title of the app as shown in Launchpad and the app window. The app title is unique; once set, it cannot be changed after publishing the app.

### main

- Type: `String`
- Required: `Yes`
  
The launch point for the app. The file path must be relative to the project root directory and needs to point to the following, depending on the app type:

- Web app: `index.html`
- QML app: `main.qml`
- Native app: `<executable file name>`
### icon

- Type: `String`
- Required: `Yes`

Icon image displayed for your app. The icon should be in PNG format. The file path must be relative to the project root directory.

- **Default Value**: `icon.png`

### type

- Type: `String`
- Required: `Yes`

App type. The value must be specified as follows depending on the app type:

- Web app: `web`
- QML app: `qml`
- Native app: `native`

### largeIcon

- Type: `String`
- Required: `No`

Large app icon. The icon should be in PNG format.

### vendor

- Type: `String`
- Required: `No`

Provides the information of the app owner. This is used in deviceinfo dialogs.

### version

- Type: `String`
- Required: `No`

The app version number. This consists of three non-negative integers: major, minor, and revision numbers.

The major, minor, and revision numbers are all mandatory, e.g. "2.1.0" (not "2.1"). Otherwise, the app may not be installed. The major, minor, and revision numbers are discrete. For example, 1.5.3 is lower version than 1.15.3.

- **Default value**: `1.0.0`

{{< note >}}
Each version number (major, minor, and revision) cannot exceed 9 digits and cannot contain leading zeroes.
{{< /note >}}

### appDescription

- Type: `String`
- Required: `No`

Provides brief information of the app, like a short tagline for the app. It cannot exceed 60 characters.

### resolution

- Type: `String`
- Required: `No`
	
The screen resolution of the app. webOS Open Source Edition (OSE) supports the following resolutions:

- `1920x1080`: FHD resolution (Default value)
- `1280x720`: HD resolution

{{< note >}}
webOS OSE does not support UHD resolution for web apps.
{{< /note >}}

### iconColor

- Type: `String`
- Required: `No`
	
Indicates the background color for the app tile.

- **Default value**: `white`

### splashBackground

- Type: `String`
- Required: `No`
	
Path for a background image to be shown while the app is loading. The file path must be relative to the project root directory. The file should be in PNG format and the image size should be 1920 x 1080.

### transparent

- Type: `Boolean`
- Required: `No`

App background overlays system background. If you did not set the background color or background image, system background (black color) will be displayed.

This property configures the transparency of the app background. If set to true, the system background will be displayed clearly. If set to false, the transparency rate of app background will be decreased and the system background will be shown as little grey color.

- **Default value**: `false`
  
### requiredMemory

- Type: `Number`
- Required: `No`

Indicates the minimum amount of memory in megabytes required to run the app.

### requiredPermissions

- Type: `String array`
- Required: `No`

Specifies the required [Access Control Group (ACG)]({{< relref "security-guide" >}}) names associated with the LS2 API methods used in the app. The ACG names associated with each method can be found in their respective [LS2 API Reference]({{< relref "ls2-api-index" >}}).
    
### allowAudioCapture

- Type: `Boolean`
- Requires: `No`

Indicates whether to allow access to audio capture devices.

Possible values are:

- `true`: Allow audio capture.
- `false`: (default) Disallow audio capture.

{{< note >}}
Note: Added in API level 28.
{{< /note >}}

### allowVideoCapture

- Type: `Boolean`
- Requires: `No`

This indicates whether to allow access to video capture devices.

Possible values are:

- `true`: Allow video capture.
- `false`: (default) Disallow video capture.

### locationHint

- Type: `String`
- Requires: `No`

This property allows a Wayland client to ask the compositor to place its shell surface (main window) at a specific position expressed as cardinal points. 

Possible values are:

- `center` (default) 
- `north`
- `west`
- `south`
- `east`
- `northwest`
- `northeast`
- `southwest`
- `southeast`

### thirdPartyCookiesPolicy	

- Type: `String`
- Requires: `No`

This indicates whether to allow third-party cookies or not.

Possible values are: 

- `allow`: (default) Allow third-party cookies
- `deny`: Disallow third party cookies

### useUnlimitedMediaPolicy

- Type: `Boolean`
- Requires: `No`

This indicates whether the strict media policy will be relaxed.

Possible values are:

- `true`: Relax the strict media policy.
- `false`: (default) The strict media policy applies

## Example

{{< code "appinfo.json (web app)" true >}}
``` json
{
    "id": "com.myco.app.web",
    "title": "Web App",
    "main": "index.html",
    "icon": "icon.png",
    "type": "web"
}
```
{{< /code >}}

{{< code "appinfo.json (QML app)" true >}}
``` json
{
    "id": "com.myco.app.qml",
    "title": "QML App",
    "main": "main.qml",
    "icon": "icon.png",
    "type": "qml"
}
```
{{< /code >}}

{{< code "appinfo.json (native app)" true >}}
``` json
{
    "id": "com.myco.app.native",
    "title": "Native App",
    "main": "native",
    "icon": "icon.png",
    "type": "native"
}
```
{{< /code >}}

{{< code "appinfo.json (web app, with optional properties)" true >}}
``` json
{
    "id": "com.myco.app.appname",
    "title": "AppName",
    "main": "index.html",
    "icon": "AppName_80x80.png",
    "type": "web",
    "largeIcon": "AppName_130x130.png",
    "vendor": "My Company",
    "version": "1.0.0",
    "appDescription": "This is an app tagline",
    "resolution": "1920x1080",
    "iconColor": "red",
    "splashBackground": "AppName_Splash.png",
    "transparent": false,
    "requiredMemory": 20,
    "requiredPermissions": ["time.query", "media.operation"]
}
```
{{< /code >}}

## Localizing App Metadata

If the app is localized into more than one language, each language can have its own `appinfo.json` file. However, the app ID and version number in each localized `appinfo.json` must be the same as those in the top-level `appinfo.json`. The app ID and version in the top-level `appinfo.json` are validated for correct value and structure. Any app that fails the validation cannot be packaged or uploaded.

According to the locale setting value, the app metadata localization shows the matching app information at the Launchpad.

To provide app information in a specific locale, you need to create locale folders under the `resources` folder, then `appinfo.json` files for each locale under correct locations as shown below:

{{< figure src="/images/docs/guides/development/configuration-files/folder-structure-appinfo-json-localization.png" alt="" caption="Folder structure of appinfo.json localization" width="700px" >}}

{{< note >}}
The locale consists of Language, Script, and Country/Region information. (e.g. ko-KR, mn-Cy-MN)
{{< /note >}}

With additional `appinfo.json` files, `title` and `appDescription` can be provided in various languages. All other properties will be kept the same as the default `appinfo.json` file in the root of the project.

``` json
{
    "title": "<Translated app title>",
    "appDescription": "<Translated app description>",
}
```

{{< note >}}
  - In the `appinfo.json` file for localization, only `appDescription` and `title` properties can be filled.
  - If you need to use non-Latin letters (non-ASCII) in the `appinfo.json` file, the file needs to be saved in UTF-8 without BOM format.
{{< /note >}}

When the locale value is changed after adding an `appinfo.json` file corresponding to the locale information, the `appinfo.json` file in the app root directory is loaded into the system memory of the webOS device. Then the other `appinfo.json` files are overridden depending on the locale setting.
