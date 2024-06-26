# Run PHP Tests Action

This GitHub Action sets up a PHP environment (optionally with WordPress via [mantle-ci](https://github.com/alleyinteractive/mantle-ci)) and runs install, audit, test, and build commands using Composer for your PHP projects.

## Usage

Example usage in a workflow:

```yaml
name: PHP CI

on:
  pull_request:
    branches:
      - main
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  php-tests:
    if: github.event.pull_request.draft == false
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
    - uses: actions/checkout@v4

    - name: Run PHP Tests in src directory
      uses: alleyinteractive/action-test-php@v1.0.0-alpha
      with:
        php-version: '8.0'
        working-directory: './src'
        cache-dependency-path: './src/composer.lock'
        audit-skip: 'true'
        test-command: 'composer run-script test:unit'
        build-command: 'composer run-script build:prod'

```

## Inputs

> Specify using `with` keyword.

### `php-version`

- Specify the PHP version to use.
- Accepts a string.
- Defaults to `'latest'`.

### `php-tools`

- Specify the PHP tools to install.
- Accepts a string, comma-separated.
- Defaults to `'composer'`.

### `php-extensions`

- Specify additional PHP extensions to install.
- Accepts a string, comma-separated.
- Defaults to `apcu, bcmath, calendar, ctype, curl, date, dom, exif,
      filter, ftp, gd, gmp, gnupg, hash, iconv,
      igbinary, intl, json, libxml, mbstring, memcache,
      memcached, mysqli, mysqlnd, openssl, pcntl,
      pcre, pdo, pdo_mysql, pdo_sqlite, phar, posix, reflection,
      session, shmop, simplexml, soap, sockets, sodium, spl,
      sqlite3, ssh2, standard, sysvsem, sysvshm, timezonedb,
      tokenizer, xml, xmlreader, xmlwriter, zip, zlib`.

### `php-coverage`

- Specify [coverage support](https://github.com/shivammathur/setup-php?tab=readme-ov-file#signal_strength-coverage-support) for the PHP application.
- Accepts a valid coverage support value (`xdebug`, `pcov`, `none`).
- Defaults to 'none'.

### `wordpress-version`

- Specify the WordPress version to use, or 'false' to skip WordPress installation and related WordPress services. If you specify a version, [test-command](#test-command) will be run from within the context of the WordPress installation.
- Accepts a string.
- Defaults to `'latest'`.

### `wordpress-multisite`

- Specify whether to enable WordPress multisite.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`.

### `wordpress-host`

- Specify the host for the WordPress site.
- Accepts a string. (`'vip'`, `'pantheon'`, or `'false'`)
- Defaults to `'vip'`.

### `working-directory`

- Specify the directory to run the commands in.
- Accepts a string.
- Defaults to `.`.

### `cache-dependency-path`

- Specify the path to the dependency file to use for caching.
- Accepts a string.
- Defaults to `'composer.lock'`.

### `install-skip` or `skip-install`

- Determine whether to skip the composer install step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`.

### `install-command`

- Specify the command to run for composer install.
- Accepts a string.
- Defaults to `'composer install --no-dev --prefer-dist --no-interaction --no-progress'`.

### `audit-skip` or `skip-audit`

- Determine whether to skip the composer audit step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`.

### `audit-command`

- Specify the command to run for composer audit.
- Accepts a string.
- Defaults to `'composer audit --no-dev --locked --ansi --no-interaction --ignore-platform-reqs --no-progress'`.

### `test-skip` or `skip-test`

- Determine whether to skip the test step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`.

### `test-command`

- Specify the command to run for tests.
- Accepts a string.
- Defaults to `'composer run-script test'`.

### `build-command`

- Specify the command to run for build. Unlike the other steps, the default action is to not run a build command.
- Accepts a string.
- Defaults to `''`.

### `github-token`

- Specify the GitHub token to use for Composer authentication (eg. for private repositories).
- Accepts a string.
- Defaults to `''`.

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed
recently.

## Related Projects ❤️

- [alleyinteractive/mantle-ci](https://github.com/alleyinteractive/mantle-ci)
- [shivammathur/setup-php](https://github.com/shivammathur/setup-php)
- [shivammathur/cache-extensions](https://github.com/shivammathur/cache-extensions)


## Credits

This project is actively maintained by [Alley
Interactive](https://github.com/alleyinteractive).

- [Ben Bolton](https://github.com/benpbolton)
- [All Contributors](../../contributors)

## License

The GNU General Public License (GPL) license. Please see [License File](LICENSE)
for more information.⏎
