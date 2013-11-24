jQuery Autotab
==============
Autotab is a jQuery plugin that provides auto tabbing and filtering on text fields in a form. Once the maximum number of characters has been reached within a text field, the focus is automatically set to a defined element. Likewise, clearing out the text field's content by pressing backspace eventually places the focus on a previous element.


## Why jQuery Autotab?
* Auto tabbing behaves logically, in both tabbing forward and tabbing backwards.
* Allow your users to easily modify your text in a tab that would otherwise auto tab away.
* Reduce the amount of bad data submitted in a form by filtering text fields.
* Populate multiple text fields by pasting into one.
* Enhance text fields by auto tabbing when a specific character is pressed.
* It is small, fast, easy to load and built on the powerful jQuery library.


## Table of Contents
* [Requirements](#requirements)
* [Installation](#installation)
* [Setup and Usage](#setup-and-usage)
  * [Auto Tabbing](#auto-tabbing)
    * [Examples](#examples)
  * [Remove and Restore](#remove-and-restore)
    * [Examples](#examples-1)
  * [Filtering](#filtering)
    * [Examples](#examples-2)
  * [Forced Auto Tabbing](#forced-auto-tabbing)
* [Options](#options)
* [Filter Formats](#filter-formats)
* [Feedback](#feedback)
* [Copyright and License](#copyright-and-license)


## Requirements

Autotab works in both jQuery 1.7+ and 2.x. If your site supports Internet Explorer 6, 7, and/or 8, use jQuery 1.7+ since 2.x drops support for these browsers.


## Installation

Add a reference to jquery.autotab.js.

```html
<script src="jquery.autotab.js"></script>
```


## Setup and Usage

Autotab can be setup in several different ways within jQuery's `$(document).ready()` event. The two components that make up Autotab, auto tabbing and filtering, can be managed independently from one another, providing numerous ways of achieving the same result, depending on how indepth you want to setup your form.


### Auto Tabbing

__Note:__ If the selector matches multiple elements, the target and previous fields will be overwritten if previously set.

<table width="100%">
  <tr>
    <td width="25%">.autotab()</td>
    <td>Accepts no arguments and applies auto tabbing rules only.</td>
  </tr>
  <tr>
    <td valign="top">.autotab(string)</td>
    <td>
      <strong>string</strong>: Can be a filter format or a value that tells the script to remove or restore auto tab and filtering functionality.
      <br />
      <strong>Note</strong>: Previous auto tabbing order will be overwritten. To change the filter only, call <code>.autotab('filter', '')</code>
    </td>
  </tr>
  <tr>
    <td>.autotab(object)</td>
    <td><strong>object</strong>: Applies the specified options to all matched elements.</td>
  </tr>
</table>


#### Examples

Establishes auto tabbing rules only and forces each field to have a `maxlength` of 1.

```js
$('.answer').autotab({ maxlength: 1 });
```
```html
<div>
    <label>Answer 1</label>
    <input type="text" id="answer1" class="answer" size="3" /> -
    <label>Answer 2</label>
    <input type="text" id="answer2" class="answer" size="3" /> -
    <label>Answer 3</label>
    <input type="text" id="answer3" class="answer" size="3" /> -
</div>
```

Automatically establishes auto tabbing order and number filtering.

```js
$('.number').autotab('number');
```
```html
<div>
    <label>Phone Number</label>
    <input type="text" id="number1" class="number" maxlength="3" size="3" /> -
    <input type="text" id="number2" class="number" maxlength="3" size="3" /> -
    <input type="text" id="number3" class="number" maxlength="4" size="5" />
</div>
```

Manually defines auto tabbing order and alphanumeric filtering.

```js
$('#alphanumeric1').autotab({ format: 'alphanumeric', target: '#alphanumeric2' });
$('#alphanumeric2').autotab({ format: 'alphanumeric', target: '#alphanumeric3', previous: '#alphanumeric1' });
$('#alphanumeric3').autotab({ format: 'alphanumeric', target: '#alphanumeric4', previous: '#alphanumeric2' });
$('#alphanumeric4').autotab({ format: 'alphanumeric', target: '#alphanumeric5', previous: '#alphanumeric3' });
$('#alphanumeric5').autotab({ format: 'alphanumeric', previous: '#alphanumeric4' });
```
```html
<div>
    <label>Product Key</label>
    <input type="text" id="alphanumeric1" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric2" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric3" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric4" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric5" class="alphanumeric" maxlength="5" size="4" />
</div>
```


### Remove and Restore

<table width="100%">
  <tr>
    <td width="35%" valign="top">
      .autotab('remove|destroy|disable')
    </td>
    <td>
      <strong>string</strong>: Disables auto tab and filtering functionality on all matched elements.
      <br />
      <strong>Note</strong>: Both <code>destroy</code> and <code>remove</code> will disable auto tab and filtering. Standard and custom event bindings persist as they check the status of an element when called. Removing the <code>keydown</code> and <code>keypress</code> can have a negative impact in both user and developer experience if the same events have been bound in other areas.
    </td>
  </tr>
  <tr>
    <td valign="top">.autotab('restore|enable')</td>
    <td>
      <strong>string</strong>: Restores auto tab and filtering functionality on all matched elements.
    </td>
  </tr>
</table>


#### Examples

Manually turn off auto tab and filtering functionality on all text boxes.

```js
$('#remove-autotab').on('click', function () {
    $('input[type=text]').autotab('remove');
});
```
```html
<button id="remove-autotab">Turn Off</button>
```

Manually turn on auto tab and filtering functionality on all text boxes. 

```js
$('#restore-autotab').on('click', function () {
    $('input[type=text]').autotab('restore');
});
```
```html
<button id="restore-autotab">Turn On</button>
```


### Filtering

__Note:__ If passing an object, the target and previous fields are ignored, if included, to preserve previously established auto tab rules. Use `.autotab(object)` to modify the target and previous fields.

<table width="100%">
  <tr>
    <td width="25%">.autotab('filter', string)</td>
    <td><strong>string</strong>: Applies the specified filter format to all matched elements.</td>
  </tr>
  <tr>
    <td valign="top">.autotab('filter', object)</td>
    <td>
      <strong>object</strong>: Applies the specified filter options to all matched elements. The target and previous fields are ignored.
    </td>
  </tr>
</table>

Because of how Autotab's settings are stored, it is possible to define the filter format using `data-autotab-format`. If using `custom`, place your regular expression in `data-autotab-pattern`.


#### Examples

Manually defines text filtering.

```js
$('#salt').autotab('filter', 'text');
```
```html
<div>
    <label>Salt</label>
    <input type="text" id="salt" maxlength="16" size="12" />
</div>
```

Manually defines alphanumeric filtering and converts all alpha characters to uppercase format.

```js
$('.alphanumeric').autotab('filter', { format: 'alphanumeric', uppercase: true });
```
```html
<div>
    <label>Product Key</label>
    <input type="text" id="alphanumeric1" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric2" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric3" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric4" class="alphanumeric" maxlength="5" size="4" /> -
    <input type="text" id="alphanumeric5" class="alphanumeric" maxlength="5" size="4" />
</div>
```

Manually defines number filtering via `data-autotab-format`. In this example, `$(selector).autotab()` will take the attribute into account.

```html
<div>
    <label>Phone Number</label>
    <input type="text" id="phone1" maxlength="3" size="3" data-autotab-format="number" /> -
    <input type="text" id="phone2" maxlength="3" size="3" data-autotab-format="number" /> -
    <input type="text" id="phone3" maxlength="4" size="4" data-autotab-format="number" />
</div>
```

Other random JavaScript examples

```js
$('input[type=text]').autotab();
$('#username').autotab({ format: 'alphanumeric', target: '#password' });
$('#password').autotab({ previous: '#username', target: '#confirm' });
$('#product-key').autotab('filter', { format: 'alphanumeric', uppercase: true });
$('#ip-address').autotab('filter', { format: 'custom', pattern: '[^0-9\.]' });
$('#function').autotab('filter', function (text) { alert(text); });
$('#number1, #number2, #number3').autotab('filter', 'number');
$('.ipv6').autotab('filter', 'hexadecimal');
```


### Forced Auto Tabbing

Autotab comes with two functions that can be used to force an auto tab from a field if a criteria is met.

__Note__: These methods are only useful if an element setup with Autotab has focus.

<table width="100%">
  <tr>
    <td width="30%" valign="top">$.autotab.next()</td>
    <td>Triggers the `autotab-next` event, which sets the focus on the target element, if it exists.</td>
  </tr>
  <tr>
    <td valign="top">$.autotab.previous()</td>
    <td>Triggers the `autotab-previous` event, which sets the focus on the previous element, if it exists.</td>
  </tr>
</table>


## Options

```js
var options = {
    format: string|function,
    pattern: string,
    uppercase: boolean,
    lowercase: boolean,
    nospace: boolean,
    maxlength: integer,
    target: string|element,
    previous: string|element,
    trigger: string|array
};
```
<table width="100%">
  <tr>
    <td valign="top">format</td>
    <td>
      <strong>string</strong>: Speficies which format rule to use on a text box's value.
      <br />
      <strong>function(value, element)</strong>: If a single regular expression is insufficient, a function can be used for custom formatting. The parameter <code>value</code> is the typed character and <code>element</code> is the focused JavaScript element.
      <br />
      <strong>Note</strong>: Go to <a href="#filter-formats">Filter Formats</a> to see each available <code>format</code> option.
    </td>
  </tr>
  <tr>
    <td>pattern</td>
    <td>
      <strong>string</strong>: Used only when the <code>custom</code> format is specified, and it must be a string.
    </td>
  </tr>
  <tr>
    <td>uppercase</td>
    <td>
      <strong>boolean</strong>: Forces all <code>alpha</code> characters to uppercase format.
    </td>
  </tr>
  <tr>
    <td>lowercase</td>
    <td>
      <strong>boolean</strong>: Forces all <code>alpha</code> characters to lowercase format.
    </td>
  </tr>
  <tr>
    <td valign="top">nospace</td>
    <td>
      <strong>boolean</strong>: Determines if spaces are allowed or not.
      <br />
      <strong>Note</strong>: Space and underscore are not alpha characters and are not included in the <code>alpha</code> and <code>alphanumeric</code> format options. Use the <code>custom</code> format to allow these characters.
    </td>
  </tr>
  <tr>
    <td valign="top">maxlength</td>
    <td>
      <strong>integer</strong>: The maximum number of characters allowed in a text box. Maxlength can be specified with the HTML attribute <code>maxlength</code>.
      <br />
      <strong>Note</strong>: The maxlength attribute value can be overwritten if the maxlength field is passed to <code>autotab()</code>.
    </td>
  </tr>
  <tr>
    <td valign="top">target</td>
    <td>
      When auto tabbing occurs, <code>target</code> is the element that will gain focus.
      <br/>
      <strong>string</strong>: A selector identifying the next element.
      <br/>
      <strong>element</strong>: The JavaScript or jQuery element.
    </td>
  </tr>
  <tr>
    <td valign="top">previous</td>
    <td>
      When backspacing or reverse tabbing, <code>previous</code> is the element that will gain focus.
      <br/>
      <strong>string</strong>: A selector identifying the next element.
      <br/>
      <strong>element</strong>: The JavaScript or jQuery element.
    </td>
    </td>
  </tr>
  <tr>
    <td valign="top">trigger</td>
    <td>
      Triggers <code>autotab-next</code> when the specified characters are pressed.
      <br/>
      <strong>string</strong>: A string of one or more characters
      <br/>
      <strong>element</strong>: An array of one or more strings
    </td>
    </td>
  </tr>
</table>


## Filter Formats

Autotab has several filter formats available, all passed into the `format` key. If none of the formats meet your needs, Autotab also supports a passing a function or specifying `custom` option where you can pass a regular expression.

<table width="100%">
  <tr>
    <td width="25%">all</td>
    <td>Allows any and all characters.</td>
  </tr>
  <tr>
    <td>text</td>
    <td>Allows all characters, including special characters, except numbers.</td>
  </tr>
  <tr>
    <td>alpha</td>
    <td>Allows only letters.</td>
  </tr>
  <tr>
    <td>number|numeric</td>
    <td valign="top">Allows only numbers.</td>
  </tr>
  <tr>
    <td>alphanumeric</td>
    <td>Allows only letters and numbers.</td>
  </tr>
  <tr>
    <td>hex|hexadecimal</td>
    <td>Allows only letters A-F, a-f and numbers.</td>
  </tr>
  <tr>
    <td>
      custom
    </td>
    <td>
      Allows a developer to provide a custom regular expression: <code>new RegExp(pattern, 'g');</code>
      <br />
      <strong>Note</strong>: Requires <code>pattern: <em>string</em></code>, ie: <code>pattern: "[^0-9\.]"</code>
    </td>
  </tr>
  <tr>
    <td valign="top">function(value, element)</td>
    <td>
      Allows a developer to provide a their own function in case a regular expression is insufficient.
      <br />
      <strong>Note</strong>: <code>value</code> is the typed character, <code>element</code> is the focused JavaScript element.
    </td>
  </tr>
</table>


## Feedback

Please provide feature requests and bug reports here on [GitHub](../../issues).

You can also reach out to me on twitter: [@mathachew](http://www.twitter.com/mathachew)

## Copyright and license

&copy; 2013 Matthew Miller

Licensed under the MIT licensing: http://www.opensource.org/licenses/mit-license.php
