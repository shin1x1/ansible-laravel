# Laravel

Ansible role to easily deploy Laravel 4 applications. It's inspired by [https://github.com/servergrove/ansible-symfony2](https://github.com/servergrove/ansible-symfony2).

This role is supported below features.

* create application directories(Capisrano style)
* deploy application code
* composer install
* php artisan migrate
* php artisan db:seed(optional)
* execute phpunit(optional)

```
.
├── current -> symlink to latest deployed release_version
├── releases
│   └── release_version
└── shared
    └── storage
        ├── cache
        ├── logs
        ├── meta
        ├── sessions
        └── views
```

## Laravel Application Settings

### Storage directory

Application storage directory change to below.

```bootstrap/path.php
   'storage' = __DIR__ . '/../../../shared/storage',
```


## Role Variables

|variable|comment|default|
|--------|-------|-------|
|laravel_app_release_version|Release Number.(version number, datetime, etc)|1|
|laravel_local_app_path|Application local_path(for rsync)|../../../../src/|
|laravel_app_path|Path where application will be deployed on server.|/var/www/app|
|laravel_app_current_path||{{ laravel_app_path }}/current|
|laravel_app_releases_path||{{ laravel_app_path }}/releases|
|laravel_app_releases_version_path||{{ laravel_app_releases_path }}/{{ laravel_app_release_version }}|
|laravel_app_shared_path||{{ laravel_app_path }}/shared|
|laravel_deploy|Deploy method(rsync, share, git)|share|
|laravel_env|Laravel application environment(local, production, etc)|local|
|laravel_phpunit|If set true then phpunit execute after deployed.(Boolean)|no|
|laravel_db_seeds|Execute Database seeder.(List)|None|


## Dependencies

None

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      vars:
        laravel_app_release_version: 1
        laravel_app_root_path: /var/www/app
        laravel_deploy: rsync
        laravel_env: production
        laravel_db_seeds:
          - DatabaseSeeder
      roles:
        - shin1x1.laravel

## License

MIT

## Author Information

Contributions are welcome: https://github.com/shin1x1/ansible-laravel

