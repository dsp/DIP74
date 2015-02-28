DIP74 Release Process
=====================

Abstract
--------
The current release process of DMD, Druntime and Phobos (from now on referred to
as "release package"), is done on a "done when it's done" basis. This DIP
proposes a time-based release schedule. This allows:

 * reduce times to get bugfixes out
 * a clear way of managing backwards compatibility
 * packagers have a more predictable release schedule
 * cleaner responsibilities
 * developer know when their feature get's released and don't have to wait
 * synchronize with releases processes of major distributions

In addition the DIP proposes the idea of a "Release Manager", which
is responsible for a timely release.

Versions
--------
We propose to introduce **bugfix versions** and **feature versions**. A
**feature version** can contain new features, language changes, and
deprecations. For every release version the minor part of the version
is incremented: 2.066, 2.067, ...  A **bugfix version** is based
on a feature version and contains only bugfixes and no new features,
nor deprecations of other features or library changes. Bugfix
versions are for example: 2.066.1, 2.066.2, etc. There is only one
supported version at a time, but release managers are free to release
additional bugfix versions when needed.

Schedule
--------
A bugfix version is released every month. A feature version is released every 3
month. Two weeks before a feature release a *feature freeze* is put
in place and no new features are added to the master branch. A week before the
release a *code freeze* is put in place. Only urgent bugfixes are allowed in
this week.

Example schedule:

  - Dec 14th: Feature freeze 2.069
  - Dec 21th: Code freeze 2.069
  - Jan 1st: 2.069
  - Feb 1st: 2.069.1
  - Mar 1st: 2.069.2
  - Mar 14th: Feature freeze 2.070
  - Mar 21th: Code freeze 2.070
  - Apr 1st: 2.070

Support and Packages
------
Only the most recent version is supported. Distributions are free to backport
what is needed. In addition Release Managers can decided to release additional
fix versions if needed. The release manager offer the source tarball as well
as a Windows version. All other formats are left to packagers and should be
preferable automized.

Branching strategy
------------------
There are two branches: master and ${version}. On a feature release date the
master branch becomes for example 2.069. All subsequent "bugfix" versions are
tagged off the 2.069 branch. New features go to master, which will become the
next major version.

Branching Figure:

    ----- master ------------------------------------
     \                                         \
      2.069 -------------------                 2.070 ----
       \           \            \
        TAG 2.069  TAG 2.069.1   TAG 2.069.2


Release manager
---------------
Release managers are responsible for releasing the *release package* on time.
They ensure that bugfix releases do not contain any backwards compatibilities and
maintain the changelog. Release managers are free to remove features or fixes
when necessary. Release managers are able to merge features and bugfixes on
github. They are to provide a GPG signed tarball and a feature. Release managers
are appointed by Walter and Andrei.

Security Management
-----------------
Release managers should keep track of security releated bugs. They
are responsible for following a *responsible disclosure policy* for
D. This means, set an exepcted fix date, communicate the date with
the original vulnerability reporter. Contact packages to get ready
to publish packages at the given date and obtain an CVE if necessary.
Upon release date they notify the packagers and write an announcement
explaining the vulnerability and include the reporter if desired. That
way we ensure a smooth handling of security problems in line with
standard community processes.
