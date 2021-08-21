# cordova-plugin-splitview

## Native iOS Split View


## What’s New

* Supports either iOS14 and later  column-style layouts with two or three columns, or the classic split view. 
* Supports separate compact-view tab bar .
* Set properties via json.
* Similar behavior for embedding and non-embedding cases.

Except for the classic split view, this version no longer supports the TableView option .  A future version will include a more modern replacement. 
Classic split view will be supported as long as it is supported by Apple but all future plug-in development will target the iOS14+ version .   


## What’s Ahead

* TableView Option Replacement
* Additional Documentation
* Remove 6 tab limit and support “more” in TabView



## Installation
```bash
cordova plugin add cordova-plugin-splitview
```

## Configuration

Auto hiding of splash screen needs to be disabled in config.xml

```
<preference name="AutoHideSplashScreen" value="false" />
```


## iOS Split View

An iOS split view is a container that  manages  two or three child columns. 
The plugin creates a split view and the child views, supplying each with a WebView. Child WebViews can manage the split view and communicate with each other. 



## Getting Started

The best way is to build the Demo App. The demo shows both new and classic view options: two column, three column and tab-bar compact.

 - https://github.com/j-crosson/cordova-plugin-split-view-demo

See Apple’s UISplitViewController documentation for a more detailed explanation of the split view. 


See Classic Split View to support pre-iOS14 devices.




## Tab View

**Compact Size Class and TabView**

There are two size classes: Regular, which you would find on a large device such as an iPad or an iPhone 11 in landscape, and Compact which you would find on smaller device or an iPad running multiple apps in a split screen. 

The plug-in has the option of using a TabView for the Compact Size. The view will dynamically switch to/from a split view as the Size Class changes.  For example, when an iPhone 11 is rotated from portrait to landscape or when a second app is launched on an iPad. 


**Regular size**

