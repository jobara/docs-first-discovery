---
title: Sticky Key Panel
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.panel.keyboard`

**File:** `panels.js`

The Sticky Key panel offers:

1. Assesses whether the user needs the assistance of the sticky key feature;
2. Provides a means for users to experiment the experience when the sticky key preference is turned on or off;
3. Turn the sticky key preference on or off.

## Adding a Sticky Key Panel to a Component/Grade

*Option 1*: Typically the Sticky Key Panel is integrated into the
[First Discovery Tool](https://wiki.fluidproject.org/display/fluid/First+Discovery+Tool+Architecture)
by supplying it in an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
"keyboard": {
    "type": "gpii.firstDiscovery.stickyKeys",
    "panel": {
        "type": "gpii.firstDiscovery.panel.keyboard",
        "container": ".gpiic-fd-prefsEditor-panel-keyboard",
        "template": "%prefix/keyboard.html",
        "message": "%prefix/keyboard.json",
        "gradeNames": ["gpii.firstDiscovery.panel.keyboardTts"]
    }
}
```

Working in conjunction with the Auxiliary Schema, the type and its default value of the
Sticky Key preference are defined in the
[Primary Schema](http://docs.fluidproject.org/infusion/development/PrimarySchemaForPreferencesFramework.html):

```javascript
fluid.defaults("gpii.firstDiscovery.schemas.stickyKeys", {
    gradeNames: ["autoInit", "fluid.prefs.schemas"],
    schema: {
        "gpii.firstDiscovery.stickyKeys": {
            "type": "boolean",
            "default": false
        }
    }
});```

*Option 2*: Outside the context of the First Discovery Tool, developers may wish to create a standalone component:
```javascript
var myPanel = gpii.firstDiscovery.panel.keyboard(container, options);
```

## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.prefs.panel`](http://docs.fluidproject.org/infusion/development/Panels.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `offerAssistance` | Whether or not the sticky key feature should be offered. | Boolean | undefined |
| `tryAccommodation` | Whether or not users select to try the sticky key feature. | Boolean | false |
| `userInput` | The user input. | String | "" |

## Supported Events

| Event  | Type |Description | Parameters | Parameter Description |
|--------|------|------------|------------|-----------------------|
| `onOfferAssistance` | default | Fired when the sticky key feature is determined to be offered. | Boolean |  undefined |
| `onInitInput` | default | Fired when it's time to initialize the [keyboard input](keyboardInput.md) sub-component. | Boolean | false  |

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `toggleAssistance` | Toggles the given state that could be `model.offerAssistance` or `model.tryAccommodation`. | A state |

## Subcomponents

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`assistance`</td>
        <td>Used to turn on/off the sticky key assistance.</td>
        <td>[`"gpii.firstDiscovery.keyboard.stickyKeysAdjuster"`](stickyKeysAdjuster.md)</td>
        <td>
        <pre><code>assistance: {
    type: "gpii.firstDiscovery.keyboard.stickyKeysAdjuster",
    createOnEvent: "onOfferAssistance",
    container: "{that}.container",
    options: {
        messageBase: "{keyboard}.options.messageBase",
        model: {
            tryAccommodation: "{keyboard}.model.tryAccommodation",
            stickyKeysEnabled: "{keyboard}.model.stickyKeysEnabled"
        },
        listeners: {
            "{keyboard}.events.onRenderTree": "{that}.tooltip.close"
        }
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`stickyKeysAssessor`</td>
        <td>Used to assess whether the user needs the help of the sticky key feature.</td>
        <td>[`"gpii.firstDiscovery.keyboard.stickyKeysAssessment"`](stickyKeysAssessment.md)</td>
        <td>
        <pre><code>stickyKeysAssessor: {
    type: "gpii.firstDiscovery.keyboard.stickyKeysAssessment",
    options: {
        requiredInput: "%",
        model: {
            userInput: "{keyboard}.model.userInput",
            offerAssistance: "{keyboard}.model.offerAssistance"
        }
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`keyboardInput`</td>
        <td>Used for the user input.</td>
        <td>[`"gpii.firstDiscovery.keyboardInput"`](keyboardInput.md)</td>
        <td>
        <pre><code>keyboardInput: {
    type: "gpii.firstDiscovery.keyboardInput",
    createOnEvent: "onInitInput",
    container: "{that}.dom.input",
    options: {
        gradeNames: ["gpii.firstDiscovery.keyboardInputTts"],
        model: {
            userInput: "{keyboard}.model.userInput",
            stickyKeysEnabled: "{keyboard}.model.stickyKeysEnabled"
        },
        messageBase: "{keyboard}.options.messageBase"
    }
}</code></pre>
        </td>
    </tr>
</table>

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors) below</td>
    </tr>
</table>

## Selectors

One of the options that can be provided to the First Discovery Editor is a set of CSS-based
selectors identifying where in the DOM different elements can be found. The value for the option
is itself a Javascript object containing name/value pairs:

```javascript
selectors: {
    selector1Name: "selector 1 string",
    selector2Name: "selector 2 string",
      ...
}
```

| Selector Name | Description | Default |
|---------------|-------------|---------|
| `input` | The input field. | `".gpiic-fd-keyboard-input"` |
| `instructions` | The panel instruction. | `".gpiic-fd-keyboard-instructions"` |
| `assistance` | The area for assessing and experimenting the sticky key feature. | `".gpiic-fd-keyboard-assistance"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
```
