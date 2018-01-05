Release notes
=============

This document describes all the changes made to the *Organizational Units API*
document, starting from its first beta draft version.


2.1.0
-----

* Publishing data on external units is now only "recommended" (previously it
  was "required").
* Fixed obsolete links.


2.0.0
-----

 * This API now requires implementers to upgrade their implementations to
   [Version 2](https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v2)
   of the *Authentication and Security* document.

   In particular, this means that the clients MUST be aware of the fact, that
   the server is no longer required to support methods of authentication and
   encryption which it *was* required to support in the previous versions of
   this API. Clients SHOULD consult the newly introduced `<http-security>`
   element in the server's manifest entry before making their requests.

 * Because we are releasing a new major release (which is no longer
   backward-compatible with the previously released stable `1.x.x` releases),
   XML namespaces were changed to reflect that.

   In particular, the API-entry namespace was changed from:

   ```
   https://github.com/erasmus-without-paper/ewp-specs-api-ounits/blob/stable-v1/manifest-entry.xsd
   ```

   to:

   ```
   https://github.com/erasmus-without-paper/ewp-specs-api-ounits/blob/stable-v2/manifest-entry.xsd
   ```

   And the response namespace was changed from:

   ```
   https://github.com/erasmus-without-paper/ewp-specs-api-ounits/tree/stable-v1
   ```

   to:

   ```
   https://github.com/erasmus-without-paper/ewp-specs-api-ounits/tree/stable-v2
   ```


1.1.1
-----

* Explicitly declare that this version still requires the use of
  [Version 1](https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v1)
  of the *Authentication and Security* document. You can find more information
  on the planned process of updating security requirements
  [here](https://github.com/erasmus-without-paper/ewp-specs-sec-intro/issues/1).


1.1.0
-----

* Added an optional field for the logo of the unit.


1.0.0
-----

* Changed XML Namespace. Replaced the draft `master` branch:

  ```
  https://github.com/erasmus-without-paper/ewp-specs-api-ounits/tree/master
  ```

  With the `stable-v1` one:

  ```
  https://github.com/erasmus-without-paper/ewp-specs-api-ounits/tree/stable-v1
  ```

* Similar change has been made to the `manifest-entry.xsd` namespace.

* Changed XML Namespaces of the Phone Number, Address and Abstract Contact data
  types (all of them are now `stable-v1`).

* `minOccurs` and `maxOccurs` are now provided explicitly
  ([why?](https://github.com/erasmus-without-paper/general-issues/issues/22)).

* Organizational Unit IDs are now of `ewp:AsciiPrintableIdentifier` type
  ([why?](https://github.com/erasmus-without-paper/general-issues/issues/23)).

This is the first official stable version, accepted by all the partners
([details here](https://github.com/erasmus-without-paper/general-issues/issues/24)).


0.4.1
-----

* Modified the `<contact>` elements in examples to fit recent additions to the
  [Abstract Contact Type](https://github.com/erasmus-without-paper/ewp-specs-types-contact).


0.4.0
-----

* The server is now REQUIRED to provide `<ounit-code>` element
  (`minOccurs="1"`).

* New `ounit_code` parameter was added to allow requesters searching for units
  by their codes (the server is now REQUIRED to support this parameter).
  Providing `ounit_id` parameter is no longer required, if the requester
  provides the `ounit_code` parameter. This is a part of a larger change in all
  APIs described
  [here](https://github.com/erasmus-without-paper/general-issues/issues/21).

* An optional `<abbreviation>` element wad added. See
  [this thread](https://github.com/erasmus-without-paper/ewp-specs-api-institutions/issues/10).

* Specified that servers are allowed to "hide" units which they believe EWP
  doesn't need to see, but if they do, they need to do this consistently. See
  [this thread](https://github.com/erasmus-without-paper/general-issues/issues/20).

* Specified how server should respond when "required" parameters are missing.


0.3.0
-----

* New `<ounit-code>` elements were added to allow separation of surrogate and
  natural/business keys. See
  [this thread](https://github.com/erasmus-without-paper/ewp-specs-api-omobilities/issues/9#issuecomment-271387634).

* Up to now, Organizational Units API described only the units of HEIs
  *covered* by the host. Now, servers are REQUIRED to also describe units of
  *foreign HEIs*, but only if they *refer to* these units in other APIs
  ([why?](https://github.com/erasmus-without-paper/ewp-specs-api-iias/issues/6)).


0.2.0
-----

* Added `<mobility-factsheet-url>` element
  ([issue link](https://github.com/erasmus-without-paper/ewp-specs-api-ounits/issues/2#issuecomment-266738633)).
* Clarified some differences between "tree-like" and "flat" structure
  approaches.


0.1.0
-----

Initial release.
