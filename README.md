railsbuild
==========

Scripts to ease the update of Ruby on Rails core packages for Fedora Project.

## Usage

```
./railsbuild FEDORA_VERSION OLD_RAILS_VERSION NEW_RAILS_VERSION
```

To update Rails from 4.1.4 to 4.1.5 for rawhide:

```
./railsbuild 22 4.1.4 4.1.5
```

To change the value for Fedora Rawhide, edit `railsbuild-common` file.

## Requirements

railsbuild needs rpmdev-packager script, fedpkg, koji and git installed.

## Components

Each script can be used on its own so you don't have to do the automatic
build, but just let railsbuild to prepare the update.

### railsbuild-prepare

```
./railsbuild-prepare FEDORA_VERSION
```
Prepares directories for the railsbuild scripts including fetching Fedora
and upstream repositories at ~/.railsbuild/upstream/rails and
~/.railsbuild/f$FEDORA_VERSION/rubygem-$gem.

### railsbuild-fetch-tests

```
railsbuild-fetch-tests FEDORA_VERSION RAILS_VERSION
```
Gets the upstream tests from the repository at ~/.railsbuild/upstream/rails
and move the gzipped test suites to Fedora git repositories at
~/.railsbuild/f$FEDORA_VERSION/rubygem-$gem.

### railsbuild-update-pkgs

```
./railsbuild-update-pkgs FEDORA_VERSION OLD_RAILS_VERSION NEW_RAILS_VERSION
```
Prepares the update of all Rails gems at once in Fedora git repositories at:
~/.railsbuild/f$FEDORA_VERSION/rubygem-$gem.

### railsbuild-update-bootstrapped

```
./railsbuild-update-bootstrapped FEDORA_VERSION OLD_RAILS_VERSION NEW_RAILS_VERSION
```
Prepare the update of previously bootstrapped Rails gems at once in Fedora git
repositories at: ~/.railsbuild/f$FEDORA_VERSION/rubygem-$gem.

### railsbuild-build

```
./railsbuild-build FEDORA_VERSION RAILS_VERSION
```
Does the builds of gems. It always tries to do a scratch-build first and
if that goes fine, does a final build. Afterwards it waits for the build
to become available and continues with the next gem.

Once all the gems are built, it disable the bootstrapping of previously
bootstrapped gems and builds them as well.
