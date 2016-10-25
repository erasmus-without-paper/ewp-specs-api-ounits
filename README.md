Departments API
===============

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Departments API**. Once implemented by the host,
it allows external clients to retrieve general information on selected
departments covered by this host. It responds with similar type of information
as [Institutions API][institutions-api] does, but on the department level.


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

Each department is identified by two values: ID of the institution, and the ID
of the department within this institution. Departments API allows clients to
ask for information on *multiple departments*, but all of these must be within
**a single institution**. This is the ID of this institution.


### `department_id` (repeatable, required)

A list of department identifiers (no more than `<max-department-ids>` items).

This parameter is *repeatable*, so the request MAY contain multiple occurrences
of it. The server is REQUIRED to process all of them.

Server implementers provide their own chosen value of `<max-department-ids>`
via their manifest entry (see [manifest-entry.xsd](manifest-entry.xsd)).
Clients SHOULD parse this value (or assume it's equal to `1`).

Clients may retrieve valid department identifiers from other APIs, e.g. the
[Institutions API][institutions-api]. Servers MUST **ignore** invalid
identifiers.


Permissions
-----------

 * All requests from the EWP Network MUST be allowed to access this API.

 * Additionally, implementers MAY allow this API to be accessed by
   **anonymous** external clients too (without the need of using any client
   certificate).


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Invalid (uncovered) `hei_id` values SHOULD result in an HTTP 400 error.

 * Invalid `department_id` values MUST be **ignored**. Servers MUST return
   a valid (HTTP 200) XML response in such cases, and the response should
   simply not contain the information on the unknown `department_id` values.
   If all values are unknown, servers MUST respond with an empty `<response>`
   element. This requirement is true even when `<max-department-ids>` is `1`.

 * If the length of `department_id` list is greater than
   `<max-department-ids>`, servers MUST respond with HTTP 400.


Response
--------

Servers MUST respond with a valid XML document described by the [response.xsd]
(response.xsd) schema. See the schema annotations for further information.


Data model entities involved in the response
--------------------------------------------

 * Inst/Org Unit
 * Coordinator
 * Person
 * Academic Year?
 * Academic Term


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[institutions-api]: https://github.com/erasmus-without-paper/ewp-specs-api-institutions
