The sources section
=================
Sources are used to specify how to collect data from the source database. They
can have four properties: table, on, switch, conditions and aggregation.

Table
#####
The table from which data will be taken. If it's not the first table, you must
specify the *on* property.


::

    {
        "mynewtable": {
            "sources": [
                {"table": "tablename"}
            ]
        }
    }

On
##
The on property is used to specify join condition when retrieving data from
multiple tables.

::

    {
        "mynewtable": {
            "sources": [
                {"table": "tablename"},
                {"table": "related_table", "on": "foreignkey_to_tablename"}
            ]
        }
    }

If the table does not have a foreign key, but the data is still related, you
can specify both columns::

    {
        "table": "related_table",
        "on": [
            "tablename_primary_key",
            "relatedtable_reference_column"
        ]
    }



Switch
######
The switch property allows to set the context back to the original table.
This is useful when joining three or more tables.


::

    {
        "mynewtable": {
            "sources": [
                {"table": "tablename"},
                {"table": "related_table", "on": "foreignkey_to_tablename"},
                {"table": "yet_another",
                  "on": "foreignkey_to_tablename",
                  "switch": true
                }
            ]
        }
    }

Conditions
##########
The conditions that retrieved data must abide. These are translated to where
queries. For example, to get items with colour equal to blue::

    {
        "mynewtable": {
            "sources": [
                {
                    "table": "pens",
                    "conditions": {
                        "colour": "blue"
                    }
                }
            ]
        }
    }

You can specify a different operator. Conditions support *gt*, *not*, *lt*,
*in* and *isnull* as operators::

    "conditions": {
        "ink_level": {
            "operator": "gt",
            "value": 5
        }
    }

Aggregation
###########
Aggregations can be used instead of condiitions, placing constraints on groups
of items rather than each::

    "aggregation": {
        "function": "count",
        "group": "field",
        "condition": {
            "operator": "eq",
            "value": 1
        }
    }

Function, group and condition control the aggregation parameters:

- function: The function to be used to aggregate data. Only count is supported.
- group: The field on which the aggregation will be performed
- condition: The condition that the aggregation has to abide
