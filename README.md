# Sketch Squarespace Data Populator
> A Sketch App plugin to populate your documents with content from a Squarespace website.

> This repo is a fork of the origin plugin, with a few examples we built from a Squarespace website. We're still in the progress of adding examples and building our Squarespace JSON export tool.



## Overview
All too often, designers use Lorem Ipsum text and stock images to craft designs. On top of that, mocking up content is sometimes hard. This Sketch App plugin will let you import JSON data directly into Sketch.



## Why JSON?
Well, it's much easier to work with. Instead of typing out content into Sketch, or finding images and dropping them in, you can use placeholders like `{title}`, `{excerpt}`, or `{image}`. Then you can use this data populator plugin to load that content directly into Sketch. It's beautiful.



## Installation
1. Download the ZIP file (or clone repository)
2. Move the file ```Sketch Data Populator.sketchplugin``` into your Sketch Plugins folder. In Sketch 3, choose **Plugins › Reveal Plugins Folder…** to open it.



## How to use …

The **Sketch Data Populator** plugin creates a grid from a selected element (Layer Group or Artboard) and replaces text and image {placeholders} with data from a JSON source:

### Here's how it works:

1. Create a Layer Group that contains at least one Text Layer. In these Text Layers, use placeholders for you data fields in curly brackets – such as ```{firstname}``` or ```{lastname}```. Within a Text Layer, you can do arbitrary string concatenation such as ```{lastname}, {firstname}```. The plugin's "Populate with …" command will replace all these placeholders with respective data.

2. In the same Layer Group, create a Shape Layer (this is your image placeholder). Give the Shape Layer a placeholder name in curly brackets – such as ```{image}```. The plugin's "Populate with …" command will replace this placeholder with respective image data (PNG, JPG).

3. Create another Shape Layer as your icon placeholder. Give it a placeholder name in double curly brackets, something like ```{{icon}}```. Set any of its properties like size, fill color or shadow as desired – all properties will apply to the final icon once populated. The plugin's "Populate with …" command will replace this placeholder with respective icon vector data (SVG).


### All available Commands:

#### Populate with JSON
will ask you to choose a JSON file that can sit anywhere on your Computer. After picking a JSON file you can configure Data and Layout options:

![Populate with JSON](populate-with-json-dialog.png)

#### Populate with Preset
will display a dialog that allows you to select one of your Presets as well as configure Data and Layout options:

![Populate with Preset](populate-with-preset-dialog.png)

**Data options**  
* _Randomize data order_: instead of going through the JSON top down row by row, it will pick a random data set.  
* _Trim overflowing text_: a Text Layer that has been set with a fixed width will trim overflowing text.  
* _Insert ellipsis after trimmed text_: will insert a "…" after the trimmed text.  
* _Default substitute_ (see below)  

**Handling missing data**  

_Text Substitutes_  
`{placeholder}` inserts an empty string if no data are available for placeholder  
`{placeholder?}` uses the _Default substitute_  
`{placeholder?substitute}` uses the custom substitute you append after the "?"

_Image & SVG Substitutes_  
If there's no image or SVG available, it will turn off the fill of the placeholder shape and turn it on again once there's data available when re-populating. So for images, it's recommended to put a substitute image or pictogram behind the actual image. So this will be visible if there's no actual image data (see "demo.sketch" for examples).

**Layout options**  
If "Create grid" is checked, the plugin will create a grid from selected elements (Layer Groups or Artboards) and populate them in one go. Set the amount of rows and columns and the respective margins. This option works very similar to Sketch's "Make Grid" tool.

#### Populate again (⌘⇧X)
re-populates all selections with the last used Preset/JSON and options configuration. Great for "shuffling" through different data sets.

#### Restore Placeholders
restores populated Text Layers to their initial {placeholders}. An example: you used the placeholders "{firstname} {lastname}" in a Text Layer, they became "John Doe" after populating. "Restore Placeholders" will restore to "{firstname} {lastname}". This is useful because populating a Text Layer means the initially used {placeholders} will be persisted – so without restoring, it would always try to populate the initial {placeholders}, no matter what you type into the field.

#### Place SVG
will prompt you for picking a SVG asset on your computer. It will replace the selected shape and adapt its properties (like size, color, shadow …).

#### Place image
will prompt you for picking an image on your computer and then use it as the background for the selected shape.

#### Reveal Presets
will point you into the plugin's location for its Presets. Presets are simply JSON files and folders with image assets that live inside the plugin bundle. In there, you can use any desired folder structure. To find the "Preset" folder inside the plugin bundle, right click _Sketch Data Populator.sketchplugin_ and select _Show Package Contents_.

---

Check out the **demo.sketch** file to get an idea.

---

### Data format & assets

The data need to be stored in JSON files that can be loaded by the plugin from either the Presets Folder (Populate with Preset) or from any folder on your computer (Populate with JSON). The data in JSON need to be in an array like in this example:

```json
[
  {
    "id": 1,
    "firstname": "Willie",
    "lastname": "Willis",
    "company": "Myworks",
    "job": "Marketing Assistant",
    "email": "wwillis0@cdc.gov",
    "phone": "9-(528)011-1428",
    "address": "99 Hallows Terrace",
    "city": "Outeiro",
    "country": "Portugal",
    "image": "assets/1.jpg",
    "icon": "assets/vip.svg"
  },
  {
    "id": 2,
    "firstname": "Melissa",
    "lastname": "Flores",
    "company": "Tagtune",
    "job": "Actuary",
    "email": "mflores1@jigsy.com",
    "phone": "4-(965)937-9250",
    "address": "46 Acker Trail",
    "city": "Santiago",
    "country": "Philippines",
    "image": "assets/2.jpg",
    "icon": "assets/vip.svg"
  }
]
```

Note that in the example the image file (JPG) and the icon (SVG) are referenced from a folder called _assets_. This means all your image and icon data should be placed inside a folder that sits on the same level as your JSON file. The images/icons folders as well as your images and icons can be named anything you like, you just need to reference them relative to your JSON file.

You can also use a full URL to reference your images if that is your preference.

<sup>The mock data in "demo" were created with https://www.mockaroo.com, which is a pretty powerful tool to generate all kinds of data. The "products" images are from apple.com, the "contacts" images from https://randomuser.me/ and http://uifaces.com/</sup>



## Getting JSON Data
There's two methods to getting the data for use with this plugin.

1. Manually type out a JSON file and organize your images into subfolders to  creating content presets for various use cases.
2. Exporting JSON from an existing Squarespace website.

We're going to create a few content presets for you, which should give you some great starting points to work from. You'll be able to edit or add your own.

We're also building a JSON export tool. Right now I primarily use a some command line tools to easily get the JSON from Squarespace. We'll have more on this later as we build out this repo.



## Testing & Credits

Please report bugs, observations, ideas & feature requests as [issues](https://github.com/preciousforever/sketch-data-populator/issues) or [get in touch](mailto:feedback@datapopulator.com).

We conceived _Sketch Data Populator_ to improve our design process for working with data at [precious design studio](http://precious-forever.com/) and developed the plugin in collaboration with [Lukas Ondrej](https://github.com/lukasondrej). Please get in touch if you have questions or comments via [@preciousforever](https://twitter.com/preciousforever) or [our website](http://precious-forever.com/contact).