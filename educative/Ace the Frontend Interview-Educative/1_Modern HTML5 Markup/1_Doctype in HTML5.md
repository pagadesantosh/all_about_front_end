#### Points to Remember

- ##### Syntax to define Doctype in HTML5 is < !DOCTYPE html >
- ##### The < !DOCTYPE html > declaration is considered as an information to the browser about what document type to expect, it is not considered as an HTML tag.

- ##### The following are the three modes that are defined by layout engines in web browsers

- ###### Quirks Mode, Almost standards mode, Full standards mode.

- Quirks mode refers to a strategy used by some web browsers to preserve backward compatibility with web pages built for old web browsers, rather than solely complying with standard W3C and IETF requirements in the standards mode.

- Almost standards mode rendering matches “full standards” mode in all details except, the image layout inside table cells is treated in the same way that “quirks” mode works. This means that sliced image-in-table layouts are less likely to collapse in browsers in either “quirks” or “almost normal” mode than in “full standards” mode.

- Full standards mode In this mode, the behavior described is the same as described by HTML and CSS specifications. Most of the modern browsers use full standard mode.

- ##### With DOCTYPE placed at the start of the HTML markup, "Full standards mode" is enabled in web browsers.

- ##### Will adding any non-executing code, e.g. comments, XML declaration `before the DOCTYPE declaration will trigger quirks mode` in Internet Explorer 9 and older.

- ##### The HTML5 doctype, < !DOCTYPE html>, triggers Full Standards mode in every browser (including IE6).

- ##### The main issue that arises if we don’t define DOCTYPE at the beginning of our HTML code is it activates the Quriks mode.

- #### For example: new features & tags in HTML5 such as article, footer,header, nav, section may not be supported if the <!DOCTYPE> is not declared.
