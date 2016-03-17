# Example theme for Pantheon training

This theme is an example subtheme of Drupal 8's Bartik. This theme is meant for demonstration and training purposes. It is not meant to be used as a starting point for any real site.

# MidCamp 2016 Training agenda

The purpose of [this training at MidCamp 2016] is to introduce developers to the ways in which Pantheon's tools interact with Drupal development best practices. By the end of the day attendees should feel comfortable with basic Drupal site development tasks like adding modules and editing custom theme files. Additionally, attendees will know where to start with Pantheon's development power tools like [Multidev], [Quicksilver Platform Hooks] and [Terminus], our command line tool.


## 9am - 9:30am: Introduction

* Everyone introduce yourself.
  * What do you do with Drupal?	
  * What is your experience with Pantheon?
  * What do you want to learn today?
* Agenda overview.

## 9:30am - 10:30am: Pantheon overview

Pantheon staff will explain Pantheon's key features and demonstrate basic usage of the dashboard and other tools.

## 10:30am - 10:45am: Break

During this time Pantheon staff can help anyone who has had difficulty registering for a Pantheon account.

## 10:45am - Noon: Installing Drupal 8 and using the dashboard

This section will start with everyone walking through the same steps together:

* Add and enable [devel] module while using SFTP mode.
* Add and enable [d8trainingtheme].
* Create the test environment.
* Create the live environment.

Once everyone has gotten this far, each attendee is encouraged to work independently to explore areas of the Pantheon workflow. If you are uncertain of what to do next, try any of the following:

* Add more modules.
* Add twig files to the example theme that override Bartik.
* Edit CSS in the example theme.
* Add content on the live site. Then clone the database and files from the live environment down to the dev environment.
* Switch to git mode on the dev environment. Clone the site to your machine. Make CSS changes and push them back up.
* Create a backup on the live environment. Download the archives.
* Turn on HTTP authentication in one of the environments.

## Noon - 1pm: Lunch!


## 1pm - 2pm: Multidev / group work

This time will start with a demonstration of Pantheon's [Multidev] feature which allows for additional development environments to be created per git branch. After the demonstration, attendees will be split into groups. Group members will make Multidev branches on each other's test sites and merge them to the master branch.

### Prompts for group work

* Have one team member make a CSS change in a Multidev environment. Have another team member merge and review it.
* Have two team members (A and B) make changes to different files in different Multidev environments.
  * Merge A's branch into master.
  * Merge master in B's branch.
  * Merge B's branch into master.

## 2pm - 3pm: Terminus, the Pantheon Command line tool

During this section we will review the basics of [Terminus][], the Pantheon command line tool.  You can authenticate in Terminus with your password using `terminus auth login`. You can also authenticate with a [Terminus machine token][terminus token].

### Step-by-step introduction

Everyone will walk through the following commands together.

* **Create a sample node on your live environment**
  * To create this node on the live environment you need to be logged in and go to the node add form. This Terminus command uses drush to generate a login link that will also redirect to a node add form.
    * `terminus --site=SITEMACHINENAME --env=live  drush 'user-login admin  node/add/article' ` replace `SITEMACHINENAME` with the machine name of your site. For example `perschd8training`.
  * Create and example article node.
* **Copy the database and files from the live site to the dev site**
  * `terminus site clone-content --site=SITEMACHINENAME --from-env=live --to-env=dev`
* **Set the dev environment to SFTP mode.**
  *  `terminus site set-connection-mode  --mode=sftp  --env=dev --site=SITEMACHINENAME`
* **Edit the CSS file in `d8trainingtheme`**
  * If you don't still have your SFTP client open, you can grab the SFTP connection info:
    * `terminus site connection-info --env=dev --site=SITEMACHINENAME`
  * If you want to stay entirely on the command line you can grab just the command line SFTP connection string.
    * `terminus site connection-info --env=dev --site=SITEMACHINENAME --field=sftp_command`
  * Edit a CSS background color.
  * Commit your change.
    * `terminus site code commit  --site=SITEMACHINENAME --env=dev  --message="A CSS change committed via terminus"`
  * See your commit in the log.
    * `terminus site code log  --site=SITEMACHINENAME --env=dev`
