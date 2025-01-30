# Twig example

## Reproduce the issue

To reproduce the issue, please run command:

```bash
composer run compile-templates
```

## Fixing the issue

To fix the issue using [the fix suggested by user stof](https://github.com/twigphp/Twig/issues/4393#issuecomment-2598813767), in `src/GetText.php`, replace

```php
$twig->registerUndefinedFunctionCallback(function ($name) {
    return new \Twig\TwigFunction($name, $name);
});
$twig->registerUndefinedFilterCallback(function ($name) {
    return new \Twig\TwigFilter($name, $name);
});
```

with

```php
$twig->registerUndefinedFunctionCallback(function ($name) {
    return new \Twig\TwigFunction($name, function () {});
});
$twig->registerUndefinedFilterCallback(function ($name) {
    return new \Twig\TwigFilter($name, function () {});
});
```