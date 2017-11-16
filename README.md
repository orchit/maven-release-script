maven-release-script
====================

This script provides similar functionality to the Maven release script, but works nicely with git.

The script asks you for the version numbers if they are not provided and then:

- builds the project with the "clean verify" target to make sure that tests pass
- replaces the old dev version (most likely the snapshot version) with the release version (most likely the dev version without the -snapshot)
- commits the release version
- tags the commit with v${release version}
- either 
-- release branch does not exist
--- creates the release branch
--- pushes current master with the commit to the server
-- release branch does exist
--- pulls the latest version from the repo
--- rebases the master onto the release branch
- updates the version to the next development version (most likely the old dev version +1 minor and -snapshot)
- pushes changes and tags


As the script is supposed to be checked in along with your code it has a -u parameter that updates the script with the latest version from github.

This is forked from the repo: petergeneric/maven-release-script

Usage
=====

```
Usage:
  release.sh [-a | [ -r RELEASE_VERSION ] [ -n NEXT_DEV_VERSION ] ]  [ -c ASSUMED_POM_VERSION ] [ -s ]
Updates release version, then builds and commits it

  -a    Shorthand for -a auto -n auto
  -r    Sets the release version number to use ('auto' to use the version in pom.xml)
  -n    Sets the next development version number to use (or 'auto' to increment release version)
  -c    Assume this as pom.xml version without inspecting it with xmllint
  -s    If provided, digitally signs the release before deploying it

  -u    update the script from github
  -h    For this message
```
