Release notes
=============

2.8.1
-----

Bugs
^^^^

* Restore defaults for three settings back to the values they had in Bodhi 2.7.0 (
  `#1633 <https://github.com/fedora-infra/bodhi/pull/1633>`_,
  `#1640 <https://github.com/fedora-infra/bodhi/pull/1640>`_, and
  `#1641 <https://github.com/fedora-infra/bodhi/pull/1641>`_).


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors submitted patches for Bodhi 2.8.1:

* Patrick Uiterwijk (the true 2.8.1 hero)
* Randy Barlow


2.8.0
-----

Special instructions
^^^^^^^^^^^^^^^^^^^^

* There is a new setting, ``ci.required`` that defaults to False. If you wish to use CI, you must
  add a cron task to call the new ``bodhi-babysit-ci`` CLI periodically.


Deprecation
^^^^^^^^^^^

The ``/search/packages`` API call has been deprecated.


New Dependencies
^^^^^^^^^^^^^^^^

* Bodhi now uses Bleach to sanitize markdown input from the user.
  python-bleach 1.x is a new dependency in this release of Bodhi.


Features
^^^^^^^^

* The API, fedmsg messages, bindings, and CLI now support non-RPM content (
  `#1325 <https://github.com/fedora-infra/bodhi/issues/1325>`_,
  `#1326 <https://github.com/fedora-infra/bodhi/issues/1326>`_,
  `#1327 <https://github.com/fedora-infra/bodhi/issues/1327>`_, and
  `#1328 <https://github.com/fedora-infra/bodhi/issues/1328>`_).
  Bodhi now knows about Fedora's new module format, and is able to handle everything they need
  except publishing (which will appear in a later release). This release is also the first Bodhi
  release that is able to handle multiple content types.
* Improved OpenQA support in the web UI
  (`#1471 <https://github.com/fedora-infra/bodhi/issues/1471>`_).
* The type icons are now aligned in the web UI
  (`4b6b7597 <https://github.com/fedora-infra/bodhi/commit/4b6b7597>`_ and
  `d0940323 <https://github.com/fedora-infra/bodhi/commit/d0940323>`_).
* There is now a man page for ``bodhi-approve-testing``
  (`cf8d897f <https://github.com/fedora-infra/bodhi/commit/cf8d897f>`_).
* Bodhi can now automatically detect whether to use DDL table locks if BDR is present during
  migrations (`059b5ab7 <https://github.com/fedora-infra/bodhi/commit/059b5ab7>`_).
* Locked updates now grey out the edit buttons with a tooltip to make the lock more obvious to the
  user (`#1492 <https://github.com/fedora-infra/bodhi/issues/1492>`_).
* Users can now do multi-line literal code blocks in comments
  (`#1509 <https://github.com/fedora-infra/bodhi/issues/1509>`_).
* The web UI now has more descriptive placeholder text
  (`1a7122cd <https://github.com/fedora-infra/bodhi/commit/1a7122cd>`_).
* All icons now have consistent width in the web UI
  (`6dfe6ff3 <https://github.com/fedora-infra/bodhi/commit/6dfe6ff3>`_).
* The front page has a new layout
  (`6afb6b07 <https://github.com/fedora-infra/bodhi/commit/6afb6b07>`_).
* Bodhi is now able to use Pagure and PDC as sources for ACL and package information
  (`59551861 <https://github.com/fedora-infra/bodhi/commit/59551861>`_).
* Bodhi's configuration loader now validates all values and centralizes defaults. Thus, it is now
  possible to comment most of Bodhi's settings file and achieve sane defaults. Some settings are
  still required, see the default ``production.ini`` file for documentation of all settings and
  their defaults. A few unused settings were removed
  (`#1488 <https://github.com/fedora-infra/bodhi/issues/1488>`_,
  `#1489 <https://github.com/fedora-infra/bodhi/issues/1489>`_, and
  `263b7b7f <https://github.com/fedora-infra/bodhi/commit/263b7b7f>`_).
* The web UI now displays the content type of the update
  (`#1329 <https://github.com/fedora-infra/bodhi/issues/1329>`_).
* Bodhi now has a new ``ci.required`` setting that defaults to False. If enabled. updates will gate
  based on Continuous Integration test results and will not proceed to updates-testing unless the
  tests pass
  (`0fcb73f8 <https://github.com/fedora-infra/bodhi/commit/0fcb73f8>`_).
