Changelog
=========

Unreleased
----------

- Make flask an optional dependency
- Remove the global es object in favor of explicitly passing it
- Python 3 compatibility

0.11.2
------

-  SECURITY: Fixed bug that allowed authenticated users to overwrite annotations
   on which they did not have permissions (#82).

0.11.1
------

-  Fixed support for using ElasticSearch instances behind HTTP Basic auth

0.11.0
------

-  Add support for ElasticSearch 1.0
-  Create changelog
