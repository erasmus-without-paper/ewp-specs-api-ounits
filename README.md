Organizational Units API
========================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Organizational Units API**. Once implemented by
the host, it allows external clients to retrieve general information on
selected organizational units (faculties, departments, divisions, etc.)
**either covered, or otherwise known** by this host. It responds with similar
type of information as [Institutions API][institutions-api] does, but on a
lower level.


"Covered" vs "known"
--------------------

Please read [this chapter in the Intitutions
API](https://github.com/erasmus-without-paper/ewp-specs-api-institutions#known-heis).
The concept of *known organizational units* is exactly the same as the concept
of *known institutions*. Server implementers MUST provide some basic
information on known external organizational units, **if it refers to them** in
other APIs.


Request method
--------------

 * Requests MUST be made with either HTTP GET or HTTP POST method. Servers MUST
   support both these methods. Servers SHOULD reject all other request methods.

 * Clients are advised to use POST when passing large number of parameters
   (servers MAY set a limit on their GET query string length).


Request parameters
------------------

Parameters MUST be provided in the regular `application/x-www-form-urlencoded`
format.


### `hei_id` (required)

Each unit is identified by two values: ID of the institution, and the ID of the
organizational unit within this institution. Organizational Units API allows
clients to ask for information on *multiple units*, but all of these must be
within **a single institution**. This parameter takes the the ID of this
institution.


### `ounit_id` or `ounit_code` (repeatable, required)

A list of unit IDs OR unit codes (no more than `<max-ounit-ids>` or
`<max-ounit-codes>` items, respectively). The requester MUST provide either a
list of `ounit_id` values, or a list of `ounit_code` values, **but not both**.

This parameter is *repeatable*, so the request MAY contain multiple occurrences
of it. The server is REQUIRED to process all of them.

Server implementers provide their own chosen values of `<max-ounit-ids>` and
`<max-ounit-codes>` via their manifest entry (see
[manifest-entry.xsd](manifest-entry.xsd)). Clients SHOULD parse this value (or
assume it's equal to `1`).


Security and permissions
------------------------

For all endpoints of this API, implementers MUST follow the rules described in
[EWP Authentication and Security, Version 1][sec-v1] document.

Server implementers MAY choose to hide some of their organizational units from
EWP members. But if they do, they MUST keep proper referential integrity in
mind (if a unit is referenced somewhere in other APIs, then it MUST be visible
here).


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Invalid (or unknown) `hei_id` values SHOULD result in an HTTP 400 error.

 * Invalid (or unknown) `ounit_id` and `ounit_code` values MUST be **ignored**.
   Servers MUST return a valid (HTTP 200) XML response in such cases, and the
   response should simply not contain any information on these missing entities.
   If all values are unknown, servers MUST respond with an empty `<response>`
   element. This requirement is true even when both `<max-ounit-ids>` and
   `<max-ounit-codes>` is set to `1`.

 * If the length of `ounit_id` list is greater than `<max-ounit-ids>` (or the
   length of `ounit_code` list is greater than `<max-ounit-codes>`), then the
   server MUST respond with HTTP 400.

 * If both lists are empty, then the server SHOULD respond with HTTP 400.


Response
--------

Servers MUST respond with a valid XML document described by the
[response.xsd](response.xsd) schema. See the schema annotations for further information.


Data model entities involved in the response
--------------------------------------------

 * Inst/Org Unit
 * Coordinator
 * HEI Contact Info
 * Person


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[institutions-api]: https://github.com/erasmus-without-paper/ewp-specs-api-institutions
[sec-v1]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v1
