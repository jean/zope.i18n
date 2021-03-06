=======
CHANGES
=======

4.0.0 (2014-12-20)
--------------------

- Added support for testing with Travis.

- Added explicit support for Python 3.4 and PyPy.


4.0.0a4 (2013-02-18)
--------------------

- Restore zope.i18n.testing.{setUp,PlacelessSetup} that got lost in 4.0.0a3.
  These require zope.publisher, which is not ported to Python 3 yet, so I
  haven't added it back to install_requires in setup.py.  User beware.


4.0.0a3 (2013-02-15)
--------------------

- Added support for Python 3.3.

- Log DEBUG when loading translations from directories.

- Replaced deprecated ``zope.interface.implements`` usage with equivalent
  ``zope.interface.implementer`` decorator.

- Dropped support for Python 2.4 and 2.5.


3.8.0 (2012-03-15)
------------------

- Added optional ``domain`` attribute to ``registerTranslations`` directive to
  only load the specified translation domain. Allows to move catalogs to
  `/usr/share/locale` and avoid loading hundreds of unrelated domains.

- Include meta.zcml files in our own zcml configuration as needed, added a
  test for our configure.zcml.

- Update zope.i18n.NAME_RE to be identical to zope.tal as required by the
  comment next to it. Fixes #611746.


3.7.4 (2010-07-08)
------------------

- Added missing test dependency on ``zope.testing``.


3.7.3 (2010-04-30)
------------------

- Removed use of 'zope.testing.doctestunit' in favor of stdlib's 'doctest.

3.7.2 (2009-12-14)
------------------

- It's a critical error when the ``GetText`` library is unavailable
  and compilation is required.

- Use getSiteManager rather than getGlobalSiteManager in ZCML (these
  should be one in the same in any non-fancy setup, however if you've
  hooked getSiteManager, you want the ZCML handler to use the hooked
  version).

3.7.1 (2009-08-07)
------------------

- Fixed the interpackage translation domain merging feature to actually work.
  We need to defer the merging into the ZCML handler execution phase, as the
  utilities don't exist yet during the ZCML parsing phase. Thx to Andreas
  Zeidler for finding and fixing the issue in PlacelessTranslationService in
  the first place.

- Fix translation domains translating a message for a different domain. In the
  process, fix testMessageIDTranslateForDifferentDomain which seemed to work by
  mistake as the "other" and "default" domains used the same catalog. This is
  basically a reversion of 39991.


3.7.0 (2009-03-18)
------------------

- Updated locale data to CLDR 1.1. This introduces contextual month
  and day names and different month/day name widths. More CLDR updates
  are expected, see the "nadako-cldr" branch of zope.i18n.

- Add `configure.zcml` that registers standard negotiator utility and includes
  ``zope.i18n.locales`` configuration. This was previously done by
  ``zope.app.i18n``.


3.6.0 (2008-10-26)
------------------

- Fixed a test failure in the compile mo file support.

- Move the zcml support into an extra. This reduces the dependencies of a
  standard zope.i18n install by half a dozen packages.


3.5.0 (2008-07-10)
------------------

- Feature: Added new top-level negotiate function, which can be used to
  negotiate the language when the available languages are set globally via
  `zope_i18n_allowed_languages`.

- Feature: Added support for restricting the available languages. We support
  an environment variable called `zope_i18n_allowed_languages` now, which is
  a list of comma or space separated language codes. If the environment
  variable is set, the ZCML registration will only process those folders
  which are in the allowed languages list.

- Feature: Added optional automatic compilation of mo files from po files.
  You need to depend on the `zope.i18n [compile]` extra and set an environment
  variable called `zope_i18n_compile_mo_files` to any True value to enable
  this option.

- Feature: Re-use existing translation domains when registering new ones.
  This allows multiple packages to register translations in the same domain.
  If the same message exists in multiple catalogs the one registered first
  will take precedence.

- Feature: Recursive translations of message strings with mappings
  (https://bugs.launchpad.net/zope3/+bug/210177), thanks to Hermann
  Himmelbauer for the inital patch.

- Bug: When parsing a date, the parsing pattern did not ensure that the line
  started and ended with the matching pattern, so that '1/1/2007' parsed into
  '1/1/20' for example.

3.4.0 (2007-10-02)
------------------

- Updated meta-data. No code changes.


3.4.0b5 (2007-08-15)
--------------------

- Bug: Fixed dependency on ``zope.component`` to require it with the 'zcml'
  extra instead of requiring ``zope.security`` directly.


3.4.0b4 (2007-07-19)
--------------------

- Bug: Number parsing was too forgiving, allowing non-numerical and/or
  formatting characters before, after and within the number. The parsing is
  more strict now.


3.4.0b3 (2007-06-28)
--------------------

- Bug: There was a bug in the parser that if no decimal place is given
  you still had to type the decimal symbol. Corrected this problem (one
  character ;-) and provided a test.


3.4.0b2 (2007-06-25)
--------------------

- Feature: Added ability to change the output type when parsing a
  number.


3.4.0b1 (?)
-----------

- Bug: Fixed dependency on ``zope.security`` to require a version that
  does not have the hidden dependency on ``zope.testing``.


Note: Releases between 3.2.0 and 3.4.0b1 were not tracked as individual
packages. The changes can be reconstructed from the Zope 3 changelog.


3.2.0 (2006-01-05)
------------------

- Corresponds to the verison of the zope.i18n package shipped as part of the
  Zope 3.2.0 release.

- Added a picklable offset-based timezone to 'pytz', a la
  zope.app.datetimeutils'.  Added tests in 'zope.i18n' to show that we need
  something like it, and then actually use it in 'zope.18n.format'.

- Added support for parsing / formatting timezones using 'pytz' (new external
  dependency).

- Implemented remaining date/time formatters, including adding week
  information to the calendar.


3.0.0 (2004-11-07)
------------------

- Corresponds to the version of the zope.i18n package shipped as part of
  the Zope X3.0.0 release.
