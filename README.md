jQuery Autotab
==============
Autotab is a jQuery plugin that provides auto tabbing and filtering on text fields in a form. Once the maximum number of characters has been reached within a text field, the focus is automatically set to a defined element. Likewise, clearing out the text field's content by pressing backspace eventually places the focus on a previous element.


## Why jQuery Autotab?
* Auto tabbing behaves logically, in both tabbing forward and tabbing backwards.
* Allow your users to easily modify your text in a tab that would otherwise auto tab away.
* Reduce the amount of bad data submitted in a form by filtering text fields.
* Populate multiple text fields by pasting into one.
* It is small, fast, easy to load and built on the powerful jQuery library.

_Pasting support has basic functionality and has a lot of room for improvement, so use at your own risk._


## Table of Contents
* [Requirements](#requirements)
* [Installation](#installation)
* [Setup and Usage](#setup-and-usage)
  * [Auto Tabbing](#auto-tabbing)
    * [Examples](#examples)
  * [Filtering](#filtering)
    * [Examples](#examples-1)
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
    <td>.autotab(string)</td>
    <td><strong>string</strong>: Defines the filter format that will be used on all matched elements.</td>
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

Other random JavaScript examples

```js
$('input[type=text]').autotab();
$('#username').autotab({ format: 'alphanumeric', target: '#password' });
$('#password').autotab({ previous: '#username', target: '#confirm' });
$('#product-key').autotab('filter', { format: 'alphanumeric', uppercase: true });
$('#ip-address').autotab('filter', { format: 'custom', pattern: '[^0-9\.]' });
$('#function').autotab('filter', function (text) { alert(text); });
$('#number1, #number2, #number3').autotab('filter', 'number');
```


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
    previous: string|element
};
```
<table width="100%">
  <tr>
    <td valign="top">format</td>
    <td>
      <strong>string</strong>: Speficies which format rule to use on a text box's value.
      <br />
      <strong>function</strong>: If a single regular expression is insufficient, a function can be used for custom formatting.
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
</table>


## Filter Formats

Autotab has several filter formats available. If none of the formats meet your needs, Autotab also supports a `custom` option where you can pass either a regular expression or a function.

<table width="100%">
  <tr>
    <td>format: 'all'</td>
    <td>Allows any and all characters.</td>
  </tr>
  <tr>
    <td width="30%">format: 'text'</td>
    <td>Allows all characters, including special characters, except numbers.</td>
  </tr>
  <tr>
    <td>format: 'alpha'</td>
    <td>Allows only letters.</td>
  </tr>
  <tr>
    <td>format: 'number|numeric'</td>
    <td valign="top">Allows only numbers.</td>
  </tr>
  <tr>
    <td>format: 'alphanumeric'</td>
    <td>Allows only letters and numbers.</td>
  </tr>
  <tr>
    <td>
      format: 'custom',
      <br />
      pattern: string
    </td>
    <td>
      Allows a developer to provide a custom regular expression: <code>new RegExp(pattern, 'g');</code>
      <br />
      <strong>Note</strong>: Requires <code>pattern: <em>string</em></code>, ie: <code>"[^0-9\.]"</code>
    </td>
  </tr>
  <tr>
    <td>format: function</td>
    <td>Allows a developer to provide a their own function in case a regular expression is insufficient.</td>
  </tr>
</table>


## Feedback

Please provide feature requests and bug reports here on [GitHub](../../issues).

You can also reach out to me on twitter: [@mathachew](http://www.twitter.com/mathachew)

## Copyright and license

&copy; 2013 Matthew Miller

Licensed under the MIT licensing: http://www.opensource.org/licenses/mit-license.php
