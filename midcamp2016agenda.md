# d8trainingtheme
An example custom theme for Pantheon/Drupal 8 training


## 9am - 9:30am Introduction

* Everyone introduce yourself
  * What do you do with Drupal?	
  * What is your experience with Pantheon?
  * What do you want to learn today?
* Agenda overview

## 9:30am - 10:30am Pantheon overview

## 10:30 - 10:45am Break

## 10:45 - Noon Hands-on time

## 1pm - 2pm Multidev / Group work

## 2pm - 3pm Terminus, the Pantheon Command line tool

During this section we will review the basics of [Terminus][], the Pantheon command line tool.

### Sample commands


#### Log in to terminus with a Password.
```
terminus auth login

```
You also have the option of [authenticating with a machine token][terminus token].

#### See all workflows on a site

```
terminus workflows watch --site=MACHINENAMEOFSITE
```

#### Use drush to get a login link to a dev environment

```
terminus --site=MACHINENAMEOFSITE --env=dev  drush 'user-login'
``` 

## 3pm - 3:15pm Break

## 3:15pm - 4:15pm Quicksilver Platform Hooks

In this hour we will cover Pantheon's [Quicksilver Platform Hooks].

## 4:15pm - 5pm Questions and Independent work


[Quicksilver Platform Hooks]: https://pantheon.io/docs/articles/sites/quicksilver/ 'Respond to plaform-level events with Quicksilver'
[Terminus]: http://github.com/pantheon-systems/terminus "The Pantheon command line tool"
[terminus token]: https://pantheon.io/docs/articles/local/cli/machine-tokens/ "Create a terminus token with your account"
