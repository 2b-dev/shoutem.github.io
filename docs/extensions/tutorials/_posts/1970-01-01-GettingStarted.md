---
layout: doc
permalink: /docs/extensions/tutorials/getting-started
title: Getting Started
section: Tutorials
---

# Getting Started

Shoutem is a platform that enables you to build, publish and manage high-quality native iOS and Android apps. It's built on top of React Native and open sourced for developers. The philosophy behind Shoutem is to let you build apps efficiently without restricting you on how to use React Native.

## Apps and Extensions

The efficiency of building apps is achieved with a simple architecture: apps are built using smaller modules called `extensions`. An extension is a self-contained and complete functionality that can be reused. Everything in the app is an extension: navigation, places (list and details), push notifications, analytics, ads, etc...

<p class="image">
<img src='{{ site.url }}/img/tutorials/getting-started/apps-are-made-of-extensions.png'/>
</p>

Shoutem prepared and [open sourced](https://github.com/shoutem/extensions) a lot of extensions that you can use in your apps. **Don't reinvent the wheel**: reuse extensions which are suitable for your app, customize them or create new ones. It's the world-first WordPress-like solution for mobile apps.

## The Builder

Shoutem apps are managed on a beautiful web interface called the **Builder**. It allows you to host your project online and make it customizable for non-technical people, which is perfect for a developer's clients. It also allows developers to save time setting up a part of their app so they can focus on their own unique features.

## Your First App

#### Prerequisites

Before going through this tutorial, make sure you've installed the following:

- [Node.js and npm](https://www.npmjs.com/) (installing `Node.js` also installs `npm`)
- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- react-native-cli - `$ npm install -g react-native-cli`
- shoutem-cli - `$ npm install -g @shoutem/cli`

> #### Note
> If the `npm install` commands fail because of _permission_ issues, you need to run them with `sudo`: `sudo npm install -g <package-name>`.

If you haven't already, go to the [Builder]({{ site.shoutem.builderURL }}) and create an account. Once signed in, create a new `Blank app`. For this quick tutorial, we'll make a Restaurants and Food app, let's call it `Restaurants`. To rename your app, click on the `Blank app` text, delete it and type in `Restaurants`.

Let's say we want to add an RSS feed screen to our app. To do that, click on the + button next to Screens and select the News RSS extension. Since the app is about Restaurants, to stick to the Food theme, let's use a food related News RSS feed:
http://foodengineeringmag.com/rss/topic/2639-top-100-food-beverage-companies

After you add this screen, it should look something like this:

<p class="image">
<img src='{{ site.url }}/img/tutorials/getting-started/01-builder-before-clone.png'/>
</p>

## Creating a New Extension

As a developer, you use the Shoutem CLI to handle the lifecycle of extensions.

Start by using the `shoutem login` command with your Shoutem credentials ("{{ site.example.devName }}" is used as a developer name in this example).

```ShellSession
$ shoutem login
Enter your Shoutem credentials (obtained at {{ site.shoutem.builderURL }}):
Email: {{ site.example.devEmail }}
Password:

Logged in as {{ site.example.devEmail }}.
Enter developer name.
Developer name: {{ site.example.devName }}

Registered as `{{ site.example.devName }}`.
```

Clone the app you made in the Builder to your machine by using `shoutem clone` and selecting your app from the list:

```ShellSession
$ shoutem clone
Select your app: Restaurants ({{ site.example.appId }})
Cloning `Restaurants` to `Restaurants`
...
```

`shoutem clone` turns your app you see on the Builder into a Shoutem flavored React Native app locally. Once the cloning process is done, locate to `Restaurants/extensions` (where you can find all the extensions installed into your app) and create your new extension using `shoutem init`:

```ShellSession
$ cd Restaurants/extensions
$ shoutem init restaurants
Enter information about your extension. Press `return` to accept (default) values.
Title: Restaurants
Version: 0.0.1
Description: A restaurants extension.

Initializing extension:
...

Extension initialized!
```

The `shoutem init` command bootstrapped the `{{ site.example.devName }}.restaurants` folder with extension files. Let's add a screen that we'll use as a list of restaurants in the My first extension tutorial series, so we'll name it `List` and give it a shortcut `Restaurants`:

```ShellSession
$ cd {{ site.example.devName }}.restaurants
$ shoutem screen add List --shortcut Restaurants
Enter shortcut information:
Title: Restaurants

Screen `List` is created in file `app/screens/Hello.js`!
Shortcut `Restaurants` is created!
Shortcut `Restaurants` opens `List` screen.
File `app/extension.js` was modified.
File `extension.json` was modified.
```

This created a `List` screen in `app/screens/List.js` file. Any time you make a new screen it'll be a simple _Hello World_ screen. To fit the app, let's change the screen so it says `Let's eat!` instead of `Hello World!`:

```JavaScript{5}
#file: app/screens/List.js
export default class List extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>Let's eat!</Text>
      </View>
    );
  }
}
```

Now push what we've built to Shoutem with `shoutem push`:

```ShellSession
$ shoutem push
Checking the extension code for syntax errors...
Uploading `Restaurants` extension to Shoutem...
Success!
```

And install the extension into the Restaurants app using `shoutem install`:

```ShellSession
$ shoutem install
Select your app: Restaurants ({{ site.example.appId }})

Extension installed.
See it in the builder: {{ site.shoutem.builderURL }}/app/{{ site.example.appId }}
```

Now we need to add the screen to the app. Open the app in the Builder. Click on the `+` next to **Screens** and select the `Custom` category. You can see your `Restaurants` extension there. Click on it to add it's screen to Main navigation, just like you did with the News RSS.

<p class="image">
<img src='{{ site.url }}/img/tutorials/getting-started/02-builder-custom-extension-screen.png'/>
</p>

Great! Let's make our newly created extension's screen the Starting Screen for the app. Just drag it to the top of Main navigation and you're done.

Since we just added a new extension to our app, we need to reconfigure the app to link the extension code and utilize it. We do that with `shoutem configure`:

```ShellSession
$ shoutem configure

> @shoutem/mobile-app@1.1.0 configure /path/to/Restaurants
...
```

After that's done, we can preview the app locally using `react-native run-ios` `react-native run-android`. You can also use `shoutem run`, which will make the CLI print a QR code for you to scan with the **Shoutem Preview app** (available for [iOS]({{ site.shoutem.previewAppiOS }}) and [Android]({{ site.shoutem.previewAppAndroid }})). Using the Shoutem Preview app, you can even preview iOS apps when developing on Windows!

```ShellSession
$ shoutem run
Scanning folders for symlinks in /path/to/Restaurants/node_modules
...
```

Once you scan the generated QR code, this is the result you'll have on your phone:

<p class="image">
<img src='{{ site.url }}/img/tutorials/getting-started/03-lets-eat.png'/>
</p>

**Well done!** You just built your first app using your own custom built extension!

## What's next?

To leverage the full power of Shoutem, we'd suggest you go through the [My first extension]({{ site.url }}/docs/extensions/my-first-extension/introduction) tutorial, which explains the underlying concepts in more detail.
