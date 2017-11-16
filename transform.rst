The transform section
=====================
The transform instruction is used to declare which columns will be migrated,
and how. In its simplest form, the data is moved as it is::

    {
        "mynewtable": {
            "joins": [...],
            "tranform": {
                "new_column": "old_column"
            }
        }
    }

Static
######
The static transformation simply fills in the specified value into the column.

This is useful when you have non-nullable columns in the new database, but the
original data does not always provide a value or when you need to set a foreign
key (or anything else) to an arbitrary value.

::

    "transform": {
        "new_column": {
            "static": "skyrim belongs to the nords"
        }
    }

Expression
##########
The expression transformation runs a regular expression on the original value.

::

    "transform": {
        "new_column": {
            "expression": "regexp",
            "from": "old_column"
        }
    }

Factor
######
Factor transforms a value multiplying it by a factor.

::

    "transform": {
        "new_column": {
            "factor": 2.8,
            "from": "old_column"
        }
    }


Format
######
Formats the original value using python's format function.

::

    "transform": {
        "new_column": {
            "from": "old_column"
            "format": "Now I am {}",
        }
    }

More columns can be specified::

    "new_column": {
        "from": ["old_column", "another_column"]
        "format": "{} and {} are best friends",
    }


Transform
#########
Transforms the original values following a switch-like pattern::

    "transform": {
        "new_column": {
            "from": "old_column",
            "transform": {
                "zero": 0,
                "one": 1
            }
        }
    }


Match
#####
Matches the original value against a previously tracked  and migrated item::

    "transform": {
        "new_column": {
            "match": "foreign_key_name",
            "from": "tracking_name"
        }
    }
