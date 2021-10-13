# Drupal 9 - ACMS using DrupalVM
This repository consists of the drupal9 acms.

# Getting Started
This project is based on BLT 13.x with DrupalVM local env, an open-source project template and tool that enables building, testing, and deploying Drupal installations following Acquia Professional Services best practices. While this is one of many methodologies, it is one of our recommended methodology.

1. Review the [Required / Recommended Skills](https://docs.acquia.com/blt/developer/skills/) for working with a BLT project.
2. Ensure that your computer meets the minimum installation requirements (and then install the required applications). See the [System Requirements](https://docs.acquia.com/blt/install/).

# Prerequisites
1. Composer 2: To install composer2 follow the steps mentioned here. (https://getcomposer.org/download/)
2. Vagrant & VirtualBox: To install vagrant follow the steps from here. (https://www.vagrantup.com/downloads)
```
$ brew install virtualbox vagrant
```
3. Site Studio API Keys


# If Starting From Scratch
1. Download the latest version of Drupal + ACMS
```
$ composer create-project acquia/acquia-cms-project acms --no-interaction
```

2. Goto project directory
```
$ cd acms
```

3. Add Blt
```
composer require acquia/blt --with-all-dependencies
```

4. Add Blt site studio plugin

Add below details in composer.json under repository
```
"blt-site-studio": {
     "type": "vcs",
     "url": "https://github.com/davidtrainer/blt-site-studio.git",
     "no-api": true
 }
```
and after that execute
```
composer require acquia/blt-site-studio
```

5. Add BLT DrupalVM plugin

```
composer require acquia/blt-drupal-vm
```

6. Check PHP version and other config of the DrupalVM box.
Update box/config.yml with details like:
```
php_version: "7.4"
```
and update composer.json file as well:
```
    "php": "^7.4",
```

7. Update composer changes in lock file.

```
composer update
```

8. Add DrupalVM

```
blt recipes:drupalvm:init
```

9. Start vagrant
```
$ vagrant up
```

10. Login into vagrant machine

```
vagrant ssh
```

12. Finalize settings and setup
```
$ composer acms:install
```
or
```
drush site:install acquia_cms --yes --account-pass admin
```


## Other Local Setup Steps

1. Set up frontend build and theme.
By default BLT sets up a site with the lightning profile and a cog base theme. You can choose your own profile before setup in the blt.yml file. If you do choose to use cog, see [Cog's documentation](https://github.com/acquia-pso/cog/blob/8.x-1.x/STARTERKIT/README.md#create-cog-sub-theme) for installation.
See [BLT's Frontend docs](https://docs.acquia.com/blt/developer/frontend/) to see how to automate the theme requirements and frontend tests.
After the initial theme setup you can configure `blt/blt.yml` to install and configure your frontend dependencies with `blt setup`.

2. Pull Files locally.
Use BLT to pull all files down from your Cloud environment.
```
$ blt drupal:sync:files
```

3. Sync the Cloud Database.
If you have an existing database you can use BLT to pull down the database from your Cloud environment.
```
$ blt sync
```

# Resources

Additional [BLT documentation](https://docs.acquia.com/blt/) may be useful. You may also access a list of BLT commands by running this:
```
$ blt
```

Note the following properties of this project:
* Primary development branch: Develop
* Local site URL: http://www.local.acms.com/

## Working With a BLT Project
BLT projects are designed to instill software development best practices (including git workflows). \
Our BLT Developer documentation includes an [example workflow](https://docs.acquia.com/blt/developer/dev-workflow/).

### Important Configuration Files
BLT uses a number of configuration (`.yml` or `.json`) files to define and customize behaviors. Some examples of these are:

* `blt/blt.yml` (formerly blt/project.yml prior to BLT 9.x)
* `blt/local.blt.yml` (local only specific blt configuration)
* `drush/sites` (contains Drush aliases for this project)
* `composer.json` (includes required components, including Drupal Modules, for this project)
