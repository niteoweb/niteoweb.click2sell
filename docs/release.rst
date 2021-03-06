.. _releasing_a_new_version:

=======================
Releasing a new version
=======================

Releasing a new version of `niteoweb.click2sell` involves the following steps:

#. Create a git tag for the release.
#. Push the git tag upstream to GitHub.
#. Generate a distribution file for the package.
#. Upload the generated package to Python Package Index (PyPI).


Checklist
=========

Before every release make sure that:

#. You have documented your changes in the ``HISTORY.rst`` file.

#. You have modified the version identifier in the ``version.txt`` to reflect
   the new release.

#. You have confirmed that the package description (generated from
   ``README.rst`` and others) renders correctly by running ``bin/longtest``.

#. You have committed all changes to the git repository and pushed them
   upstream.

#. You have the working directory checked out at the revision you wish to
   release.


Actions
=======

For help with releasing we use ``jarn.mkreleaser``. It's listed as a dependency
in ``setup.py`` and should already be installed in your local bin:

.. sourcecode:: bash

    $ bin/mkrelease -d pypi -pq ./

.. note::
  In order to push packages to PyPI you need to have the appropriate access
  rights to the package on PyPI and you need to configure your PyPI credentials
  in the ``~/.pypirc`` file, e.g.::

    [distutils]
    index-servers =
      pypi

    [pypi]
    username = fred
    password = secret


Example
=======

In the following example we are releasing version 0.1 of `niteoweb.click2sell`. The
package has been prepared so that ``version.txt`` contains the version ``0.1``,
this change has been committed to git and all changes have been pushed
upstream to GitHub:

.. sourcecode:: bash

  # Check that package description is rendered correctly
  $ bin/longtest

  # Make a release and upload it to PyPI
  $ bin/mkrelease -d pypi -pq ./
  Releasing niteoweb.click2sell 0.1
  Tagging niteoweb.click2sell 0.1
  To git@github.com:niteoweb/niteoweb.click2sell.git
  * [new tag]         0.1 -> 0.1
  running egg_info
  running sdist
  warning: sdist: standard file not found: should have one of README, README.txt
  running register
  Server response (200): OK
  running upload
  warning: sdist: standard file not found: should have one of README, README.txt
  Server response (200): OK
  done

.. note::
  Please ignore the sdist warning about README file above. PyPI does not depend
  on it and it's just a bug in setupools (reported and waiting to be fixed).
