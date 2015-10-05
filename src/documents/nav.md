---
title: Navigation
layout: default
category: API
---

## Navigation Overview

Handles the navigation between panels as well as maintaining a set of icons representing each panel.

## Adding a Navigation Component

*Option 1*: Typically used as a sub-component of a Preferences Editor Loader, particularly the
[First Discovery Tool Editor](firstDiscoveryEditor.md).

Adding as sub-component:
```javascript
nav: {
    type: "gpii.firstDiscovery.nav",
    container: "{that}.dom.nav",
    options: {}
}
```

*Option 2*: Adding as a stand alone component::
```javascript
var myNav = gpii.firstDiscovery.nav(container, options);
```


## Grades

The base [grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)
used by the the First Discovery Editor:

* [`fluid.viewRelayComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Model

| Path   | Description | Values | Default |
|--------|-------------|--------|---------|
| `currentPanelNum` | The panel currently displayed | Panel ID (Number) | 1 |

## Subcomponents

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`navButtons`</td>
        <td>Specifies the component to manage the buttons and their states for navigating between panels</td>
        <td>[`"gpii.firstDiscovery.navButtons"`](navButtons.md)</td>
        <td>
        <pre><code>navButtons: {
    type: "gpii.firstDiscovery.navButtons",
    container: "{that}.dom.navButtons",
    options: {
        model: {
            currentPanelNum: "{nav}.model.currentPanelNum"
        },
        messageBase: "{nav}.options.messageBase",
        styles: "{nav}.options.styles",
        panelTotalNum: "{nav}.options.panelTotalNum"
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`navIcons`</td>
        <td>Specifies the component which is responsible for displaying the panel icons and managing their state</td>
        <td>[`"gpii.firstDiscovery.navIcons"`](navIcons.md)</td>
        <td>
        <pre><code>navIcons: {
    type: "gpii.firstDiscovery.navIcons",
    container: "{nav}.dom.navIcons",
    options: {
        model: {
            currentPanelNum: "{nav}.model.currentPanelNum"
        },
        styles: "{nav}.options.styles"
    }
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`stepCount`</td>
        <td>Specifies the component responsible for displaying the current step message. ( I.E. a textual indicator of the current panel id and progress. )</td>
        <td>`"gpii.firstDiscovery.stepCount"`</td>
        <td>
        <pre><code>stepCount: {
    type: "gpii.firstDiscovery.stepCount",
    container: "{that}.dom.stepCount",
    options: {
        messageBase: "{nav}.options.messageBase",
        model: {
            currentPanelNum: "{nav}.model.currentPanelNum"
        },
        panelTotalNum: "{nav}.options.panelTotalNum"
    }
}</code></pre>
        </td>
    </tr>
</table>

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`panelTotalNum`</td>
        <td>The total number of panels in the editor. This must be supplied by an integrator.</td>
        <td>Any valid integer</td>
        <td>
        <pre><code>panelTotalNum: null</code></pre>
        </td>
    </tr>
    <tr>
        <td>`messageBase`</td>
        <td>The loaded message bundle.</td>
        <td>Any valid key/value pairing, where the value is a localized string. The key could also take a namespace by providing a prefix (e.g. namespace-key). This allows for grouping strings to be accessed as an array of strings. (See: [Message Lookup API](msgLookup.md))
        <pre><code>messageBase: {
    "someMessage": "a localized message",
    "myNamespace-string1": "The first localized string",
    "myNamespace-string2": "The second localized string"
}</code></pre></td>
        <td>
        <pre><code>tooltipOptions: {
    delay: 0,
    duration: 0,
    position: {
        my: "left bottom",
        at: "right+1 top"
    },
    styles: {
        tooltip: "gpii-fd-tooltip"
    },
    items: ".gpiic-fd-tooltip:not([disabled])"
}</code></pre>
        </td>
    </tr>
    <tr>
        <td>`selectors`</td>
        <td>Javascript object containing selectors for various fragments of the markup, including the containers for the subcomponents.</td>
        <td></td>
        <td>See [Selectors](#selectors)</td>
    </tr>
    <tr>
        <td>`styles`</td>
        <td>Specific class names used to achieve the look and feel.</td>
        <td></td>
        <td>
        <pre><code>styles: {
    active: "gpii-fd-active",
    show: "gpii-fd-show"
}</code></pre>
        </td>
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
| `navButtons` | The container for the navButtons sub-component | `".gpiic-fd-navButtons"` |
| `navIcons` | The container for the navIcons sub-component | `".gpiic-fd-navIcons"` |
| `stepCount` | The container for the stepCount sub-component | `".gpiic-fd-stepCountMsg"` |

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script src="src/js/msgLookup.js"></script>
<script src="src/js/tooltip.js"></script>
<script src="src/js/navIcons.js"></script>
<script src="src/js/navButtons.js"></script>
<script src="src/js/stepCount.js"></script>
<script src="src/js/nav.js"></script>
```
