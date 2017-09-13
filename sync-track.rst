Tracking and syncing items
===========================

Track
-----
::

    "track": "foreignkeyname"

The track instruction can be used to record old items' ids and their new ids,
so that they can be retrieved later. It is used in conjunction with the
match rule, placed in another ruleset.

This ensures that foreign keys will still relate to the same item, even if
their ids are changed.


Sync and sync-transform
-----------------------
Sync and sync-transform are strictly related instructions and they are used
together.

Sync changes the migration behaviour, updating items rather than
creating new ones. The items that need to be updated must have been tracked::

    "sync": {
        "from": "tracking_name",
        "attribute": "id"
    }

Then, instead of using transform, we will use sync-transform::

    "sync-transform": {
        "new_column": "old_column"
    },
    "sync": {
        "from": "tracking_name",
        "attribute": "id"
    }