* Update builds are now sorted by NVR
  (`#1441 <https://github.com/fedora-infra/bodhi/issues/1441>`_).
* The backend code is reworked to allow gating on resultsdb data and requirement validation
  performance is improved
  (`#1550 <https://github.com/fedora-infra/bodhi/issues/1550>`_).
* Bodhi is now able to map distgit commits to Builds, which helps map CI results to Builds. There is
  a new ``bodhi-babysit-ci`` CLI that must be run periodically in cron if ``ci.required`` is
  ``True``
  (`ae01e5d1 <https://github.com/fedora-infra/bodhi/commit/ae01e5d1>`_).


Bugs
^^^^

* A half-hidden button is now fully visible on mobile devices
  (`#1467 <https://github.com/fedora-infra/bodhi/issues/1467>`_).
* The signing status is again visible on the update page
  (`#1469 <https://github.com/fedora-infra/bodhi/issues/1469>`_).
* The edit update form will not be presented to users who are not auth'd
  (`#1521 <https://github.com/fedora-infra/bodhi/issues/1521>`_).
* The CLI ``--autokarma`` flag now works correctly
  (`#1378 <https://github.com/fedora-infra/bodhi/issues/1378>`_).
* E-mail subjects are now shortened like the web UI titles
  (`#882 <https://github.com/fedora-infra/bodhi/issues/882>`_).
* The override editing form is no longer displayed unless the user is logged in
  (`#1541 <https://github.com/fedora-infra/bodhi/issues/1541>`_).


Development improvements
^^^^^^^^^^^^^^^^^^^^^^^^

* Several more modules now pass pydocstyle PEP-257 tests.
* The development environment has a new ``bshell`` alias that sets up a usable Python shell,
  initialized for Bodhi.
* Lots of warnings from the unit tests have been fixed.
* The dev environment cds to the source folder upon ``vagrant ssh``.
* There is now a ``bfedmsg`` development alias to see fedmsgs.
* A new ``bresetdb`` development alias will reset the database to the same state as when
  ``vagrant up`` completed.
* Some unused code was removed
  (`afe5bd8c <https://github.com/fedora-infra/bodhi/commit/afe5bd8c>`_).
* Test coverage was raised significantly, from 85% to 88%.
* The development environment now has httpie by default.
* The default Vagrant memory was raised
  (`#1588 <https://github.com/fedora-infra/bodhi/issues/1588>`_).
* Bodhi now has a Jenkins Job Builder template for use with CentOS CI.
* A new ``bdiff-cover`` development alias helps compare test coverage in current branch to the
  ``develop`` branch, and will alert the developer if there are any lines missing coverage.


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following developers contributed to Bodhi 2.8.0:

* Ryan Lerch
* Ralph Bean
* Pierre-Yves Chibon
* Matt Prahl
* Martin Curlej
* Adam Williamson
* Kamil Páral
* Clement Verna
* Jeremy Cline
* Matthew Miller
* Randy Barlow


2.7.0
-----

Features
^^^^^^^^

* The bodhi CLI now supports editing an override.
  (`#1049 <https://github.com/fedora-infra/bodhi/issues/1049>`_).
* The Update model is now capable of being associated with different Build types
  (`#1394 <https://github.com/fedora-infra/bodhi/issues/1394>`_).
* The bodhi CLI now supports editing an update using the update alias.
  (`#1409 <https://github.com/fedora-infra/bodhi/issues/1409>`_).
* The web UI now uses Fedora 26 in its example text instead of Fedora 20
  (`ec0c619a <https://github.com/fedora-infra/bodhi/commit/ec0c619a>`_).
* The Build model is now polymorphic to support non-RPM content
  (`#1393 <https://github.com/fedora-infra/bodhi/issues/1393>`_).


Bugs
^^^^

* Correctly calculate days to stable for critical path updates
  (`#1386 <https://github.com/fedora-infra/bodhi/issues/1386>`_).
* Bodhi now logs some messages at info instead of error
  (`#1412 <https://github.com/fedora-infra/bodhi/issues/1412>`_).
* Only show openQA results since last update modification
  (`#1435 <https://github.com/fedora-infra/bodhi/issues/1435>`_).


Development improvements
^^^^^^^^^^^^^^^^^^^^^^^^

* SQL queries are no longer logged by default.
* fedmsgs are now viewable in the development environment.
* There is a new test to ensure there is only one Alembic head.
* There is a new bash alias, bteststyle, that runs the code style tests.
* The BuildrootOverride model is now documented.


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors submitted patches for Bodhi 2.7.0:

