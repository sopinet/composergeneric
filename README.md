composergeneric
===============

General composer for Symfony2 use

Use sample
==========

You could install Symfony2 with this composer, you can add more libraries if you need it:

```yaml
{
    "name": "Project name",
    "description": "Project description",
    "autoload": {
        "psr-0": { "": "src/" }
    },
    "repositories": [
        {
            "type": "package",
            "package": {
                "name": "jquery/jquery",
                "version": "1.10.2",
                "dist": {
                    "url": "http://code.jquery.com/jquery-1.10.2.js",
                    "type": "file"
                }
            }
        }
    ], 
    "minimum-stability": "dev",  
    "require": {
        "sopinet/composergeneric": "dev-master"
    }
}
```
