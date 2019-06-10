# phpinsights-action

This GitHub Action executes [phpinsights](https://github.com/nunomaduro/phpinsights). The output of the Insights Command can be viewed in the Actions log.

You can optionally define minimum values for Insights categories. If the value falls below your given threshold, the run fails.

If you're using Laravel, there's also [a framework specific Action](https://github.com/stefanzweifel/laravel-phpinsights-action) available.

### Usage

This Action doesn't install composer dependencies on it's own and doesn't contain a `phpinsights` binary.

It's therefore required that `phpinsights` is set as a dependency in your project and that another Action installs the composer dependencies.

An example Workflow can look like this.

```terraform
workflow "phpinsights" {
  on = "push"
  resolves = [
    "phpinsights"
  ]
}

action "composer install" {
  uses = "MilesChou/composer-action@master"
  args = "install -q --no-ansi --no-interaction --no-scripts --no-suggest --no-progress --prefer-dist"
}

action "phpinsights" {
  needs = ["composer install"]
  uses = "stefanzweifel/phpinsights-action@v1.0.0"
}
```


### Arguments

You can pass any valid `phpinsights` argument to the Action. In this example, all issues are always displayed and a minimum value of 80 has to be achieved in all categories.

```terraform
action "phpinsights" {
  needs = ["composer install"]
  uses = "stefanzweifel/phpinsights-action@v1.0.0"
  args = "-v --min-quality=80 --min-complexity=80 --min-architecture=80 --min-style=80"
}
```

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/stefanzweifel/phpinsights-action/tags).

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/stefanzweifel/phpinsights-action/blob/master/LICENSE) file for details.