* Clement Verna
* Jeremy Cline
* Bianca Nenciu
* Caleigh Runge-Hottman
* Adam Williamson
* Robert Scheck
* Ryan Lerch
* Randy Barlow


2.6.2
-----

This release focused on CLI authentication issues. One of the issues requires users to also update
their python-fedora installation to at least 0.9.0.


Bugs
^^^^

* The CLI is now able to appropriately handle expiring sessions
  (`#1474 <https://github.com/fedora-infra/bodhi/issues/1474>`_).
* The CLI now only prompts for a password when needed
  (`#1500 <https://github.com/fedora-infra/bodhi/pull/1500>`_).
* Don't traceback if the user doesn't use the ``--user`` flag
  (`#1505 <https://github.com/fedora-infra/bodhi/pull/1505>`_).


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors submitted patches for Bodhi 2.6.2:

* Randy Barlow


2.6.1
-----

This release fixes 4 issues with three commits.


Bugs
^^^^

* Web requests now use the correct session for transactions
  (`#1470 <https://github.com/fedora-infra/bodhi/issues/1470>`_,
  `#1473 <https://github.com/fedora-infra/bodhi/issues/1473>`_).
* fedmsgs are now converted to dictionaries before queuing
  (`#1472 <https://github.com/fedora-infra/bodhi/issues/1472>`_).
* Error messages are still logged if rolling back the transaction raises an Exception
  (`#1475 <https://github.com/fedora-infra/bodhi/issues/1475>`_).


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors submitted patches for Bodhi 2.6.1:

* Jeremy Cline
* Randy Barlow


2.6.0
-----

Special instructions
^^^^^^^^^^^^^^^^^^^^

#. The database migrations have been trimmed in this release. To upgrade to this version of Bodhi
   from a version prior to 2.3, first upgrade to Bodhi 2.3, 2.4, or 2.5, run the database
   migrations, and then upgrade to this release.
#. Bodhi cookies now expire, but cookies created before 2.6.0 will not automatically expire. To
   expire all existing cookies so that only expiring tickets exist, you will need to change
   ``authtkt.secret`` to a new value in your settings file.


Dependency adjustments
^^^^^^^^^^^^^^^^^^^^^^

* zope.sqlalchemy is no longer a required dependency
  (`#1414 <https://github.com/fedora-infra/bodhi/pull/1414>`_).
* WebOb is no longer a directly required dependency, though it is still indirectly required through
  pyramid.


Features
^^^^^^^^

* The web UI footer has been restyled to fit better with the new theme
  (`#1366 <https://github.com/fedora-infra/bodhi/pull/1366>`_).
* A link to documentation has been added to the web UI footer
  (`#1321 <https://github.com/fedora-infra/bodhi/issues/1321>`_).
* The bodhi CLI now supports editing updates
  (`#937 <https://github.com/fedora-infra/bodhi/issues/937>`_).
* The CLI's ``USERNAME`` environment variable is now documented, and its ``--user`` flag is
  clarified (`28dd380a <https://github.com/fedora-infra/bodhi/commit/28dd380a>`_).
* The icons that we introduced in the new theme previously didn't have titles.
  Consequently, a user might not have know what these icons meant. Now if a user
  hovers over these icons, they get a description of what they mean, for
  example: "This is a bugfix update" or "This update is in the critial path"
  (`#1362 <https://github.com/fedora-infra/bodhi/issues/1362>`_).
* Update pages with lots of updates look cleaner
  (`#1351 <https://github.com/fedora-infra/bodhi/issues/1351>`_).
* Update page titles are shorter now for large updates
  (`#957 <https://github.com/fedora-infra/bodhi/issues/957>`_).
* Add support for alternate architectures to the MasherThread.wait_for_sync()
  (`#1343 <https://github.com/fedora-infra/bodhi/issues/1343>`_).
* Update lists now also include type icons next to the updates
  (`5983d99c <https://github.com/fedora-infra/bodhi/commit/5983d99c>`_).
* Testing updates use a consistent label color now
  (`62330644 <https://github.com/fedora-infra/bodhi/commit/62330644>`_).
* openQA results are now displayed in the web ui
  (`450dbafe <https://github.com/fedora-infra/bodhi/commit/450dbafe>`_).
* Bodhi cookies now expire. There is a new ``authtkt.timeout`` setting that sets Bodhi's session
  lifetime, defaulting to 1 day.


Bugs
^^^^

