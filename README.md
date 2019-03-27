# Docksal powered Drupal 8 Core Contribution Installation

This is a Drupal 8 installation geared for local Core and Contrib development
for use with Docksal.

[![Build status](https://travis-ci.org/jhedstrom/drupal8-contrib.svg?branch=master)](https://travis-ci.org/jhedstrom/drupal8-contrib?branch=master)

Features:

- Core Drupal 8 repository for local contribution development
- `fin init` [example](.docksal/commands/init)
- Using the [default](.docksal/docksal.env#L9) Docksal LAMP stack with [image version pinning](.docksal/docksal.env#L13-L15)
- PHP and MySQL settings overrides [examples](.docksal/etc)
- Drush aliases [example](drush/aliases.drushrc.php) (`drush @docksal status`)

## Setup instructions

### Step #1: Docksal environment setup

**This is a one time setup - skip this if you already have a working Docksal environment.**  

Follow [Docksal environment setup instructions](https://docs.docksal.io/en/master/getting-started/env-setup)

### Step #2: Project setup

1. Clone this repo into your Projects directory

    ```
    git clone https://github.com/docksal/drupal8-contrib.git drupal8
    cd drupal8
    ```

2. Initialize the site

    This will clone the core repository into `docroot`, initialize local
    settings and install the site via drush

    ```
    fin init
    ```

3. Point your browser to

    ```
    http://drupal8.docksal
    ```

When the automated install is complete the command line output will display the admin username and password.

### Step #3: Contributing to core!

1. Find and issue, and create a local branch in the `docroot` folder:

   ```
   cd docroot
   git checkout -b 12345-short-description
   ```

   where `12345` is the issue number, and `short-description` is just something to remind you of the issue.

2. Apply the patch from the issue if it exists.

3. Run any relevant phpunit tests locally:

    ```
    fin phpunit path/to/file/or/directory
    ```

    for instance:

    ```
    fin phpunit core/tests/Drupal/Tests/Component/Utility/UnicodeTest.php
    ```

    **Note**: it is not advisable to simply run `fin phpunit` as this will run _all_ the core tests, which can take hours locally.

## Security notice

This repo is intended for local core contributions and includes a hardcoded value for `hash_salt` in `settings.php`.
**You should not base your project off of this code base**. If you do for whatever reason, make sure you regenerate and
update the `hash_salt` value. A new value can be generated with `drush ev '$hash = Drupal\Component\Utility\Crypt::randomBytesBase64(55); print $hash . "\n";'`
