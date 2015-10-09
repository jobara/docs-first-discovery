---
title: First Discovery Editor - Preferences Server Integration
layout: default
category: API
---

## Overview

**Component Name:** `gpii.firstDiscovery.prefsServerIntegration`

**File:** `firstDiscoveryEditor.js`

First Discovery Editor (Preferences Server Integration) component is a grade containing the configuration necessary to connect the [First Discovery Editor](firstDiscoveryEditor.md) with the [Preferences Server](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md). This grade is intended to be added as a base grade to the [First Discovery Editor](firstDiscoveryEditor.md).

This component uses the [Preferences Server API](https://github.com/GPII/universal/blob/master/documentation/PreferencesServer.md) to save preferences that users select in the First Discovery Tool to the server. The server returns a token that identifies the saved preferences for them to be applied to other devices.

## Adding a First Discovery Editor - Preferences Server Integration

The First Discovery Editor - Preferences Server Integration is intended to work in conjuction with the [First Discovery Editor](firstDiscoveryEditor.md) by supplying both components as the loaderGrade in an
[Auxiliary Schema](http://docs.fluidproject.org/infusion/development/AuxiliarySchemaForPreferencesFramework.html):

```javascript
fluid.defaults("my.auxSchema", {
    auxiliarySchema: {
        "loaderGrades": ["gpii.firstDiscovery.firstDiscoveryEditor", "gpii.firstDiscovery.prefsServerIntegration"]
    }
});
```

## Grades

This component uses the following base
[grades](http://docs.fluidproject.org/infusion/development/ComponentGrades.html):

* [`fluid.modelComponent`](http://docs.fluidproject.org/infusion/development/ComponentGrades.html)

## Methods

| Method | Description | Parameters |
|--------|-------------|------------|
| `setLastPanelStyle` | Applies a special class name to the First Discovery Editor container when the current visible panel is the last panel of the First Discovery Tool. | none |

## Options

<table>
    <tr><th>Name</th><th>Description</th><th>Values</th><th>Default</th></tr>
    <tr>
        <td>`styles`</td>
        <td>Specific the class name used to identify the last panel is visible.</td>
        <td></td>
        <td>
        <pre><code>styles: {
    lastPanel: "gpii-fd-lastPanel"
}</code></pre>
        </td>
    </tr>
</table>

## Dependencies

```html
<script type="text/javascript" src="src/lib/infusion/infusion-custom.js"></script>
<script type="text/javascript" src="src/schemas/schemas.js"></script>
<script type="text/javascript" src="src/js/keyboardShortcut.js"></script>
<script type="text/javascript" src="src/js/ttsHookup.js"></script>
<script type="text/javascript" src="src/js/tooltip.js"></script>
<script type="text/javascript" src="src/js/msgLookup.js"></script>
<script type="text/javascript" src="src/js/selfVoicing.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAssessment.js"></script>
<script type="text/javascript" src="src/js/keyboardInput.js"></script>
<script type="text/javascript" src="src/js/stickyKeysAdjuster.js"></script>
<script type="text/javascript" src="src/js/panels.js"></script>
<script type="text/javascript" src="src/js/enactors.js"></script>
<script type="text/javascript" src="src/js/navButtons.js"></script>
<script type="text/javascript" src="src/js/navIcons.js"></script>
<script type="text/javascript" src="src/js/helpButton.js"></script>
<script type="text/javascript" src="src/js/stepCount.js"></script>
<script type="text/javascript" src="src/js/nav.js"></script>
<script type="text/javascript" src="src/js/firstDiscoveryEditor.js"></script>
```