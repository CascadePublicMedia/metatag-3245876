# Purpose

Confirms an infinite loop OOM issue caused by the combination of Metatags
v1.18+ and Search API when using memcache for caching on the search view.

## Related issues

- [Out of memory error with metatag_view submodule and Search API view](https://www.drupal.org/project/metatag/issues/3245876)
- [Out of memory error when used with views, metatag and memcache modules](https://www.drupal.org/project/search_api/issues/3258375)

## Install

### Prerequisites

- Git
- [Lando](https://docs.lando.dev/basics/installation.html)

### Setup

1. `git clone https://github.com/CascadePublicMedia/metatag-3245876.git`
2. `cd metatag-3245876`
3. `composer install`
4. `lando start`
5. `lando db-import metatag-3245876.sql.gz`

## Reproduction

1. Navigate to [http://metatag-3245876.lndo.site/](http://metatag-3245876.lndo.site/).
2. Search for a term with results: "dolore" (should work).
3. Run `lando drush cr`.
4. Search for the same term again: "dolore" (OOM exception).

After following these steps the search term will causes OOM executions until
memcache is flushed manually with:

`lando drush ev "Drupal::service('memcache.factory')->get('default')->flush();"`

## Notes

Admin login and password is `drupal9`.
