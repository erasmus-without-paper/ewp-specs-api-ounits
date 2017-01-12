Release notes
=============

This document describes all the changes made to the *Organizational Units API*
document, starting from its first beta draft version.


0.3.0
-----

* New `<ounit-code>` elements were added to allow separation of surrogate and
  natural/business keys. See [this thread]
  (https://github.com/erasmus-without-paper/ewp-specs-api-mobilities/issues/9#issuecomment-271387634).

* Up to now, Organizational Units API described only the units of HEIs
  *covered* by the host. Now, servers are REQUIRED to also describe units of
  *foreign HEIs*, but only if they *refer to* these units in other APIs ([why?]
  (https://github.com/erasmus-without-paper/ewp-specs-api-iias/issues/6)).


0.2.0
-----

* Added `<mobility-factsheet-url>` element ([issue link]
  (https://github.com/erasmus-without-paper/ewp-specs-api-ounits/issues/2#issuecomment-266738633)).
* Clarified some differences between "tree-like" and "flat" structure
  approaches.


0.1.0
-----

Initial release.
