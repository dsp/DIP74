Abstract
--------
The current release process of DMD, Druntime and Phobos (from now on referred to
as "release package"), is done on a "done when it's done" basis. This DIP
proposes a time-based release schedule. This allows:

 (1) get bugfixes out faster
 (2) packagers have a more predictable release schedule
 (3) developer know when their feature get's released and don't have to wait
 (4) in line with releases of major distributions

In addition the DIP proposes the idea of a "Release Manager", which
is responsible for a timely release.

Versions
--------
We propose to introduce "bugfix versions" and "feature versions". A release
version can contain new features, language changes, and deprecation. For every
release version the Minor part of the version is incremented: 2.066, 2.067, ...
A bugfix version is based on a feature version and contains only bugfixes
and no new features, nor deprecations of other features or library
changes. Bugfix versions are for example: 2.066.1, 2.066.2, etc. There is only
one supported version at a time, but release managers are free to release
additional bugfix versions when needed.

Schedule
--------
A bugfix version is released every month. A feature version is released every 3
month. For example:

 Jan 1st: 2.069
 Feb 1st: 2.069.1
 Mar 1st: 2.069.2
 Apr 1st: 2.070

Support
------
Only the most recent version is supported. Distributions are free to backport
what is needed. In addition Release Managers can decided to release additional
fix versions if needed.

Branching strategy
------------------
There are two branches: master and ${version}. On a feature release date the
master branch becomes for example 2.069. All subsequent "bugfix" versions are
tagged off the 2.069 branch. New features go to master, which will become the
next major version.

Release manager
---------------
