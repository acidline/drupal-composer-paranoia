# drupal-composer-paranoia
This is an __experimental__ Composer plugin to be used in Drupal composer projects that want to improve the site security by moving __all PHP files out of docroot__.

The critical security issue with [Coder](https://www.drupal.org/project/coder) was a good example to consider moving PHP files outside of docroot: 
- [Remote Code Execution - SA-CONTRIB-2016-039](https://www.drupal.org/node/2765575)
- https://twitter.com/drupalsecurity/status/753263548458004480

More related links:
- [Moving all PHP files out of the docroot](https://www.drupal.org/node/2767907)
- [#1672986: Option to have all php files outside of web root](https://www.drupal.org/node/1672986)

## Experimental Plugin
The implementation of this Plugin is currently being discussed and validated, so it is not recommended to use it in the production environments, however any use for testing and feedback is welcome.
- Original issue: https://github.com/drupal-composer/drupal-project/issues/176

The implementation are based on:
- https://github.com/drupal-composer/drupal-project/pull/335
- https://github.com/drupal-composer/drupal-project/pull/180

## Usage
Make sure you have a based [drupal-composer/drupal-project](https://github.com/drupal-composer/drupal-project) project created.

Add the following additional parameters to the `composer.json` of your root package:
```
    "scripts": {
        "drupal-paranoia": "Jkribeiro\\DrupalComposerParanoia\\Plugin::install",
        "..."
    }
```
```
    "extra": {
        "drupal-app-dir": "app",
        "drupal-web-dir": "web",
        "..."
    }
```
Use `composer require ...` to install this Plugin in your project.
```
composer require jkribeiro/drupal-composer-paranoia:~1
```

Done! Plugin installed.

Every time you install or update a Drupal package, the paranoia installer will rebuild the `drupal-web-dir` folder with the symlinks of the asset files from the `drupal-app-dir` folder.

If you need to rebuild the docroot folder, for example, when developing locally in the app folder with new themes images, CSS and JS, you can use the command:
```
composer run-script drupal-paranoia
```
Remember: The document root configuration of your web server should point to `drupal-web-dir` path.
