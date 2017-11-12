# Shopware Composer Project

The idea of the project is to use Shopware as a composer dependency.

Note: Project is not finished yet.

## Installation
`composer create-project luklewluk/shopware-composer-project [directory name]`

### Command Line
WIP

### Nginx

Some static files for Administration Panel are inside the engine folder. Because of that small changes to nginx
configuration are required:

From:
```
try_files $uri /shopware.php?controller=Media&action=fallback;
```
To:
```
try_files $uri /vendor/shopware/shopware/$uri /shopware.php?controller=Media&action=fallback;
```

In following locations

`location ~* "^/themes/Frontend/Responsive/frontend/_public/vendors/fonts/open-sans-fontface/(?:.+)\.(?:ttf|eot|svg|woff)$"`

`location ~* "^/themes/Frontend/Responsive/frontend/_public/src/fonts/(?:.+)\.(?:ttf|eot|svg|woff)$"`

`location ~* "^/web/cache/(?:[0-9]{10})_(?:.+)\.(?:js|css)$"`

Replace `try_files` with:
```
try_files $uri /vendor/shopware/shopware/$uri;
```

Example:
```
        location ~* "^/themes/Frontend/Responsive/frontend/_public/vendors/fonts/open-sans-fontface/(?:.+)\.(?:ttf|eot|svg|woff)$" {
            expires max;
            add_header Cache-Control "public";
            access_log off;
            log_not_found off;
            try_files $uri /vendor/shopware/shopware/$uri;
        }
```

## Plugins

Plugins can be installed using the Shopware way (coping files to the directories and by the backend) or using
composer if plugin uses [Composer Installers](https://github.com/composer/installers).

## TODO
List may be not completed.

- allow to create custom templates (it already works by custom plugins but needs more tests)
- move frontend cache `web/cache` to the root directory
- move `files` and `media` folders to the root directory
- installation by composer scripts
- update `.gitignore`
- build tests