* Comments that don't carry karma don't count as a user's karma vote
  (`#829 <https://github.com/fedora-infra/bodhi/issues/829>`_).
* The web UI now uses the update alias instead of the title so editors of large updates can click
  the edit button (`#1161 <https://github.com/fedora-infra/bodhi/issues/1161>`_).
* Initialize the bugtracker in ``main()`` instead of on import so that docs can be built without
  installing Bodhi (`#1359 <https://github.com/fedora-infra/bodhi/pull/1359>`_).
* Make the release graph easier to read when there are many datapoints
  (`#1172 <https://github.com/fedora-infra/bodhi/issues/1172>`_).
* Optimize the JavaScript that loads automated test results from ResultsDB
  (`#983 <https://github.com/fedora-infra/bodhi/issues/983>`_).
* Bodhi's testing approval comment now respects the karma reset event
  (`#1310 <https://github.com/fedora-infra/bodhi/issues/1310>`_).
* ``pop`` and ``copy`` now lazily load the configuration
  (`#1423 <https://github.com/fedora-infra/bodhi/issues/1423>`_).


Development improvements
^^^^^^^^^^^^^^^^^^^^^^^^

* A new automated PEP-257 test has been introduced to enforce docblocks across the codebase.
  Converting the code will take some time, but the code will be expanded to fully support PEP-257
  eventually. A few modules have now been documented.
* Test coverage is now 84%.
* The Vagrant environment now has vim with a simple vim config to make sure spaces are used instead
  of tabs (`#1372 <https://github.com/fedora-infra/bodhi/pull/1372>`_).
* The Package database model has been converted into a single-table inheritance model, which will
  aid in adding multi-type support to Bodhi. A new RpmPackage model has been added.
  (`#1392 <https://github.com/fedora-infra/bodhi/pull/1392>`_).
* The database initialization code is unified
  (`e9a26042 <https://github.com/fedora-infra/bodhi/commit/e9a26042>`_).
* The base model class now has a helpful query property
  (`8167f262 <https://github.com/fedora-infra/bodhi/commit/8167f262>`_).
* .pyc files are now removed when running the tests in the dev environment
  (`9e9adb61 <https://github.com/fedora-infra/bodhi/commit/9e9adb61>`_).
* An unused inherited column has been dropped from the builds table
  (`e8a95b12 <https://github.com/fedora-infra/bodhi/commit/e8a95b12>`_).


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors submitted patches for Bodhi 2.6.0:

* Jeremy Cline
* Ryan Lerch
* Clement Verna
* Caleigh Runge-Hottman
* Bianca Nenciu
* Adam Williamson
* Ankit Raj Ojha
* Jason Taylor
* Randy Barlow


2.5.0
-----

Bodhi 2.5.0 is a feature and bugfix release.


Features
^^^^^^^^

* The web interface now uses the Fedora Bootstrap theme. The layout of the
  update page has also been revamped to display the information about an update
  in a clearer manner.
  (`#1313 <https://github.com/fedora-infra/bodhi/issues/1313>`_).
* The ``bodhi`` CLI now has a ``--url`` flag that can be used to switch which Bodhi server it
  communicates with. The ``BODHI_URL`` environment can also be used to configure this flag.
* The documentation has been reorganized.
* The Python bindings are now documented.
* Bodhi will now announce that karma has been reset to 0 when builds are added or removed from
  updates (`6d6de4bc <https://github.com/fedora-infra/bodhi/commit/6d6de4bc>`_).
* Bodhi will now announce that autokarma has been disabled when an update received negative karma
  (`d3ccc579 <https://github.com/fedora-infra/bodhi/commit/d3ccc579>`_).
* The docs theme is now Alabaster
  (`57a80f42 <https://github.com/fedora-infra/bodhi/commit/57a80f42>`_).
* The Bodhi documentation now has a description of Bodhi on the landing page
  (`#1322 <https://github.com/fedora-infra/bodhi/issues/1322>`_).
* The REST API is now documented
  (`#1323 <https://github.com/fedora-infra/bodhi/issues/1323>`_).
* The client Python bindings can now accept a ``base_url`` that doesn't end in a slash
  (`1087939b <https://github.com/fedora-infra/bodhi/commit/1087939b>`_).


Bugs
^^^^
* The position of the Add Comment button is now the bottom right.
  (`#902 <https://github.com/fedora-infra/bodhi/issues/902>`_).
