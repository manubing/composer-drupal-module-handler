Automatically uninstall a Drupal module before removing it with Composer
====


# About

This composer-plugin contains a plugin witch tries to properly uninstall a Drupal module before Composer attempts to remove it.

> This plugin is intended to be used with a composer-managed Drupal project, eg: [drupal-composer/drupal-project](https://github.com/drupal-composer/drupal-project)

# How it works

This plugin listens the `prePackageUninstall` Composer event. In case of a package of type `drupal-module` being removed, it tries to:

- Bootstrap Drupal
- Invoke the Module Installer service to uninstall the module

If this plugin can't proceed, Composer will still remove the package.

# Installation

```bash
composer require manubing/composer-drupal-module-handler
```

No configuration required 🎊

# Configuration

If no configuration is provided, this package will use default values matching [drupal-composer/drupal-project](https://github.com/drupal-composer/drupal-project):

- Default value of Drupal `app_root` is `{COMPOSER_DIR}/../web`
- Default value of Drupal `site_path` is `{app_root}/sites/default`

However, if your project have a different directory structure, use the `composer.json` `extra` section:

```json
{
  "extra": {
    "drupal-project": {
      "app-root": "html",
      "site-path": "sites/some-site"
    }
  }
}
```

# Note

This plugin does not currently support multi-sites projects.