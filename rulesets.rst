Writing rulesets
================
.. highlight:: javascript
    :linenothreshold: 5


Instructions allow you to specify how a migration should be performed, in
general terms.

There are four instructions: label, joins, transform, sync, sync-transform and
track.


Label
-----
The label instruction is actually just a label: a string that can be used as
description or comment for the ruleset::

    {
        "mynewtable": {
            "label": "A description of the ruleset"
        }
    }