* An unusuable ``--request`` flag has been removed from a CLI command
  (`#1187 <https://github.com/fedora-infra/bodhi/issues/1187>`_).
* The cursor is now a pointer when hovering over Releases button
  (`#1296 <https://github.com/fedora-infra/bodhi/issues/1296>`_).
* The number of days to stable is now correctly calculated on updates
  (`#1305 <https://github.com/fedora-infra/bodhi/issues/1305>`_).
* Fix a query regular expression so that Fedora update ids work
  (`d5bec3fa <https://github.com/fedora-infra/bodhi/commit/d5bec3fa>`_).
* Karma thresholds can now be set when autopush is disabled
  (`#1033 <https://github.com/fedora-infra/bodhi/issues/1033>`_).


Development improvements
^^^^^^^^^^^^^^^^^^^^^^^^

* The Vagrant development environment automatically configures the BODHI_URL environment
  variable so that the client talks to the local server instead of production or staging.
* Test coverage is up another percentage to 82%.
* Bodhi is now PEP-8 compliant.
* The development environment now displays all Python warnings once.


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following developers contributed to Bodhi 2.5.0:

* Ryan Lerch
* Trishna Guha
* Jeremy Cline
* Ankit Raj Ojha
* Ariel O. Barria
* Randy Barlow


2.4.0
-----

Bodhi 2.4.0 is a feature and bugfix release.


Features
^^^^^^^^
* The web interface now displays whether an update has autopush enabled
  (`#999 <https://github.com/fedora-infra/bodhi/issues/999>`_).
* Autopush is now disabled on any update that receives authenticated negative karma
  (`#1191 <https://github.com/fedora-infra/bodhi/issues/1191>`_).
* Bodhi now links to Koji builds via TLS instead of plaintext
  (`#1246 <https://github.com/fedora-infra/bodhi/issues/1246>`_).
* Some usage examples have been added to the ``bodhi`` man page.
* Bodhi's server package has a new script called ``bodhi-clean-old-mashes`` that can recursively
  delete any folders with names that end in a dash followed by a string that can be interpreted as a
  float, sparing the newest 10 by lexigraphical sorting. This should help release engineers keep the
  Koji mashing folder clean.
* There is now a ``bodhi.client.bindings`` module provided by the Bodhi client package. It contains
  Python bindings to Bodhi's REST API.
* The ``bodhi`` CLI now prints autokarma and thresholds when displaying updates.
* ``bodhi-push`` now has a ``--version`` flag.
* There are now man pages for ``bodhi-push`` and ``initialize_bodhi_db``.


Bugs
^^^^
* Users' e-mail addresses will now be updated when they log in to Bodhi
  (`#902 <https://github.com/fedora-infra/bodhi/issues/902>`_).
* The masher now tests for ``repomd.xml`` instead of the directory that contains it
  (`#908 <https://github.com/fedora-infra/bodhi/issues/908>`_).
* Users can now only upvote an update once
  (`#1018 <https://github.com/fedora-infra/bodhi/issues/1018>`_).
* Only comment on non-autokarma updates when they meet testing requirements
  (`#1009 <https://github.com/fedora-infra/bodhi/issues/1009>`_).
* Autokarma can no longer be set to NULL
  (`#1048 <https://github.com/fedora-infra/bodhi/issues/1048>`_).
* Users can now be more fickle than ever about karma
  (`#1064 <https://github.com/fedora-infra/bodhi/issues/1064>`_).
* Critical path updates can now be free of past negative karma ghosts
  (`#1065 <https://github.com/fedora-infra/bodhi/issues/1065>`_).
* Bodhi now comments on non-autokarma updates after enough time has passed
  (`#1094 <https://github.com/fedora-infra/bodhi/issues/1094>`_).
* ``bodhi-push`` now does not crash when users abort a push
  (`#1107 <https://github.com/fedora-infra/bodhi/issues/1107>`_).
* ``bodhi-push`` now does not print updates when resuming a push
  (`#1113 <https://github.com/fedora-infra/bodhi/issues/1113>`_).
* Bodhi now says "Log in" and "Log out" instead of "Login" and "Logout"
  (`#1146 <https://github.com/fedora-infra/bodhi/issues/1146>`_).
* Bodhi now configures the Koji client to retry, which should help make the masher more reliable
  (`#1201 <https://github.com/fedora-infra/bodhi/issues/1201>`_).
* Bodhi is now compatible with Pillow-4.0.0
  (`#1262 <https://github.com/fedora-infra/bodhi/issues/1262>`_).
