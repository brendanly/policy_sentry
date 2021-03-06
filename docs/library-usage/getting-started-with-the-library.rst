Getting Started with the Library
--------------------------------------

When using Policy Sentry manually, you have to build a local database file with the initialize function.

However, if you are developing your own Python code and you want to import Policy Sentry as a third party package, you can skip the initialization and leverage the local database file that is bundled with the Python package itself.

This is especially useful for developers who wish to leverage Policy Sentry's capabilities that require the use of the IAM database (such as querying the IAM database table). This way, you don't have to initialize the database and can just query it immediately.

The code example is  located `here <https://github.com/salesforce/policy_sentry/blob/master/examples/library-usage/example.py>`_. It is also shown below.

We've built a trick into the `connect_db` function that developers can specify to leverage the local database. The trick is to just use `'bundled'` as the single parameter for the `connect_db` method. See the example.

.. code-block:: python

    from policy_sentry.shared.database import connect_db
    from policy_sentry.querying.actions import get_actions_for_service


    def example():
        db_session = connect_db('bundled')  # This is the critical line. You just need to specify `'bundled'` as the parameter.
        actions = get_actions_for_service(db_session, 'cloud9')  # Then you can leverage any method that requires access to the database.
        for action in actions:
            print(action)


    if __name__ == '__main__':
        example()


Try running the code from the root of the repository:


.. code-block:: bash

    ./examples/library-usage/example.py

The results will look like this:

.. code-block:: text

    cloud9:createenvironmentec2
    cloud9:createenvironmentmembership
    cloud9:deleteenvironment
    cloud9:deleteenvironmentmembership
    cloud9:describeenvironmentmemberships
    cloud9:describeenvironmentstatus
    cloud9:describeenvironments
    cloud9:getusersettings
    cloud9:listenvironments
    cloud9:updateenvironment
    cloud9:updateenvironmentmembership
    cloud9:updateusersettings

