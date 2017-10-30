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

add:
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

## TODO
List might be not completed.

- move frontend cache `web/cache` to the root directory
- allow to create custom templates
- move files from `files` folder to the root directory
- update `.gitignore`