* The bodhi cli no longer prints update JSON when setting the request
  (`#1408195 <https://bugzilla.redhat.com/show_bug.cgi?id=1408195>`_).
* Bodhi's signed handler now skips builds that were not assigned to a release.
* The comps file is now cloned into an explicit path during mashing.
* The buildsystem is now locked during login.


Development improvements
^^^^^^^^^^^^^^^^^^^^^^^^
* A great deal of tests were written for Bodhi. Test coverage is now up to 81% and is enforced by
  the test suite.
* Bodhi's server code is now PEP-8 compliant.
* The docs now contain contribution guidelines.
* The build system will now fail with a useful Exception if used without being set up.
* The Vagrantfile is a good bit fancier, with hostname, dnf caching, unsafe but performant disk I/O,
  and more.
* The docs now include a database schema image.
* Bodhi is now run by systemd in the Vagrant guest.
* The Vagrant environment now has several helpful shell aliases and a helpful MOTD to advertise
  them to developers.
* The development environment now uses Fedora 25 by default.
* The test suite is less chatty, as several unicode warnings have been fixed.


Dependency change
^^^^^^^^^^^^^^^^^
* Bodhi server now depends on click for ``bodhi-push``.


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors submitted patches for Bodhi 2.4.0:

* Trishna Guha
* Patrick Uiterwijk
* Jeremy Cline
* Till Mass
* Josef Sukdol
* Clement Verna
* andreas
* Ankit Raj Ojha
* Randy Barlow


2.3.3
-----

Bodhi 2.3.3 converts koji auth to be done with krb5 and fixes one bug:

* Use krb5 for koji
  (`#1129 <https://github.com/fedora-infra/bodhi/pull/1129>`_).
* Disable caching koji sessions during mashing process
  (`#1134 <https://github.com/fedora-infra/bodhi/pull/1134>`_).


Thanks to Patrick Uiterwijk for contributing both of these commits!


2.3.2
-----

Bodhi 2.3.2 is a bugfix release that addresses the following issues:

* ``push.py`` now defaults to the current releases
  (`#1071 <https://github.com/fedora-infra/bodhi/issues/1071>`_).
* Fixed a typo in the masher in sending an ostree compose message
  (`#1072 <https://github.com/fedora-infra/bodhi/pull/1072>`_).
* Fixed a typo in looking up an e-mail template
  (`#1073 <https://github.com/fedora-infra/bodhi/issues/1073>`_).
* The fedmsg name is now passed explicitly
  (`#1079 <https://github.com/fedora-infra/bodhi/pull/1079>`_).
* The man page was corrected to state that builds should be comma separated
  (`#1095 <https://github.com/fedora-infra/bodhi/pull/1095>`_).
* Fixed a race condition between robosignatory and the signed handler
  (`#1111 <https://github.com/fedora-infra/bodhi/issues/1111>`_).
* Fix querying the updates for resumption in ``push.py``
  (`e7cb3f13 <https://github.com/fedora-infra/bodhi/commit/e7cb3f13>`_).
* ``push.py`` now prompts for the username if not given
  (`abeca57e <https://github.com/fedora-infra/bodhi/commit/abeca57e>`_).


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors authored patches for 2.3.2:

* Patrick Uiterwijk
* Randy Barlow


2.3.1
-----

Bodhi 2.3.1 fixes `#1067 <https://github.com/fedora-infra/bodhi/issues/1067>`_,
such that edited updates now tag new builds into the ``pending_signing_tag``
instead of the ``pending_testing_tag``. This is needed for automatic signing
gating to work.


2.3.0
-----

Bodhi 2.3.0 is a feature and bug fix release.

Features
^^^^^^^^

* The package input field is now autofocused when creating new updates
  (`#876 <https://github.com/fedora-infra/bodhi/pull/876>`_).
* Releases now have a ``pending_signing_tag``
  (`3fe3e219 <https://github.com/fedora-infra/bodhi/commit/3fe3e219>`_).
* fedmsg notifications are now sent during ostree compositions
  (`b972cad0 <https://github.com/fedora-infra/bodhi/commit/b972cad0>`_).
* Critical path updates will have autopush disabled if they receive negative karma
  (`b1f71006 <https://github.com/fedora-infra/bodhi/commit/b1f71006>`_).
* The e-mail templates reference dnf for Fedora and yum for Enterprise Linux
  (`1c1f2ab7 <https://github.com/fedora-infra/bodhi/commit/1c1f2ab7>`_).
