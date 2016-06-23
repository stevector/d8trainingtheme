# Example theme for Pantheon training

This theme is an example subtheme of Drupal 8's Bartik. This theme is meant for demonstration and training purposes. It is not meant to be used as a starting point for any real site.

# Twin Cities Drupal Camp 2016 Training agenda

The purpose of [this training at Twin Cities Drupal Camp](http://2016.tcdrupal.org/trainings/pantheon) is to introduce developers to the ways in which Pantheon's tools interact with Drupal development best practices. By the end of the day attendees should feel comfortable with basic Drupal site development tasks like adding modules and editing custom theme files. Additionally, attendees will know where to start with Pantheon's development power tools like [Multidev], [Quicksilver Platform Hooks] and [Terminus], our command line tool.


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

* **Create a `.env` file containing the following line in the root of your git clone of the site.**

```
TERMINUS_SITE=the-machine-name-of-your-site
```
This file will allow you to avoid adding `--site=the-machine-name-of-your-site` on all of the following commands.

* **Create a sample node on your live environment**
  * To create this node on the live environment you need to be logged in and go to the node add form. This Terminus command uses drush to generate a login link that will also redirect to a node add form.
    * `terminus --env=live  drush 'user-login admin  node/add/article' `
  * Create and example article node.
* **Copy the database and files from the live site to the dev site**
  * `terminus site clone-content --from-env=live --to-env=dev`
* **Set the dev environment to SFTP mode so that the filesystem is writeable.**
  *  `terminus  --env=dev site set-connection-mode  --mode=sftp`
* **Make a configuration change on the Dev environment**
  * Move a Drupal Block into a sidebar.
  * Export the configuration change.
    * `terminus  --env=dev drush "config-export -y"`
    * See the files that have changed.
    * `terminus --env=dev site code diffstat`
  * Commit your change.
    * `terminus --env=dev site code commit --message="A config change committed via terminus"`
  * See your commit in the log.
    * `terminus site code log  --env=dev`
* **Deploy your change to the test environment**
  * Note that the test environment still does not have the node added above. We copied the database from live to dev, but not from live to test. That's ok. We can copy the database and files to test while also bringing code changes up from the dev environment.
  * `terminus site deploy --env=test --sync-content --cc --updatedb --note="Deploying config change via terminus"`
  * Import the configuration change on the Test environment.
    * `terminus  --env=test drush "config-import -y"`
* **Deploy to the live environment**
  * `terminus site deploy --env=live --cc --updatedb --note="Deploying config change via terminus"`
  * Import the configuration change on the Live environment.
    * `terminus  --env=live drush "config-import -y"`


### Prompts for independent work

* Use `terminus workflows watch` to see logging of operations like deployments and cache clearing.
* Do the same workflow as above, but make your CSS changes in a Multidev environment. Create the Multidev environment and merge it back to dev using Terminus.
* Create a database backup on the live environment. Then download that backup.
* Add another training attendee to your site as a developer with Terminus.
* Use Terminus to find the MySQL connection information to your test environment.

## 3pm - 3:15pm: Break

## 3:15pm - 4:00pm: Quicksilver Platform Hooks

In this hour we will cover Pantheon's [Quicksilver Platform Hooks]. Quicksilver is system that allows developers to specify scripts to be run in response to platform-level operations like cache clearing, code deployments and database cloning. We will start with a demo followed by everyone working together to install the [config import example](https://github.com/pantheon-systems/quicksilver-examples/tree/master/drush_config_import) from the [Quicksilver Examples repository].


### Prompts for independent work

Pick out examples from the repository and implement them: https://github.com/pantheon-systems/quicksilver-examples. A simple one to start with is [generate_dev_content].


## Additional resources

* [The Power Users Google Group].
* [Training videos].
* [Our documentation site]. [Pull requests on our documentation are welcome]!
* [Weekly demo webinars].


[devel]: https://www.drupal.org/project/devel
[d8trainingtheme]: https://github.com/stevector/d8trainingtheme
[Multidev]: https://pantheon.io/docs/articles/sites/multidev/ 'Environments per branch'
[Quicksilver Platform Hooks]: https://pantheon.io/docs/articles/sites/quicksilver/ 'Respond to platform-level events with Quicksilver'
[Terminus]: http://github.com/pantheon-systems/terminus "The Pantheon command line tool"
[drush]: http://www.drush.org/en/master/ "Drupal's command line tool"
[terminus token]: https://pantheon.io/docs/articles/local/cli/machine-tokens/ "Create a terminus token with your account"
[debugging example]: https://github.com/pantheon-systems/quicksilver-examples/tree/master/debugging_example "Print debugging output to terminus workflows watch"
[Quicksilver Examples repository]: https://github.com/pantheon-systems/quicksilver-examples/tree/master/debugging_example "A GitHub repository of example Quicksilver script."
[generate_dev_content]: https://github.com/pantheon-systems/quicksilver-examples/tree/master/generate_dev_content
[The Power Users Google Group]: https://pantheon.io/docs/articles/power-users/
[Training videos]: https://pantheon.io/essential-training
[Our documentation site]: https://pantheon.io/docs/
[Pull requests on our documentation are welcome]: https://github.com/pantheon-systems/documentation
[Weekly demo webinars]: https://pantheon.io/pantheon-product-demo
