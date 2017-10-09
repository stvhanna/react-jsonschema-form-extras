[![Build Status](https://travis-ci.org/RxNT/react-jsonschema-form-extas.svg?branch=master)](https://travis-ci.org/RxNT/react-jsonschema-form-extras)
[![Coverage Status](https://coveralls.io/repos/github/RxNT/react-jsonschema-form-extras/badge.svg)](https://coveralls.io/github/RxNT/react-jsonschema-form-extras)
[![npm version](https://badge.fury.io/js/react-jsonschema-form-extras.svg)](https://badge.fury.io/js/react-jsonschema-form-extras)

# Catalogue

This project provides light integration over established React components, 
trying to keep configurations compatible with original project. 
All configurations you can specify in original projects, can be reused here.
  
- Composite array field (`ui:field` > `compositeArray`)
- Collapsible fields (`ui:field` > `collapsible`)
- Alternative input fields (`ui:field` > `altInput`)
- Typeahead, based on [react-bootstrap-typeahead](https://github.com/ericgio/react-bootstrap-typeahead) (`ui:field` > `typeaheadOptions`)
- Async Typeahead based on [react-bootstrap-typeahead](https://github.com/ericgio/react-bootstrap-typeahead) (`ui:field` > `typeahead`)
- Tables, based on [react-bootstrap-table](https://github.com/AllenFang/react-bootstrap-table) (`ui:field` > `table`)
- RTE, based on [react-rte](https://github.com/sstur/react-rte) (`ui:field` > `rte`)

## Use

This project uses internal react-jsonschema-form extension mechanism, through ui:field option in uiSchema. 
The simplest example of using it out of the box, is like this:

```js
import Form from "react-jsonschema-form";
import fields from "react-jsonschema-form-extras";

ReactDOM.render(
  <Form fields={fields}/>,
  document.getElementById("app")
);

```

If you have additional extensions, that are not part of this project, you can enable them, like this

```js
import Form from "react-jsonschema-form";
import otherFields from "other-fields";
import fields from "react-jsonschema-form-extras";

let allFields = Object.assign({}, fields, otherFields);

ReactDOM.render(
  <Form fields={allFields}/>,
  document.getElementById("app")
);

```

## Composite array field (`compositeArray`)

### Purpose

This is a simple UI pattern, where you want to separate entering a new value to the array and working with existing values.

### Use

The simplest `uiSchema` configuration would be:

```json
{
  "ui:field": "compositeArray",
  "inputField": "typeahead",
  "arrayField": "table",
  "typeahead": { },
  "table": { }
}
```

This means the final field will be presented in 2 parts
 - initial input with `typeahead` field
 - array field in `table` form

You can specify configurations for each field representation independently.

### Properties

There are only 2 properties needed for it to work
 - `inputField` field from form registry to use as a new field input presentation
 - `arrayField` field from form registry to use to present existing array values

## Collapsible fields (`collapsible`)

### Purpose

Collapsible helps you to hide content, that might take up too much space on the screen an expand it if user wishes.

### Use 

The simplest `uiSchema` configuration would be:

```json
{
  "ui:field": "collapsible",
  "collapse": {
    "field": "table"
  }
}
```

This is a hidden `table` field configuration, which will be presented as collapsed `schema` `title` name.

### Properties

You can customize presentation of collapsible field, with "collapse" object in uiSchema
- `field` `string` an actual hidden field to use
- `collapsed` `boolean` - indicating initial state (default `true`) 
- `icon` `object` icons configuration in `enabled` and `disabled` state
    - `enabled` `string` icon, when the field is shown (default `glyphicon glyphicon-chevron-down`)
    - `disabled` `string` icon, when field is hidden (default `glyphicon glyphicon-chevron-right`)
- `separate` `boolean` enable <hr/> after collapse menu (default `true`)  
- `wrapClassName` `string` class name to use on a parent collapse menu div (default `lead`)

Field `schema` `title` used as a header of the collapsible action. 

## Alternative input fields (`altInput`)

### Purpose

You want to enter the same `field` in 2 different ways. For example if a field might be a `string` and `number`

### Use

The simplest configuration would look something like this

```json
{
  "ui:field": "altInput",
  "defInput": "typeahead",
  "altInput": "typeaheadOptions",
  "typeahead": { },
  "typeaheadOptions": { }
}
```
In this case user would be able to enter the same field, either by using async typeahead or regular one.

### Properties

In order to configure presentation there are few options
- `defInput` `string` registry field to use as primary input method
- `altInput` `string` registry field to use as an alternative input method
- `altInputSeparator` `string` string to use in between those 2 presentations

## Typeahead, based on [react-bootstrap-typeahead](https://github.com/ericgio/react-bootstrap-typeahead) (`typeaheadOptions`)