* Updates are now obsoleted if they reach the unstable threshold while pending
  (`f033c74c <https://github.com/fedora-infra/bodhi/commit/f033c74c>`_).
* Bodhi now gates Updates based on whether they are signed yet or not
  (`#1011 <https://github.com/fedora-infra/bodhi/pull/1011>`_).


Bugs
^^^^

* Candidate builds and bugs are no longer duplicated while searching
  (`#897 <https://github.com/fedora-infra/bodhi/issues/897>`_).
* The Bugzilla connection is only initialized when needed
  (`950eee2c <https://github.com/fedora-infra/bodhi/commit/950eee2c>`_).
* A sorting issue was fixed on the metrics page so the data is presented correctly
  (`487acaaf <https://github.com/fedora-infra/bodhi/commit/487acaaf>`_).
* The Copyright date in the footer of the web interface is updated
  (`1447b6c7 <https://github.com/fedora-infra/bodhi/commit/1447b6c7>`_).
* Bodhi will comment with the required time instead of the elapsed time on updates
  (`#1017 <https://github.com/fedora-infra/bodhi/issues/1017>`_).
* Bodhi will only comment once to say that non-autopush updates have reached the threshold
  (`#1009 <https://github.com/fedora-infra/bodhi/issues/1009>`_).
* ``/masher/`` is now allowed in addition to ``/masher`` for GET requests
  (`cdb621ba <https://github.com/fedora-infra/bodhi/commit/cdb621ba>`_).


Dependencies
^^^^^^^^^^^^

Bodhi now depends on fedmsg-atomic-composer >= 2016.3, which addresses a few issues during mashing.


Development improvements
^^^^^^^^^^^^^^^^^^^^^^^^

Bodhi 2.3.0 also has a few improvements to the development environment that make it easier to
contribute to Bodhi or improve Bodhi's automated tests:

* Documentation was added to describe how to connect development Bodhi to staging Koji
  (`7f3b5fa2 <https://github.com/fedora-infra/bodhi/commit/7f3b5fa2>`_).
* An unused ``locked_date_for_update()`` method was removed
  (`b87a6395 <https://github.com/fedora-infra/bodhi/commit/b87a6395>`_).
* The development.ini.example base_address was changed to localhost so requests would be allowed
  (`0fd5901d <https://github.com/fedora-infra/bodhi/commit/0fd5901d>`_).
* The ``setup.py`` file has more complete metadata, making it more suitable for submission to PyPI
  (`5c201ac2 <https://github.com/fedora-infra/bodhi/commit/5c201ac2>`_).
* The #bodhi and #fedora-apps channels are now documented in the readme file
  (`52093069 <https://github.com/fedora-infra/bodhi/commit/52093069>`_).
* A new test has been added to enforce PEP-8 style and a few modules have been converted to conform
  (`bbafc9e6 <https://github.com/fedora-infra/bodhi/commit/bbafc9e6>`_).


Release contributors
^^^^^^^^^^^^^^^^^^^^

The following contributors authored patches for 2.3.0:

* Josef Sukdol
* Julio Faracco
* Patrick Uiterwijk
* Randy Barlow
* Richard Fearn
* Trishna Guha


2.2.4
-----

This release fixes two issues:

* `#989 <https://github.com/fedora-infra/bodhi/issues/989>`_, where Karma on
  non-autopush updates would reset the request to None.
* `#994 <https://github.com/fedora-infra/bodhi/issues/994>`_, allowing Bodhi to
  be built on setuptools-28.


2.2.3
-----

This release fixes `#951 <https://github.com/fedora-infra/bodhi/issues/951>`_, which prevented
updates with large numbers of packages to be viewable in web browsers.


2.2.2
-----

This is another in a series of bug fix releases for Bodhi this week. In this release, we've fixed
the following issues:

* Disallow comment text to be set to the NULL value in the database
  (`#949 <https://github.com/fedora-infra/bodhi/issues/949>`_).
* Fix autopush on updates that predate the 2.2.0 release
  (`#950 <https://github.com/fedora-infra/bodhi/issues/950>`_).
* Don't wait on mashes when there aren't any
  (`68de510c <https://github.com/fedora-infra/bodhi/commit/68de510c>`_).


2.2.1
-----

Bodhi 2.2.1 is a bug fix release, primarily focusing on mashing issues:

* Register date locked during mashing (`#952
  <https://github.com/fedora-infra/bodhi/issues/952>`_).
