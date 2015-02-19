Available Hooks
=============

The following is a list of all hooks present in NodeBB. This list is intended to guide developers who are looking to write plugins for NodeBB. For more information, please consult :doc:`Writing Plugins for NodeBB <create>`.

There are two types of hooks, **filters**, and **actions**. Filters take an input (provided as a single argument), parse it in some way, and return the changed value. Actions take multiple inputs, and execute actions based on the inputs received. Actions do not return anything.

**Important**: This list is by no means exhaustive. Hooks are added on an as-needed basis (or if we can see a potential use case ahead of time), and all requests to add new hooks to NodeBB should be sent to us via the `issue tracker <https://github.com/NodeBB/NodeBB/issues>`_.


As of 2014-10-08 we have moved the list of hooks into our wiki page. Please consult the list `here <https://github.com/NodeBB/NodeBB/wiki/Hooks/>`_.