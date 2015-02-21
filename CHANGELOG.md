## 1.9.2 (2015-02-20)

Bug fixes:

* fixed an issue with input elements that are a button type having their text being overwritten when pasting and modified the demo to test against the bug (#79)
* included a pull request that restores an element's original maxlength value


## 1.9.1 (2015-02-04)

Bug fixes:

* reverted a change that caused odd results with an element's maxlength property changed


## 1.9.0 (2015-01-31)

Features:

* improved support for other scripts that utilize the key events so as to prevent conflicts from happening
* added support `drop` events, which are handle just like `paste` events (#73)
* added support for tabbing through fields using the left and right arrow keys (#74)
* auto tabbing support added to several input types: tel, number, email, url and search (#75)

Bug fixes:

* fixed a pasting issue that resulted in a target's value being cleared when no additional characters were being pasted (#72)
* fixed a pasting issue in IE11 where backspacing into a previous element caused the cursor to be placed at the front of the element's value instead of at the end


## 1.8.1 (2014-11-01)

Features:

* added support for reusing predefined target/previous selectors for elements

Bug fixes:

* fixed the Angular and Knockout demos by properly applying the uppercase filter requirement on the product key example
* removed debugging code


## 1.8.0 (2014-10-28)

Features:

* added refresh global method
* updated demo to support removing examples in order to showcase the new refresh feature
* added support for readonly fields
* added support for specifying the filter format through class names based on the value of `$.autotab.selectFilterByClass`
* added demos for Knockout and Angular

Bug fixes:

* fixes several issues with handling a pasted value that contained capital letters (#41, #65)
* fixes an issue that caused disabled/readonly fields to be altered when pasting


## 1.7.1 (2014-08-21)

Bug fixes:

* fixes an issue when using deprecated methods `autotab_magic` and `autotab_filter` in a method chain


## 1.7 (2014-07-26)

Features:

* added support for additional fields and removed hidden fields from the selected elements, including maxlength support for textarea (#14)
* added option to auto tab on single value select lists when selecting a value
* added global methods to setup, remove and restore Autotab
* elements passed to Autotab now filter out hidden form fields

Bug fixes:

* fixes an issue with tabbing to a previous field that is disabled, resulting in the value being modified (#47)


## 1.6 (2014-04-30)

Features:

* restores the ability to apply a filter only (#36)
* added support to filter and tab on password fields (#36)


## 1.5.5 (2014-01-31)

Bug fixes:

* fixes a cursor position issue in IE6+ when replacing the value of a text box that is currently selected (#32)


## 1.5.4 (2014-01-15)

Features:

* added a check to apply filtering only to text fields, as support for other input types varies and may not support selection, while preserving auto tabbing functionality

Bug fixes:

* fixes an issue with multiple characters appearing after typing one when applying a filter rule more than once
* fixes an issue with maxLength and Firefox, which defaults to -1


## 1.5.3 (2014-01-13)

Bug fixes:

* addresses an issue with forms not submitting from the on-screen keyboard (#22)


## 1.5.2 (2014-01-13)

Bug fixes:

* refactoring caused filtering rules, like uppercase or lowercase, to not work correctly (#23)


## 1.5.1 (2013-12-17)

Bug fixes:

* in Internet Explorer, reaching the max length caused the last character to appear in the target element after auto tabbing (#19)


## 1.5 (2013-12-12)

Features:

* added support for auto tabbing by specific keys
* refactored various areas dealing with boolean evaulations and checking for iOS and Firefox

Bug fixes:

* fixed a bug that prevented the `change` event from triggering (#17)


## 1.4 (2013-11-12)

Features:

* pasting support has been greatly improved and behaves more intelligently
* improved support in Firefox so that special keys no longer have to be tracked in order to be allowed

Bug fixes:

* fixed a bug where the `del` key would do nothing in Firefox (introduced in 1.3)
* fixed several instances of bad evaluations of boolean values as a result of browsers storing data-* differently (introduced in 1.3)


## 1.3 (2013-11-09)

Features:

* added a 1ms timer to `$.autotab.next()` and `$.autotab.previous()` so that the calls perform as expected when the keypress event is complete
* added the ability to turn auto tab and filtering on or off at will (#4)
* added Firefox detection so that code specific to it can run separate from everything else
* improved support for using a function as the format
* refactored how Autotab's settings are stored as the previous method caused issues with turning it off and on again
* added support for loading filter formats using `data-autotab-format`
* added support for hexadecimal filtering

Bug fixes:

* if a selector has no matches, but `.autotab()` is still called, an error would occur
* if allowing periods in a text box, Firefox would display two periods when only one was typed


## 1.2 (2013-11-02)

Features:

* updated `autotab()` to be the primary means of setting up auto tabbing and filtering (see documentation for more details)
* greatly improved filtering by preventing illegal characters from appearing by changing `keyup` to `keypress`
* improved functionality when making multiple calls for auto tab and/or filtering that prevents multiple triggers of the auto tabbing and filtering from occuring
* added `$.autotab.next()` and `$.autotab.previous()`, which can be used to manually trigger the `autotab-next` and `autotab-previous` events respectively
* added support to prevent double tabbing using a timer, ie. pressing tab immediately after auto tabbing has occurred
* added basic support for pasting
* improved auto tabbing by moving to the next element when the current one reaches its maxlength while holding down a key
* auto tabbing forward will select the target element's value (#1)
* while auto tabbing does not work on iOS devices, the behavior of the script has improved, including input validation
* fully backwards compatible with Autotab 1.1b

Bug fixes:

* if rapidly typing illegal characters, the next element received focused despite the previous element not reaching it's maxlength
* addressed sevearl behavioral issues in some of the latest versions of Firefox


## 1.1b (2008-09-10)

Features:

* refactored auto tabbing and filtering functionality so that one or the other could be applied
* added `autotab_magic()`, simplifying the setup of `target` and `previous` elements
* added `custom` format option, which requires a regular expression to be passed in the `pattern` field
* updated `format` to support functions

Bug fixes:

* in Safari, pressing backspace in an empty text box would not focus on the `previous` element
* in IE, pressing the left arrow key would force the cursor to the end of the field's content


## 1.0 (2008-05-22)

Initial Release
