# Example theme for Pantheon training

This theme is an example subtheme of Drupal 8's Bartik. This theme is meant for demonstration and training purposes. It is not meant to be used as a starting point for any real site.

# BADCamp 2016 Training agenda

The purpose of [this training at BADCamp 2016](https://2016.badcamp.net/training/drupal-development-best-practices-building-sites-pantheon) is to introduce developers to the ways in which Pantheon's tools interact with Drupal development best practices. By the end of the day attendees should feel comfortable with basic Drupal site development tasks like adding and editing modules or themes, installing Drupal 8, using configuration management, and setting up composer. Additionally, attendees will know where to start with Pantheon's development power tools, such as [Multidev].


## 8am - 8:30am: Introductions

* Everyone introduce yourself.
  * What do you do with Drupal?	
  * What is your experience with Pantheon?
  * What do you want to learn today?
* Agenda overview.

## 8:30am - 9:30am: Pantheon overview

Pantheon staff will explain Pantheon's key features and demonstrate basic usage of the dashboard and other tools.

## 9:30am - 9:45am: Break

During this time Pantheon staff can help anyone who has had difficulty registering for a Pantheon account.

## 9:45am - 11am: Installing Drupal 8 and using the dashboard

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

## 11am - Noon: Multidev / group work

This time will start with a demonstration of Pantheon's [Multidev] feature which allows for additional development environments to be created per git branch. After the demonstration, attendees will be split into groups. Group members will make Multidev branches on each other's test sites and merge them to the master branch.

### Prompts for group work

* Have one team member make a CSS change in a Multidev environment. Have another team member merge and review it.
* Have two team members (A and B) make changes to different files in different Multidev environments.
  * Merge A's branch into master.
  * Merge master in B's branch.
  * Merge B's branch into master.

## Noon - 1pm: Lunch!

## 1pm - 2pm: Configuration management with Drupal 8

Once our Drupal 8 websites are installed and you're comfortable with the Pantheon dashboard, we'll walk you through using configuration management within the Dev, Test, Live workflow.

## 2pm - 3pm: Working with Composer and Drupal 8

This time will walk through using Composer on your Drupal 8 website. We'll cover a few gotchas to getting it set up and working smoothly with your Pantheon workflow and answer questions.

## 3pm - 5pm: Wrap up, questions, and independant work

You've gotten a lot accomplished today! We'll spend the rest of the day answering questions and assisting anyone who fell behind throughout the day.

## Additional resources

* [The Power Users Google Group].
* [The Power Users Slack].
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
[The Power Users Slack]: https://slackin.pantheon.io/
[Training videos]: https://pantheon.io/essential-training
[Our documentation site]: https://pantheon.io/docs/
[Pull requests on our documentation are welcome]: https://github.com/pantheon-systems/documentation
[Weekly demo webinars]: https://pantheon.io/pantheon-product-demo