![ ](https://raw.githubusercontent.com/j-crosson/cordova-plugin-split-view/main/images/regulariPad.png)

**Compact size**

![ ](https://raw.githubusercontent.com/j-crosson/cordova-plugin-split-view/main/images/compactiPad.png)



## iOS 14 and later Methods


### showView
```javascript
cordova.plugins.SplitView.showView (splitViewProps, primaryProps, secondaryProps, supProps, compactProps, success, error)
```

Show  split view.  

| Param | Type | Description |
| --- | --- | --- |
| splitViewProps | String | split view properties  |
| primaryProps | String | properties for primary view  |
| secondaryProps | String | properties for secondary view  |
| supProps | String | properties for supplementary view  |
| compactProps | String | properties for compact view  |
| onSuccess | Function | Success callback function|
| error | Function | Error callback |

Default is a modal split view.  Optionally the split view can be made the root view.  If the split view is made root, the original view (from which showView was called) is lost.  Using the “fullscreen” option preserves the original view but with the same appearance of split view as root. The split view is still modal and can be dismissed thus returning to the original view.  The original view can serve as a welcome page or simply display the startup background color and go unnoticed.   



### display
```javascript
cordova.plugins.SplitView.display (show_hide, view, success, error)
```

Present or dismiss view.  

| Param | Type | Description |
| --- | --- | --- |
| show_hide | Bool | show or hide  |
| view | String | view to show/hide: "primary", "secondary”, "supplementary", "compact"]  |
| success | Function | Success callback function|
| error | Function | Error callback |


See Apple UISplitViewController show/hide documentation for additional details.


### sendMessage 
```javascript
cordova.plugins.SplitView.sendMessage  (destination, message, success, error)
```

Send message to view.  

| Param | Type | Description |
| --- | --- | --- |
| destination | String | message destination: "primary", "secondary”, "supplementary", "compact"]  |
| message | String | message content  |
| success | Function | Success callback function|
| error | Function | Error callback |

JSON can be useful here.



### message

 function ( messageString)

| Param | Type | Description |
| --- | --- | --- |
| messageString | String | received message |

**messageString**

Received message sent by SendMessage. 


```javascript
var receivedMessage = function ( messageString) {
    //do something
}

 cordova.plugins.SplitView.message = receivedMessage;;
```



### setSplitViewProperties 
```javascript
cordova.plugins.SplitView.setSplitViewProperties  (properties, success, error)
```

Set properties on Split View.  Some properties can only be set on creation (showView)  

| Param | Type | Description |
| --- | --- | --- |
| properties | String | Container view properties |
| success | Function | Success callback function|
| error | Function | Error callback |



### setProperties 
```javascript
cordova.plugins.SplitView.setProperties (properties, success, error)
```

Set properties on Split View child view.  Some properties can only be set on creation (showView)  

| Param | Type | Description |
| --- | --- | --- |
| properties | String | Split View child properties |
| success | Function | Success callback function|
| error | Function | Error callback |



### initChild  
```javascript
cordova.plugins.SplitView.initChild  ()
```

Initialize Split View child.
Call for all views.  Typically called immediately after "device ready”.  
Call when ready to receive messages. 


### selectTab  
```javascript
cordova.plugins.SplitView.selectTab ( tab, success, error)
```
Select tab on bar

| Param | Type | Description |
| --- | --- | --- |
| tab | Number | selected tab |
| success | Function | Success callback function|
| error | Function | Error callback |






##  Properties

Properties are set via a JSON string.  

Example:

```javascript
let redBackground = 228;
let greenBackground = 228;
let blueBackground = 228;

viewPropJSON = '{"primaryTitle":"Primary", "secondaryTitle":"Secondary","fullscreen":true, "Style":"doubleColumn","backgroundColor":[' + redBackground+','+ greenBackground+ ',' + blueBackground+ ',' + '1]}';
```


| Property | Type | Description | Default |
| --- | --- | --- | --- | 
| primaryURL | String| URL of Primary View |  primary.html | 
| secondaryURL | String | URL of Secondary View  | secondary.html |
| supplementaryURL | String | URL of Supplementary View| supplementary.html | 
| compactURL | String | URL of Compact View | compact.html | 
| primaryTitle | String | Primary view NavigationBar title |  | 
| secondaryTitle | String | Secondary view NavigationBar title |  | 
| supplementaryTitle | String | Supplementary view NavigationBar title |  | 
| usesCompact | Bool | uses compactURL/TabView for Compact View |  false | 
| fullscreen | Bool | if SplitView is presented modally, make full screen | false | 
| makeRoot | Bool  |  Makes SplitView the root view | false | 
| style | String | The number of SplitView columns | doubleColumn | 
| preferredDisplayMode | String | Sets display mode if constraints allow | automatic |
| presentsWithGesture     | Bool | Hidden view controller  presented/dismissed via swipe gesture | true | 
| showsSecondaryOnlyButton | Bool | Secondary view controller—tripleColumn only—shows a secondary-only display-mode toggle button | false | 
| preferredSplitBehavior | String |  Child views  relation to each other  |  automatic |
| primaryColumnWidthFraction | Number |  Preferred relative width of the primary view.   Number between 0.0 and 1.0  | automaticDimension |
| preferredPrimaryColumnWidth | Number |  Preferred width, in points, of the primary view | automaticDimension |
| minimumPrimaryColumnWidth | Number | Sets min width, in points, of the primary view | automaticDimension | 
| maximumPrimaryColumnWidth | Number | Sets max width, in points, of the primary view | automaticDimension |
| supplementaryColumnWidthFraction | Number |  Preferred relative width of the supplementary view.   Number between 0.0 and 1.0  | automaticDimension |
| supplementaryColumnWidth | Number |  Preferred width, in points, of the supplementary view | automaticDimension |
| maximumSupplementaryColumnWidth | Number | Sets max width, in points, of the supplementary view | automaticDimension | 
| minimumSupplementaryColumnWidth | Number | Sets min width, in points, of the supplementary view | automaticDimension | 
| primaryEdge | String | Side of primary view | leading | 
| backgroundColor | Array | Sets primary view background color that is displayed during WebView load, overrides light/dark | |
| backgroundColorLight | Array | Sets primary view background color that is displayed during WebView load, in light mode | |
| backgroundColorDark | Array | Sets primary view background color that is displayed during WebView load, in dark mode | |
| tintColor | Array | Sets Navigation Bar  tint color (bar text etc.) | |
| barTintColor | Array | Sets Navigation Bar bar tint color (bar background) | |
| topColumnForCollapsingTo ProposedTopColumn | String | Provides the column to display after the split view interface collapses | |
| displayModeForExpandingTo ProposedDisplayMode | String | Provides the display mode to use after the split view interface expands | |

**Compact View TabBar Properties**

| Property | Type | Description | Default |
| --- | --- | --- | --- | 
| tabBarItems | Array| TabBar titles and images |   | 
| tabItemsAppend | Array| Modifies selected-item message |   | 
| selectedTabIndex | Number| set tab index | 0  | 


**primaryURL**

URL of Primary View content.

Type:   String

The default is “primary.html”


```javascript
viewPropJSON = '{"primaryURL":"triplePrimary.html" }';
```

**secondaryURL**

URL of Secondary View content.

Type:   String

The default is “secondary.html”

```javascript
viewPropJSON = '{"secondaryURL":"tripleSecondary.html" }';
```


**supplementaryURL**

URL of Supplementary View content.

Type:   String

The default is “supplementary.html”

```javascript
viewPropJSON = '{"supplementaryURL":"tripleSupplementary.html" }';
```

**compactURL**

URL of Compact View content.

Type:   String

The default is “compact.html”

```javascript
viewPropJSON = '{"compactURL”:”tabs.html" }';
```


**primaryTitle**

Primary view NavigationBar title.

Type:   String

The default is no title.

```javascript
viewPropJSON = '{"primaryTitle":"Primary" }';
```

**secondaryTitle**

Secondary view NavigationBar title.

Type:   String

The default is no title.

```javascript
viewPropJSON = '{"secondaryTitle":"Secondary" }';
```


**supplementaryTitle**

Supplementary view NavigationBar title.

Type:   String

The default is no title.

```javascript
viewPropJSON = '{"supplementaryTitle":"Supplementary” }';
```

**usesCompact**

uses compactURL/TabView for Compact View. 
If this option is selected, a compactURL must be set and tabBarItems added 

Type:   Bool

The default is false.

```javascript
viewPropJSON = '{"usesCompact":true }';
```

**fullscreen**

If SplitView is presented modally—the default—make full screen.  
This allows return to to the startup view programmatically but without the appearance of a modal view. 
If “makeRoot” is “true”,  “fullscreen” has no effect. 

Type:   Bool

The default is false.

```javascript
viewPropJSON = '{"fullscreen":true }';
```

**makeRoot**

Makes SplitView the root view.
The startup view is lost. 

Type:   Bool

The default is false.

```javascript
viewPropJSON = '{"makeRoot":true }';
```

**style**

The number of SplitView columns.

Type:   String

The default is “doubleColumn”.

 Values

doubleColumn   two column display.
tripleColumn      three column display.


```javascript
viewPropJSON = '{"style":"tripleColumn” }';
```

See Apple UISplitViewController Documentation for additional info.



**preferredDisplayMode**

The number of SplitView columns.

Type:   String

The default is “doubleColumn”.

 Values
automatic                       Split view controller automatically decides which display mode to use.
secondaryOnly              Only secondary view shown.
oneBesideSecondary    Sidebar appears beside secondary view.
oneOverSecondary       Sidebar on top of the secondary view, secondary view partially visible.
twoBesideSecondary    Two sidebars beside secondary view.
twoOverSecondary        Two sidebars on top of the secondary view, secondary view partially visible.
twoDisplaceSecondary  Two sidebars displace  secondary view, moving it partially offscreen.


```javascript
viewPropJSON = '{"preferredDisplayMode":"twoBesideSecondary” }';
```

See Apple UISplitViewController Documentation for additional info.



**presentsWithGesture**

 Hidden view controller  presented and dismissed via swipe gesture.

Type:   Bool

The default is true.

```javascript
viewPropJSON = '{"presentsWithGesture”:false }';
```

See Apple UISplitViewController Documentation for additional info.



**presentsWithGesture**

This only applies to tripleColumn display.
Secondary view  shows a secondary-only display-mode toggle button

Type:   Bool

The default is false.

```javascript
viewPropJSON = '{"presentsWithGesture”:false }';
```

See Apple UISplitViewController Documentation for additional info.


**preferredSplitBehavior**

Child views  relation to each other.

Type:   String

The default is “automatic”.

 Values
automatic                       Split view controller automatically selects split behavior.
tile                                   Sidebars and secondary view  tiled side-by-side.
overlay                            Sidebars overlay secondary view, secondary view partially visible.
displace                          Sidebars displace the secondary view, moving it partially offscreen.

```javascript
viewPropJSON = '{"preferredSplitBehavior":"tile” }';
```

See Apple UISplitViewController Documentation for additional info.



**primaryColumnWidthFraction**

Preferred relative width of the primary view.   Number between 0.0 and 1.0   Percentage of the overall width of the split view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"primaryColumnWidthFraction”:0.5 }';
```


See Apple UISplitViewController Documentation for additional info.



**preferredPrimaryColumnWidth**

Preferred width, in points, of the primary view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"preferredPrimaryColumnWidth”:300 }';
```

See Apple UISplitViewController Documentation for additional info.


**minimumPrimaryColumnWidth**

Sets min width, in points, of the primary view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"minimumPrimaryColumnWidth”:100 }';
```

See Apple UISplitViewController Documentation for additional info.


**maximumPrimaryColumnWidth**

Sets max width, in points, of the primary view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"maximumPrimaryColumnWidth”:200 }';
```
See Apple UISplitViewController Documentation for additional info.


**supplementaryColumnWidthFraction**

Preferred relative width of the supplementary view.   Number between 0.0 and 1.0   Percentage of the overall width of the split view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"supplementaryColumnWidthFraction”:0.5 }';
```
See Apple UISplitViewController Documentation for additional info.



**supplementaryColumnWidth**

Preferred width, in points, of the supplementary view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"supplementaryColumnWidth”:200 }';
```

See Apple UISplitViewController Documentation for additional info.



**minimumSupplementaryColumnWidth**

Sets min width, in points, of the supplementary view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"minimumSupplementaryColumnWidth”:100 }';
```

See Apple UISplitViewController Documentation for additional info.


**maximumSupplementaryColumnWidth**

Sets max width, in points, of the supplementary view.

Type:   Number

The default is automaticDimension.

```javascript
viewPropJSON = '{"maximumSupplementaryColumnWidth”:200 }';
```

See Apple UISplitViewController Documentation for additional info.


**primaryEdge**

Side of primary view.

Type:   String

The default is “leading”.

 Values
leading                       Primary view on leading edge.
trailing                        Primary view on trailing edge.

```javascript
viewPropJSON = '{"primaryEdge”:”trailing” }';
```

See Apple UISplitViewController Documentation for additional info.



**backgroundColor**

Sets primary view background color that is displayed during WebView load, overrides backgroundColorLight/backgroundColorDark.
Determine light/dark mode and set appropriate color. 

Type:   Array

[Red,Green,Blue,Alpha]

Values

Red       red value                   0-255  
Green  green value                0-255  
Blue     blue  value                 0-255  
Alpha   transparency value   0-1 



```javascript
viewPropJSON = '{"backgroundColor":[1,255,3,1] }';
```


**backgroundColorLight**

Sets primary view background color that is displayed during WebView load, if mode is light.


Type:   Array

[Red,Green,Blue,Alpha]

Values

Red       red value                   0-255  
Green  green value                0-255  
Blue     blue  value                 0-255  
Alpha   transparency value   0-1 



```javascript
viewPropJSON = '{"backgroundColorLight”:[228,228,228,1] }';
```


**backgroundColorDark**

Sets primary view background color that is displayed during WebView load, if mode is dark.


Type:   Array

[Red,Green,Blue,Alpha]

Values

Red       red value                   0-255  
Green  green value                0-255  
Blue     blue  value                 0-255  
Alpha   transparency value   0-1 



```javascript
viewPropJSON = '{"backgroundColorDark”:[30,30,30,1] }';
```

**tintColor**

Sets Navigation Bar  tint color (bar text etc.) 

Type:   Array

[Red,Green,Blue,Alpha]

Values

Red       red value                   0-255  
Green  green value                0-255  
Blue     blue  value                 0-255  
Alpha   transparency value   0-1 



```javascript
viewPropJSON = '{"tintColor”:[30,30,30,1] }';
```

See Apple UISplitViewController Documentation for additional info.


**barTintColor**

Sets Navigation Bar bar tint color (bar background)  

Type:   Array

[Red,Green,Blue,Alpha]

Values

Red       red value                   0-255  
Green  green value                0-255  
Blue     blue  value                 0-255  
Alpha   transparency value   0-1 


See Apple UISplitViewController Documentation for additional info.


```javascript
viewPropJSON = '{"barTintColor”:[30,30,30,1] }';
```

**topColumnForCollapsingToProposedTopColumn**

Provides the column to display after the split view interface collapses.

Type:   String

The default is “default”.

 Values

default                      Use “proposedTopColumn”, the column proposed by split view.
primary                     Use primary view.                    
secondary                Use secondary view.                    
supplementary         Use supplementary view.                    
compact                   Use compact view.                    


```javascript
viewPropJSON = '{"topColumnForCollapsingToProposedTopColumn":"primary" }';
```

See Apple UISplitViewControllerDelegate Documentation for additional details.



**displayModeForExpandingToProposedDisplayMode**

Provides the display mode to use after the split view interface expands.

Type:   String

The default is “default”.

 Values

default                            Use “proposedDisplayMode”, the mode proposed by split view.
secondaryOnly              Only secondary view shown.
oneBesideSecondary    Sidebar appears beside secondary view.
oneOverSecondary       Sidebar on top of the secondary view, secondary view partially visible.
twoBesideSecondary    Two sidebars beside secondary view.
twoOverSecondary        Two sidebars on top of the secondary view, secondary view partially visible.
twoDisplaceSecondary  Two sidebars displace  secondary view, moving it partially offscreen.
            

```javascript
viewPropJSON = '{"displayModeForExpandingToProposedDisplayMode":"oneOverSecondary" }';
```

See Apple UISplitViewControllerDelegate Documentation for additional details.


**tabBarItems**

Title, Image pairs for TabBar  Items

Type:   Array

[Title,Image]

Values

Title       Title of bar Item.
Image     Image of bar Item. 


```javascript
viewPropJSON = '{"tabBarItems":["title1","1.circle","title2","2.circle","title3","3.circle"] }';
```


**tabItemsAppend**

The TabBar sends a  message containing a “decorated" selected-item index to the TabBar handler.
 The string array  “tabItemsAppend” has two entries. The first array value is prepended to the selected-item index, the second is appended. 

Type:   Array
[preString,appendString]

 
preString           prepended to the selected-item index
appendString    appended to the selected-item index


The following prepends a “1” to the selected-item index.  Selecting the first item would send “10”. 

```javascript
viewPropJSON = '{“tabItemsAppend":["1",""]  }';
```


**selectedTabIndex**

Set tab index

Type:   Number

The default is 0.

```javascript
viewPropJSON = '{"selectedTabIndex”:1 }';
```




## Embedding Option 


Embeds plugin in a native app.  Using the Embedding Option with the plugin creates a hybrid app and eliminates the startup delay of creating an extra web view. 

The Embedding Option requires a native app into which Cordova is embedded.  See the Embedding Demo for an example.




## EmbedSplitColumn

Create and (if needed)  retain a reference to  EmbedSplitColumn. 

```objective-c
EmbedSplitColumn * es = [[EmbedSplitColumn alloc] init];
```

### showView

```swift
func showView(_ appWindow: UIWindow)
```
**Summary**

shows Split View  Controller as root view controller  of appWindow

**Parameters**
| Param | Description |
| --- | --- |
| appWindow | application window for split view |


##  Properties


**splitViewJSON**
**primaryViewJSON**
**secondaryViewJSON**
**supplementaryViewJSON**
**compactViewJSON**

```swift

splitViewJSON: String 
primaryViewJSON: String 
secondaryViewJSON: String 
supplementaryViewJSON: String 
compactViewJSON: String 
```

Post-iOS 14 embedding sets properties via a JSON string.   See Javascript Properties for details.


```objective-c
   EmbedSplitColumn.splitViewJson = @"{\"isEmbedded\":true,\"primaryTitle\":\"Primary\",\"primaryURL\":\"indexTriple.html\",\"topColumnForCollapsingToProposedTopColumn\":\"primary\", \"secondaryTitle\":\"Secondary\",\"secondaryURL\":\"indexTriple2.html\", \"Style\":\"tripleColumn\",\"backgroundColorLight\":[228,228,228,1],\"backgroundColorDark\":[30,30,30,1], \"showsSecondaryOnlyButton\":true,\"preferredDisplayMode\":\"twoBesideSecondary\",\"supplementaryTitle\":\"Supplementary\"}";
    [es showView:self.window ];
```




**splitViewController** 

```swift
var splitViewController: RtViewController 
```

RtViewController is the root view controller which exposes subviews for  modification above and beyond what the Javascript API offers.




To demo the embedded Split View, in the SplitDemo file AppDelegate.m comment out the current code and use the code that is currently commented out.  Post-iOS 14 multi-column Demo for the new stuff, Classic for the old.   A real app would be structured differently: the embedding demo was constructed to fit in a Cordova-generated app. 

Here’s the demo code that launches the iOS 14 embedded split view:


```objective-c


//
// Post-iOS 14 multi-column Demo
//
#import "AppDelegate.h"
#import "MainViewController.h"
#import "SplitDemo-Swift.h"

@implementation AppDelegate

@synthesize window;

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
{
    CGRect screenBounds = [[UIScreen mainScreen] bounds];

    self.window = [[UIWindow alloc] initWithFrame:screenBounds];
    self.window.autoresizesSubviews = YES;

    EmbedSplitColumn * es = [[EmbedSplitColumn alloc] init];
     
    es.splitViewJson = @"{\"isEmbedded\":true,\"primaryTitle\":\"Primary\",\"primaryURL\":\"indexTriple.html\",\"topColumnForCollapsingToProposedTopColumn\":\"primary\", \"secondaryTitle\":\"Secondary\",\"secondaryURL\":\"indexTriple2.html\", \"Style\":\"tripleColumn\",\"backgroundColorLight\":[228,228,228,1],\"backgroundColorDark\":[30,30,30,1], \"showsSecondaryOnlyButton\":true,\"preferredDisplayMode\":\"twoBesideSecondary\",\"supplementaryTitle\":\"Supplementary\"}";
    [es showView:self.window ];
    
    return YES;
}

@end

```



# Classic Split View

Shows two WebViews (or an optional primary table view) framed as an iOS split view.  
A classic split view consists of two related views:  a primary view and a secondary view.  The views can be displayed as columns if screen real estate permits.
Classic split view is the only option for supporting pre-iOS14 devices. 

The plugin can simulate a split view as the app window's root view or using the “embedding” option present the split view as a true root view.

The Demo App shows the available plugin options, as well as using the plugin "embedded" (Native app with a Cordova-enabled WebView component.)




![ ](https://raw.githubusercontent.com/j-crosson/cordova-plugin-split-view/main/images/landsc.png)
![ ](https://raw.githubusercontent.com/j-crosson/cordova-plugin-split-view/main/images/portrait.png)


## Parent view methods


### show
```javascript
cordova.plugins.SplitView.show(primaryURL, secondaryURL, success, error)
```

Show modal split view

Set attributes before calling.  


| Param | Type | Description |
| --- | --- | --- |
| primaryURL | String | URL for primary view.  Default is index1.html |
| secondaryURL | String | URL for secondary view.  Default is index1.html |
| onSuccess | Function | Success callback function|
| error | Function | Error callback |


### initSplitView
```javascript
cordova.plugins.SplitView.initSplitView()
```

Initialize split view

Must be called at least once before “show”.  Sets attributes to defaults.  

## Primary view methods


### primaryItemSelected
```javascript
cordova.plugins.SplitView.primaryItemSelected(itemString)
```

Notifies Secondary View of action in Primary View

| Param | Type | Description |
| --- | --- | --- |
| itemString | String | Notification data for secondary view |


## Secondary view methods

### initSecondary
```javascript
cordova.plugins.SplitView.initSecondary(itemString)
```

Typically called  immediately after "device ready”. Call when ready to receive messages from Primary view.



### sendResults
```javascript
cordova.plugins.SplitView.sendResults(resultsString)
```

Return results to Parent View


| Param | Type | Description |
| --- | --- | --- |
| resultsString | String | Returned results |



## Classic Split View Properties


| Property | Type | Default |
| --- | --- | --- |
| primaryTitle | string |   |
| secondaryTitle | string |   |
| leftButtonTitle | string |   |
| rightButtonTitle | string |   |
| useTableView | bool | false |
| displayModeButtonItem | bool | true |
| fullscreen | bool | false |
| preferredPrimaryColumnWidthFraction | number | automaticDimension |
| minimumPrimaryColumnWidth | number | automaticDimension |
| maximumPrimaryColumnWidth | number | automaticDimension |
| closed | function |   |
| selected | function |   |


<strong>primaryTitle</strong>

Set  primary view NavigationBar title

```javascript
cordova.plugins.SplitView.primaryTitle = "Primary";
```

<strong>secondaryTitle</strong>

Set  secondary view NavigationBar title

```javascript
cordova.plugins.SplitView.secondaryTitle = "Secondary";
```

<strong>leftButtonTitle</strong>

Sets primary view NavigationBar left button title. If a title is not provided, the button is not shown

```javascript
cordova.plugins.SplitView.leftButtonTitle = “Left”;
```

<strong>rightButtonTitle</strong>

Sets primary view NavigationBar right button title. If a title is not provided, the button is not shown

 ```javascript
 cordova.plugins.SplitView.rightButtonTitle = “Right”;
```

<strong>useTableView</strong>

Use Table View as Primary view (true) or WebView (false)
Default is WebView

```javascript
cordova.plugins.SplitView.useTableView = true;
```

<strong>displayModeButtonItem</strong>

Changes display mode.  See Apple UISplitViewController Documentation for additional details.

```javascript
cordova.plugins.SplitView.displayModeButtonItem= false;
```

<strong>fullscreen</strong>

Changes presentation style of split view to full screen.   

Set this to make the split view full screen.  This is necessary to simulate a root view. 

```javascript
cordova.plugins.SplitView.fullscreen= true;
```

The Width properties are handled automatically by iOS unless overridden by the following properties:

<strong>preferredPrimaryColumnWidthFraction</strong>

Preferred relative width of the primary view.   Number between 0.0 and 1.0   Percentage of the overall width of the split view.
See Apple UISplitViewController Documentation for additional details.

```javascript
cordova.plugins.SplitView.preferredPrimaryColumnWidthFraction= 0.5;
```


<strong>minimumPrimaryColumnWidth</strong>

Sets min width, in points, of the primary view. See Apple UISplitViewController Documentation for additional details.

```javascript
cordova.plugins.SplitView.minimumPrimaryColumnWidth = 100.0
```

<strong>maximumPrimaryColumnWidth</strong>

Sets max width, in points, of the primary view . See Apple Documentation for UISplitViewController.

```javascript
cordova.plugins.SplitView.maximumPrimaryColumnWidth = 100.0
```


### barTintColor
```javascript
cordova.plugins.SplitView.barTintColor(red,green,blue)
```

Sets Navigation Bar bar tint color (bar background) 
See Apple Docs for additional details.

| Param | Type | Description |
| --- | --- | --- |
| red | Number | red 0-255 |
| green | Number | green 0-255 |
| blue | Number | blue 0-255 |



### tintColor
```javascript
cordova.plugins.SplitView.tintColor(red,green,blue)
```

Sets Navigation Bar  tint color (bar text etc.) 
See Apple Docs for additional details.

| Param | Type | Description |
| --- | --- | --- |
| red | Number | red 0-255 |
| green | Number | green 0-255 |
| blue | Number | blue 0-255 |


### primaryBackgroundColor
```javascript
cordova.plugins.SplitView.primaryBackgroundColor(red,green,blue)
```

Sets primary view background color

| Param | Type | Description |
| --- | --- | --- |
| red | Number | red 0-255 |
| green | Number | green 0-255 |
| blue | Number | blue 0-255 |


### secondaryBackgroundColor
```javascript
cordova.plugins.SplitView.secondaryBackgroundColor(red,green,blue)
```

Sets secondary view background color

| Param | Type | Description |
| --- | --- | --- |
| red | Number | red 0-255 |
| green | Number | green 0-255 |
| blue | Number | blue 0-255 |

## Callbacks

### closed

 function ( results,status)

| Param | Type | Description |
| --- | --- | --- |
| results | String |results returned on close|
| status | enum | results status |

**results**

String sent by “sendResults” in secondary view.

**status**

| Value  | Status |
| --- | --- |
|SplitView.dismissType.swipe | Dismissed by swipe|
|SplitView.dismissType.left | Dismissed by left button|
|SplitView.dismissType.right | Dismissed by right button|

Only available in parent view.

```javascript
var onViewClosed = function ( results,status) {
    if(status == cordova.plugins.SplitView.dismissType.left) {
        //do something
    }
}

cordova.plugins.SplitView.closed = onViewClosed;
```

### selected

 function ( itemString)

| Param | Type | Description |
| --- | --- | --- |
| itemString | String | selection string |

**itemString**

String sent in primary view by “primaryItemSelected”. Typically reflects an item selection but could be any action.

Only available in secondary view.

```javascript
var onSelected = function ( itemString) {
    //do something
}

cordova.plugins.SplitView.selected= onSelected;
```



## Embedding Option — Classic Split View

Embed plugin in a native app.  Using the Embedding Option with the plugin creates a hybrid app and eliminates the startup delay of creating an extra web view. 
Embedded split view classic only supports a two-webview split view.  The tableview option is not supported.  

The Embedding Option requires a native app into which Cordova is embedded.  See the demo for an example.

### show

```swift
func show(_ appWindow: UIWindow)
```
**Summary**

shows Split View  Controller as root view controller  of appWindow

**Parameters**
| Param | Description |
| --- | --- |
| appWindow | application window for split view |

***
In the non-embedded  version,  the initial background colors of the primary and secondary views, the colors briefly displayed during WebView load,  are set by the parent WebView/Media Query.  Since the embedded case doesn’t have a parent WebView, the plugin determines light/dark mode and chooses the supplied light or dark color.  Versions of iOS that don’t support dark mode will default to light. 

### setPrimaryBackgroundColor

```swift
func setPrimaryBackgroundColor(_ light: UIColor, _ dark: UIColor) 
```
**Summary**

sets primary view background color that is displayed during WebView load. 

**Parameters**
| Param | Description |
| --- | --- |
| light | background color in light mode |
| dark | background color in dark mode |

### setSecondaryBackgroundColor

```swift
func setSecondaryBackgroundColor(_ light: UIColor, _ dark: UIColor)
```

**Summary**

sets secondary background color that is displayed during WebView load. 

**Parameters**
| Param | Description |
| --- | --- |
| light | background color in light mode |
| dark | background color in dark mode |

***

### Properties

**primaryURL**

URL of Primary View content.

```swift
var primaryURL: String
```

  The default is “index1.html”

```swift
    embedSplit.primaryURL = @"index1.html”;   //objective-c
    embedSplit.primaryURL= "index1.html"      // swift
```
  
**secondaryURL**

URL of Secondary View content.

```swift
 var secondaryURL: String
```

The default is “index2.html”

```swift
    embedSplit.secondaryURL = @"index2.html”;   //objective-c
    embedSplit.secondaryURL= "index2.html"      // swift
```

**primaryTitle**

Title of primary view.

```swift
 var primaryTitle: String
```

```swift
    embedSplit.primaryTitle = @"Primary";   //objective-c
    embedSplit.primaryTitle = "Primary"     // swift
```

**secondaryTitle**

Title of secondary view.

```swift
var secondaryTitle: String
```

```swift
    embedSplit.secondaryTitle = @"Secondary";   //objective-c
    embedSplit.secondaryTitle = "Secondary"     // swift
```

**leftButtonTitle**

Title of left button.
If a title is not provided, the button is not shown.

```swift
var leftButtonTitle: String
```

```swift
    embedSplit.leftButtonTitle = @“Left”;   //objective-c
    embedSplit.leftButtonTitle = “Left”     // swift
```

**rightButtonTitle**

Title of right button.
If a title is not provided, the button is not shown.

```swift
var rightButtonTitle: String
```

```swift
    embedSplit.rightButtonTitle = @“Right”;   //objective-c
    embedSplit.rightButtonTitle = “Right”     // swift
```
***
The Width properties are handled automatically by iOS unless overridden by the following properties:
***

**primaryColumnWidthfraction**

```swift
var primaryColumnWidthfraction: CGFloat 
```

Preferred relative width of the primary view controller’s content
See Apple’s docs for details

```swift
    embedSplit.primaryColumnWidthfraction = 0.5;   //objective-c
    embedSplit.primaryColumnWidthfraction = 0.5    // swift
```

**minimumPrimaryColumnWidth**

```swift
var minimumPrimaryColumnWidth: CGFloat 
```

In points, the minimum width for the primary view controller’s content
See Apple’s docs for details

```swift
    embedSplit.minimumPrimaryColumnWidth = 200.0;   //objective-c
    embedSplit.minimumPrimaryColumnWidth = 200.0    // swift
```

**maximumPrimaryColumnWidth**

```swift
var maximumPrimaryColumnWidth: CGFloat
```

In points, the maximum width for the primary view controller’s content
See Apple’s docs for details

 ```swift
     embedSplit.maximumPrimaryColumnWidth = 200.0;   //objective-c
     embedSplit.maximumPrimaryColumnWidth = 200.0    // swift
 ```

***

**showDisplayModeButtonItem**

```swift
var showDisplayModeButtonItem: Bool
```

Show button that changes the split view controller display mode 

Default is TRUE

```swift
    embedSplit.showDisplayModeButtonItem = false;   //objective-c
    embedSplit.showDisplayModeButtonItem = false        // swift
```



To demo the Split View, in the SplitView Demo file AppDelegate.m comment out the current code and use the classic-view code that is currently commented out. A real app would be structured differently: the embedding demo was constructed to fit in a Cordova-generated app. 

Here’s the demo code that launches the classic embedded split view:


```objective-c

#import "AppDelegate.h"
#import "MainViewController.h"
#import "SplitDemo-Swift.h"

@implementation AppDelegate

@synthesize window;

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
{
    CGRect screenBounds = [[UIScreen mainScreen] bounds];

    self.window = [[UIWindow alloc] initWithFrame:screenBounds];
    self.window.autoresizesSubviews = YES;

    EmbedSplit * es = [[EmbedSplit alloc] init];
    UIColor *colorLight = [UIColor colorWithRed:0.894 green:0.894 blue:0.894 alpha:1];
    UIColor *colorDark = [UIColor colorWithRed:0.12 green:0.12 blue:0.12 alpha:1];
    [es setPrimaryBackgroundColor:colorLight :colorDark];
    [es setSecondaryBackgroundColor:colorLight :colorDark];
    es.primaryTitle = @"Primary";
    es.secondaryTitle = @"Secondary";
    [es show:self.window ];
    
    return YES;
}

@end
```