* UTF-8 encode the updateinfo before writing it to disk (`#955
  <https://github.com/fedora-infra/bodhi/issues/955>`_).
* Improved logging during updateinfo generation (`#956
  <https://github.com/fedora-infra/bodhi/issues/956>`_).
* Removed some unused code
  (`07ff664f <https://github.com/fedora-infra/bodhi/commit/07ff664f>`_).
* Fix some incorrect imports
  (`9dd5bdbc <https://github.com/fedora-infra/bodhi/commit/9dd5bdbc>`_ and
  `b1cc12ad <https://github.com/fedora-infra/bodhi/commit/b1cc12ad>`_).
* Rely on self.skip_mash to detect when it is ok to skip a mash
  (`ad65362e <https://github.com/fedora-infra/bodhi/commit/ad65362e>`_).


2.2.0
-----

Bodhi 2.2.0 is a security and feature release, with a few bug fixes as well.


Security
^^^^^^^^

This update addresses `CVE-2016-1000008 <https://github.com/fedora-infra/bodhi/pull/857>`_ by
disallowing the re-use of solved captchas. Additionally, the captcha is
`warped <https://github.com/fedora-infra/bodhi/commit/f0122855>`_ to make it more difficult to
solve through automation. Thanks to Patrick Uiterwijk for discovering and reporting this issue.


Features
^^^^^^^^

* Bodhi's ``approve_testing.py`` script will now comment on updates when they have reached a stable
  karma threshold
  (`5b0d1c7c <https://github.com/fedora-infra/bodhi/commit/5b0d1c7c>`_).
* The web interface now displays a push to stable button when the karma reaches the right level when
  autokarma is disabled
  (`#772 <https://github.com/fedora-infra/bodhi/issues/772>`_ and
  `#796 <https://github.com/fedora-infra/bodhi/issues/796>`_).
* Masher messages now have an "agent", so it is possible to tell which user ran the mash
  (`45e4fc9f <https://github.com/fedora-infra/bodhi/commit/45e4fc9f>`_).
* Locked updates now list the time they were locked
  (`#831 <https://github.com/fedora-infra/bodhi/issues/831>`_).
* Bugs are closed and commented on in the same Bugzilla POST
  (`#404 <https://github.com/fedora-infra/bodhi/issues/404>`_).
* Karma values equal to 0 are no longer displayed with a green background to better distinguish them
  from positive karma reports (`#799 <https://github.com/fedora-infra/bodhi/issues/799>`_).
* Updates display a link to the feedback guidelines
  (`#865 <https://github.com/fedora-infra/bodhi/issues/865>`_).
* The new CLI now has a man page
  (`95574831 <https://github.com/fedora-infra/bodhi/commit/95574831>`_).
* The CLI now has a ``--version`` flag (`#895 <https://github.com/fedora-infra/bodhi/issues/895>`_).


Bugs
^^^^

* Locked updates that aren't part of a current push will now be pushed and warnings will be logged
  (`bf4bdeef <https://github.com/fedora-infra/bodhi/commit/bf4bdeef>`_). This should help us to fix
  `#838 <https://github.com/fedora-infra/bodhi/issues/838>`_.
* Don't show users an option to push to stable on obsoleted updates
  (`#848 <https://github.com/fedora-infra/bodhi/issues/848>`_).
* taskotron updates are shown per build, rather than per update
  (`ce2394c6 <https://github.com/fedora-infra/bodhi/commit/ce2394c6>`_,
  `8e199668 <https://github.com/fedora-infra/bodhi/commit/8e199668>`_).
* The Sphinx documentation now builds again
  (`b3f80b1b <https://github.com/fedora-infra/bodhi/commit/b3f80b1b>`_).
* Validator messages are now more useful and helpful
  (`#630 <https://github.com/fedora-infra/bodhi/issues/630>`_).
* The Bodhi CLI no longer depends on the server code to function
  (`#900 <https://github.com/fedora-infra/bodhi/issues/900>`_).
* Private bugs will no longer prevent the updates consumer from continuing
  (`#905 <https://github.com/fedora-infra/bodhi/issues/905>`_).
* bootstrap is now included in the setuptools manifest for the server package
  (`#919 <https://github.com/fedora-infra/bodhi/issues/919>`_).


Commit log
^^^^^^^^^^

The above lists are the highlights of what changed. For a full list of the changes since 2.1.8,
please see the
`changelog <https://github.com/fedora-infra/bodhi/compare/2.1.8...2.2.0>`_.
