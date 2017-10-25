# Shopware Composer Project

The idea of the project is to use Shopware as a composer dependency.

Note: Project is not finished yet.

## Installation
`composer create-project luklewluk/shopware-composer-project [directory name]`

### Nginx

Some static files for Administration Panel are inside the engine folder. Because of that a small change to nginx
configuration is required:

From:
```
try_files $uri /shopware.php?controller=Media&action=fallback;
```
To:
```
try_files $uri /vendor/shopware/shopware/$uri /shopware.php?controller=Media&action=fallback;
```

## TODO
List might be not completed.

- move cache folders to the root directory
- test custom templates
- move files from `files` folder to the root directory
- update `.gitignore`
