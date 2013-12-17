## 1.5.1

Bug fixes:

* in Internet Explorer, reaching the max length caused the last character to appear in the target element after auto tabbing (#19)


## 1.5

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
