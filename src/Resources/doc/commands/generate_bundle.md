Generating a New Bundle Skeleton
================================

## Usage

The `make:bundle` generates a new bundle structure and automatically
activates it in the application.

By default the command is run in the interactive mode and asks questions to
determine the bundle name, location, configuration format and default
structure:

```bash
$ php bin/console make:bundle
```

To deactivate the interactive mode, use the `--no-interaction` option but don't
forget to pass all needed options:

```bash
$ php bin/console make:bundle --namespace=Acme/Bundle/BlogBundle --no-interaction
```

**Caution!**

If the `make:bundle` command returns an error about registering the
bundle namespace in `composer.json`, add the following line to your
`composer.json` file within the `psr-4` section:

`"Acme\\Bundle\\BlogBundle\\": "src/Acme/Bundle/BlogBundle"`

for example:
```json
    "autoload": {
        "psr-4": {
            "Acme\\Bundle\\BlogBundle\\": "src/Acme/Bundle/BlogBundle"
        },
        "classmap": [ "app/AppKernel.php", "app/AppCache.php" ]
    },
```
, then execute the following command to regenerate the autoload files:

```bash
$ composer dump-autoload
```

## Available Options

`--shared`

Provide this option if you are creating a bundle that will be shared across
several of your applications or if you are developing a third-party bundle.
Don't set this option if you are developing a bundle that will be used
solely in your application (e.g. `AppBundle`).

----
`--namespace`

The namespace of the bundle to create. The namespace should begin with
a "vendor" name like your company name, your project name, or your client
name, followed by one or more optional category sub-namespaces, and it
should end with the bundle name itself (which must have Bundle as a suffix):

```bash
$ php bin/console make:bundle --namespace=Acme/Bundle/BlogBundle
```

----
`--bundle-name`

The optional bundle name. It must be a string ending with the `Bundle`
suffix:

```bash
$ php bin/console make:bundle --bundle-name=AcmeBlogBundle
```

----
`--dir`

The directory in which to store the bundle. By convention, the command
detects and uses the application's `src/` folder:

```bash
$ php bin/console make:bundle --dir=/var/www/myproject/src
```

----
`--format`

**allowed values**: `annotation|php|yml|xml`, **default**: `annotation`

Determine the format to use for the generated configuration files (like
routing). By default, the command uses the `annotation` format (choosing
the `annotation` format expects the [`SensioFrameworkExtraBundle`](http://symfony.com/doc/master/bundles/SensioFrameworkExtraBundle/index.html)
to be installed):

```bash
$ php bin/console make:bundle --format=annotation
```
