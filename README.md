# Linaro theme for Keycloak SSO

## Introduction
Linaro uses Keycloak to provide single sign-on (SSO) functionality. Keycloak provides the ability to provide your own themes to be used instead of those included with the package.

The purpose of this theme is to customise the look of the `login` view - the part of Keycloak that users will interact with the most.

For reference, the others are `account`, `admin`, `email` and `welcome`.

## Installation
Within the Keycloak installation directory, go into `themes` and clone this repository. On the current server, the directory is actually called `linaro.v2` partly because Keycloak has a `keycloak.v2` theme that provides an updated look to the `account` view, and this theme provides an updated look to the `login` view.

## Directory structure
Within the `login` directory, there are two folders (`messages` and `resources`) and two files (`template.ftl` and `theme.properties`).

## Updating Keycloak
When Keycloak is updated, a new version may include new features and these need to be included for the new features to work properly.

The aim is to keep this theme as lightweight/minimal as possible in terms of changes/differences from either the `base` or `keycloak` originals.

### messages > messages_en.properties
The official source for this file is `base/login/messages/messages_en.properties`. The following changes have been made:

* Change `doLogIn` to read "Log in" instead of "Sign In"
* Change `loginAccountTitle` to read "Log in to Linaro SSO" instead of "Sign in to your account"
* Change `loginTitle` to read "Log in to Linaro SSO" instead of "Sign in to {0}"
* Change `usernameOrEmail" to read "Email" instead of "Username or email"

### resources > css > login.css
The official source for this file is `keycloak/login/resources/css/login.css`.

Numerous changes have been made. Where the changes are to the original source, comments have been added to explain what has been changed. Also, all comments are marked "LINARO" to make it really clear.

There is a large section near the end of the file of Linaro additions. Work needs to be done to check how much of this is still being used.

### template.ftl
The official source for this file is `base/login/template.ftl`.

This file is what drives the actual look of the login interface. The principal changes are:

* Add a link to Linaro's stylesheet
* Add the Linaro logo and link to the Linaro website
* Comment out the default Keycloak header
* Add the Linaro footer section

(A diff suggests that an extra `</div>` has been removed as well. Unfortunately the spacing/layout of the file makes it hard to keep this clean. Fixing the spacing/layout would result in more changes to the file and thus make it hard to check changes with `diff`)

### theme.properties
The official source for this file is `keycloak/login/theme.properties`.

This file allows some CSS settings to be altered without affecting the FTL file itself. To that end, there are not many changes from the original source:

* Remove `css/tile.css` from `styles`
* Comment out kcLogoLink as not used with the altered template
* Add kcContentWraperClass. It is used in the template but not defined anywhere else?
* Add forgottenPasswordUrl although it isn't currently being used!