* **Deploy your change to the test environment**
  * Note that the test environment still does not have the database change. We copied the database from live to dev, but not from live to test. That's ok. We can copy the database and files to test while also bringing code changes up from the dev environment.
  * `terminus site deploy --env=test --sync-content --cc --updatedb --note="Deploying CSS change via terminus" --site=SITEMACHINENAME`
* **Deploy to the live environment**
  * `terminus site deploy --env=live --cc --updatedb --note="Deploying CSS change via terminus" --site=SITEMACHINENAME`


### Prompts for independent work

* Use `terminus workflows watch` to see logging of operations like deployments and cache clearing.
* Do the same workflow as above, but make your CSS changes in a Multidev environment. Create the Multidev environment and merge it back to dev using Terminus.
* Create a database backup on the live environment. Then download that backup.
* Add another training attendee to your site as a developer with Terminus.
* Use Terminus to find the MySQL connection information to your test environment.

## 3pm - 3:15pm: Break

## 3:15pm - 4:15pm: Quicksilver Platform Hooks

In this hour we will cover Pantheon's [Quicksilver Platform Hooks]. Quicksilver is system that allows developers to specify scripts to be run in response to platform-level operations like cache clearing, code deployments and database cloning. We will start with a demo followed by everyone working together to install the [debugging example] from the [Quicksilver Examples repository].

### Setting up the debugging example

The [debugging example] can be set up using SFTP mode or git mode. If you use SFTP mode, the changes will have to be committed before `pantheon.yml` starts working.

### Step-by-step introduction

* First create an empty file, `pantheon.yml`, in your Drupal root, it should be in the same folder as Drupal's `index.php`.
  * The copy the follow text into that file
```yaml
api_version: 1

workflows:
  clear_cache:
    after:
      - type: webphp
        description: Dump debugging output
        script: private/scripts/debug.php
```

* Copy [debug.php](https://raw.githubusercontent.com/pantheon-systems/quicksilver-examples/master/debugging_example/debug.php) to `private/scripts/debug.php`. You will have to create these folders, starting with `private`, which will also go next to `index.php`.
* Push your changes up to Pantheon, or if you're using SFTP mode, commit your changes.
  * Once the changes are committed, use `terminus workflows watch` to see reporting on workflow.
  * Clear caches and see the debugging information come through the terminal.

### Prompts for independent work

Pick out examples from the repository and implement them: https://github.com/pantheon-systems/quicksilver-examples. A simple one to start with is [enable_dev_modules] which was covered in the demo.


## 4:15pm - 5pm: Wrap up, questions, and independent work

During this time we will highlight additional resources like:

* [The Power Users Google Group].
* [Training videos].
* [Our documentation site]. [Pull requests on our documentation are welcome]!
* [Weekly demo webinars].


[this training at MidCamp 2016]: http://2016.midcamp.org/training/drupal-development-best-practices-building-sites-pantheon
[devel]: https://www.drupal.org/project/devel
[d8trainingtheme]: https://github.com/stevector/d8trainingtheme
[Multidev]: https://pantheon.io/docs/articles/sites/multidev/ 'Environments per branch'
[Quicksilver Platform Hooks]: https://pantheon.io/docs/articles/sites/quicksilver/ 'Respond to platform-level events with Quicksilver'
[Terminus]: http://github.com/pantheon-systems/terminus "The Pantheon command line tool"
[drush]: http://www.drush.org/en/master/ "Drupal's command line tool"
[terminus token]: https://pantheon.io/docs/articles/local/cli/machine-tokens/ "Create a terminus token with your account"
[debugging example]: https://github.com/pantheon-systems/quicksilver-examples/tree/master/debugging_example "Print debugging output to terminus workflows watch"
[Quicksilver Examples repository]: https://github.com/pantheon-systems/quicksilver-examples/tree/master/debugging_example "A GitHub repository of example Quicksilver script."
[enable_dev_modules]: https://github.com/pantheon-systems/quicksilver-examples/tree/master/enable_dev_modules  "Enable devel module when cloning a database from live to dev"
[The Power Users Google Group]: https://pantheon.io/docs/articles/power-users/
[Training videos]: https://pantheon.io/essential-training
[Our documentation site]: https://pantheon.io/docs/
[Pull requests on our documentation are welcome]: https://github.com/pantheon-systems/documentation
[Weekly demo webinars]: https://pantheon.io/pantheon-product-demo