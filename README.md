# Purpose

Confirms an infinite loop OOM issue caused by the combination of Metatags
v1.18 and Search API when using caching on the search view.

See [Out of memory error with metatag_view submodule and Search API view](https://www.drupal.org/project/metatag/issues/3245876).

## Install

### Prerequisites

- Git
- [Lando](https://docs.lando.dev/basics/installation.html)

### Steps

1. `git clone https://github.com/CascadePublicMedia/metatag-3245876.git`
2. `cd metatag-3245876`
3. `composer install`
4. `lando start`
5. `lando db-import metatag-3245876.sql.gz`
6. `lando drush content-sync:import --yes`
7. `lando drush cr`

## Test

1. Navigate to [http://metatag-3245876.lndo.site/](http://metatag-3245876.lndo.site/).
2. Search for a term, e.g. "dolore" (works).
3. Search for the same term again (OOM exception).

## Notes

Admin login and password is `drupal9`.
