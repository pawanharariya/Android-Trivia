# Android Trivia #
This is a trivia app with questions on android. You can answer the questions and also share results at the end. The app uses various Navigation components like navigation drawer, navigation graph, navigation UI, overflow menu and is built using fragments as UI components.

### App Preview ###

![android_trivia_preview1](https://github.com/pawanharariya/Android-Trivia/assets/43620548/9ca1dffe-1e49-4501-b14f-2df75730416c)
![android_trivia_preview2](https://github.com/pawanharariya/Android-Trivia/assets/43620548/c3a0109b-6415-4673-af9f-9a8ec820ab98)
![android_trivia_preview3](https://github.com/pawanharariya/Android-Trivia/assets/43620548/bec80361-c3bf-4bad-86d7-439ac257a5b3)
![android_trivia_preview4](https://github.com/pawanharariya/Android-Trivia/assets/43620548/766aa60a-e26f-497c-bd80-69fbab79c502)
![android_trivia_preview5](https://github.com/pawanharariya/Android-Trivia/assets/43620548/963dbcad-5228-4f2e-8518-2f0cb89f5ddc)
![android_trivia_preview6](https://github.com/pawanharariya/Android-Trivia/assets/43620548/324cf589-5acb-48be-a97d-dc3b2cd8f0eb)


## Navigation Terms ##
**Action Bar** - Appears at the top of the application screen. Contains application branding and navigation features such as the overflow menu and the navigation drawer button.

**Up/Back Button** - Appears in the action bar and takes us back through previous screens, the user has navigated to, within the app.

**Overflow Menu** - A drop down list of items within the Action Bar that can contain navigation destinations.

**Navigation Drawer** - A menu with a header that slides out from the side of the app.

**Navigation Graph** - Its a graph of all of the destinations/screens that can be navigated to, from a single activity.

## Fragments  ##
Fragments are reusable components, used for dynamic and flexible UI design. Fragments are like views contained inside activity along with UI elements that are part of activity. 
Activities inherit from context class, but fragments don't, so we need to use context propety in fragment to use app data such as string or image resources.

## Back Stack ##
When navigating through multiple activities the previous activities are put on to a stack called back stack. And, hitting the back button pops out the activities from stack. For fragments, there is a separate stack called fragment back stack and the entire stack is contained within the activity. The fragment back stack is controlled by Fragment Manager. We can also choose whether to put a fragment onto the stack or not.

## Navigation Principles ##
We use navigation components and navigation graph to perform nativation tasks in a consistent way, and follow navigation principles listed below:
1. App should have a fixed starting point, and this destination should also be the last screen before exiting the app.
2. One should always be allowed to move back to previous screen following LIFO stack.
3. The UP button `<-` in action bar should take the user to the previous screen, and should be consistent with system back button. However it shouldn't appear on the home screen.

## Navigation Components ##
**Navigation Graph** - We add fragments to nav graph and connect them using actions. Actions represent possible paths in a graph. 
**Nav Host Fragment** - It acts as host for fragments in the activity's navigation graph. As user moves to different screens in navigation graphs, the fragment in Nav Host is swaped in and out and a stack is maintained. The nav host should be part of activity's layout and the nav graph should be attached to it.
**Navigation Controller** - It manages the navigation within the nav host fragment. We can use `findNavController` helper funtion to find the appropriate navHostFragment attached to the view and get its navigation controller. Nav controller triggers the actions in navigation graph and helps in navigating to destinations.

## Overflow Menu ##
An overflow menu is a set of options that is shown when the user click the 3 dots on the action bar. The menu items can navigate to the fragments/destinations in nav graph. The Navigation UI can help to navigate to destination by matching the `id` of the menu item to the fragment's `id` in the navigation graph, hence navigating through menu doesn't require actions.

## Safe Arguments ##
Arguments are way to share data across fragments. Fragments contain arguments in the form of Android Bundle (key-value pair). We create a bundle in a fragment, add arguments to it in form of key-value pair and  attach the bundle to the fragment. When another fragment is called from this fragment, the arguments are passed. We than query the bundle in the other fragment. This approach is however not type safe. Hence navigation provides a better way called **safe args**.

Safe args is gradle plugin that helps to guarantee that arguments on both sides match, and simplifies argument passing. Safe args provide type safety, as navigation generates the action and arguments class from navigation graph. It also provides argument enforcement, as non-default arguments are required parameters in the action.

## Intents ##
Intents are a way to navigatie between activities of our app, and to activities of other apps. For example we can use Camera Activity od the system app to capture an image for our app. An Intent indicates intention of the app and describes what an activity want to perform. Intents are of two types explicit and implicit intents.

### Explicit Intent ###
It is used to launch a specific activity using the name of target activity class. It is mostly used to launch other activities within our app. We can also use Navigation Component to navigate to other activities in the navigation graph.

### Implicit Intentes ### 
They are used to launch activities exposed by other applications. Implicit Intents are used to perform an operation by providing an description of the operation, and then the Android Sytem launches the particular app that can handle this operation. When multiple apps can handle the intent, Android System shows a chooser, so that user can choose the desired app. It may also happen that the user's phone may not have any app that can handle the intent. 

Intent action describes the type of thing the app wants to be done i.e. what the intention is. For example `ACTION_VIEW`, `ACTION_DIAL`, `ACTION_EDIT` are some common actions. Intents can also include data like text or image.

### Intent-Filters ###
All activities must be registered in the Android Manifest to be launched. Activites that are only lauched explicitly can be declared with just `<activity>` tag. But implicitly lauched activities require Intent Filter.  An Intent Filter is used to expose that our activity can handle implicit intents with particular action, category andd data type. For Android System Launcher to launch an activity, it must also have an intent filter with action as `MAIN` and category as `LAUNCHER`. Hence all app's main activity has launcher intent filter.

### Resolving Intents using Package Manager ###
It may happen that the user's phone may not have any app that can handle a particular intent, in such cases it leads to a `ActivityNotFoundException`. To handle this we can catch the expection and display revelant message. A better way is to use package manager to which whether any app that can handle the intent exist on user's device or not, and then hide any options which generates the intent.

Package Manager is an Android System service which we can use to check if the intent resolves to an activity. Package Manager knows about every activity registered in the AndroidManifest across every application. 


## Quick Tips ##
1. `app:defaultNavHost="true"` property can be set to nav host fragment so that it intercepts the system back key.
2. Attach navigation graph to nav host fragment using `app:navGraph` property to access the nav controller from any destination in nav graph.
3. Actions can be used to manipulate the back stack before moving to the destination. Use `popTo` to remove fragments on back stack upto a particular fragment.
4. Use NavigationUI and link nav controller to Action Bar to navigate back using Up button in Action Bar.
5. The `showAsAction` property of a menu item can be used to display the item as an icon in the action bar, if there is space available.
6. Use `ShareCompat` Intent Buider class provides an easy way, to build a sharing intent.
