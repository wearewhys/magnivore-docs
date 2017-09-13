Introduction
=====================================

.. highlight:: javascript
    :linenothreshold: 5

Welcome to magnivore's documentation! Magnivore is a data migration tool
written in Python that can be configured through simple JSON configuration. In
essence, if you want to migrate a database without writing code, you
are in the right place.


Example
#######
Let's assume that magnivore is configured, shiny and ready to be used.
Then, let's also say that you have an old database with these tables and fields:

- users
    - id
    - email
    - address
    - city

and a new database with these tables and fields:

- users
    - id
    - username
- address_book
    - id
    - user_id
    - address
    - city

In the old database, users and addresses are in the same table, but now we want to
separete them so that in the new one users are on a table and addresses on
another.

The addresses will have a foreign key to the corresponding user - magnivore
will make sure that each address will be linked correctly to its corresponding
user.

We can now write a rules.json file for the users migration::

    {
        "users": {
            "joins": [
                {"table": "users"}
            ],
            "transform": {
                "username": "email"
            }
        },
        "track": "users_tracking"
    }

We will also write a addresses.json file, with rules for addresses migration::

    {
        "address_book": {
            "joins": [
                {"table": "users"}
            ],
            "transform": {
                "address": "address",
                "city": "city",
                "user_id" : {
                    "match": "id",
                    "from": "users_tracking"
                }
            }
        }
    }


And then launch magnivore:

.. code-block:: bash

    magnivore run rules.json
    magnivore run addresses.json

Done! You can check and see that the new database now has users with the
corresponding address, while the old table remains untouched.


.. toctree::
   :maxdepth: 2
   :hidden:

   installation
   configuration
   usage
   rulesets
   joins
   transform
   sync-track
   cookbook
