# Cards

## Import

```javascript
import { Card, CardHeader, CardBody, CardTitle } from "/imports/plugins/core/ui/client/components";
```

## Usage Example

```javascript
import React from "react";
import { Card,  CardHeader, CardBody } from "/imports/plugins/core/ui/client/components";

const MyReactComponent = () => {
  return (
    <Card>
      <CardHeader
        i18nKeyTitle=""
        title=""
      />
      <CardBody>

      </CardBody>
    </Card>
  )
};

export default MyReactComponent;
```

## Props

## Card

No Props, used as a wrapper for `CardHeader`, `CardTitle`, and `CardBody`

### CardHeader

Provides a header for the card, also contains the CardTitle component for convenience.

Property     | Type   | Description
------------ | ------ | ------------------------
i18nKeyTitle | String | Key for i18n translation
title        | String | Title for card header

### CardTitle

Provides a title for the card. In most cased CardHeader will be a better choice.

Property     | Type   | Description
------------ | ------ | ------------------------
i18nKeyTitle | String | Key for i18n translation
title        | String | Title for card header

### CardBody

No Props, use as wrapper for card content

# Settings Cards

When you need a

## Props

Property       | Type     | Description
-------------- | -------- | ----------------------------------------------------------------------------------------
i18nKeyTitle   | String   | Key for i18n translation
title          | String   | Title for card header
template       | Blaze    | A blaze template
expanded       | Boolean  | true / false if the card is expanded
onExpand       | Function | Called when card is expanded / collapsed. <br> `(event, card, name, isExpanded) => {}`
enabled        | Boolean  | true / false will set the switch to on / off
onSwitchChange | Function | Callback on switch change (on / off). <br> `(event, isChecked, name) => {}`
name           | String   | Used to identify components in callbacks.
icon           | String   | Font name from Font-awesome
children       | Node     | React child nodes. Set as the prop, or in the body of the tag.

## Usage Example

### Usage within a react component

```javascript
import React, { Component } from "react";
import { Reaction } "client/api";
import { CardGroup,  SettingsCard } from "/imports/plugins/core/ui/client/components";

class MyReactComponent extends Component {
  render() {
    return (
      <SettingsCard
        i18nKeyTitle={this.props.i18nKey}
        onExpand={this.props.onSettingExpand}
        expanded={this.props.expanded}
        title={this.props.title}
        name={this.props.name}
        enabled={this.props.enabled}
        icon={this.props.icon}
        onSwitchChange={this.props.onSettingEnableChange}
      >
        {/* Body of component (children) */}
      </SettingsCard>
    )
  }
}

export default MyReactComponent;
```

### Usage within a blaze component

**NOTE** Prefer building the settings component with React-only instead of using this method. This is provided to aide in unifying the experience while we work towards a 100% react conversion.

```javascript
import { Reaction } from "/client/api";

Template.myTemplate.helpers({
  SettingsComponent() {
    const currentData = Template.currentData();
    const preferences = Reaction.getUserPreferences("reaction-social", "settingsCards", {});

    return {
      component: SettingsCard,
      template: "nameOfBlazeTemplateToInclude"
      i18nKeyTitle: "i18nKey.path"
      title="Setting Card Title"
      icon="fa fa-plus" // Optional

      // Callbacks
      name="nameUsedForCallbacks"
      onExpand(event, card, name, isExpanded) {
        Reaction.updateUserPreferences("<PACKAGE_NAME>", "settingCards", {
          [name]: isExpanded
        });
      }
      expanded={preferences[settingName]}
      enabled={currentData.enabled}
      onSwitchChange(isChecked, name) {
        // Update package enabled / disabled status here
      }
    }
  }
})
```
