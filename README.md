Description
===========

General composer for Symfony2 use. Install a Symfony2 system easy and quickly.

Installing Symfony 2.4
======================

```
cd /var/www
curl -sS https://getcomposer.org/installer | php
php composer.phar create-project symfony/framework-standard-edition MyProject "2.4.*"
```

Modify Composer
===============
You could install Symfony2 with this composer, you can add more libraries if you need it:

```yaml
{
    "name": "Project name",
    "description": "Project description",
    "autoload": {
        "psr-0": { "": "src/" }
    },
    "minimum-stability": "dev",  
    "require": {
        "sopinet/composergeneric": "dev-master"
    }
}
```

Now... execute composer.phar update

Add to AppKernel.php
=============
```yaml
new JMS\AopBundle\JMSAopBundle(),
new JMS\DiExtraBundle\JMSDiExtraBundle($this),
new JMS\SecurityExtraBundle\JMSSecurityExtraBundle(),
new FOS\UserBundle\FOSUserBundle(),
new Knp\Bundle\MenuBundle\KnpMenuBundle(),
new Sonata\AdminBundle\SonataAdminBundle(),
new Sonata\CoreBundle\SonataCoreBundle(),
new Sonata\BlockBundle\SonataBlockBundle(),
new Sonata\CacheBundle\SonataCacheBundle(),
new Sonata\jQueryBundle\SonatajQueryBundle(),
new Sonata\EasyExtendsBundle\SonataEasyExtendsBundle(),
new Sonata\UserBundle\SonataUserBundle('FOSUserBundle'),
new Sonata\DoctrineORMAdminBundle\SonataDoctrineORMAdminBundle(),
new Knp\Bundle\PaginatorBundle\KnpPaginatorBundle(),
new Craue\FormFlowBundle\CraueFormFlowBundle(),                
new Doctrine\Bundle\FixturesBundle\DoctrineFixturesBundle(), 
new Stof\DoctrineExtensionsBundle\StofDoctrineExtensionsBundle(),
new A2lix\TranslationFormBundle\A2lixTranslationFormBundle(),
new JMS\SerializerBundle\JMSSerializerBundle($this),
new FOS\RestBundle\FOSRestBundle(),     
new Sopinet\Bundle\BootstrapExtendBundle\SopinetBootstrapExtendBundle(),
new RaulFraile\Bundle\LadybugBundle\RaulFraileLadybugBundle()
```

config.yml
==========

Add:

```yaml
framework:
    translator:      ~

fos_user:
    db_driver: orm # other valid values are 'mongodb', 'couchdb' and 'propel'
    firewall_name: main
    user_class: Application\Sonata\UserBundle\Entity\User
    group:
       group_class: Test\BaseBundle\Entity\Group
       
sonata_block:
    default_contexts: [cms]

```

Modify doctrine part:

```yaml
# Doctrine Configuration
doctrine:
    dbal:
        driver:   "%database_driver%"
        host:     "%database_host%"
        port:     "%database_port%"
        dbname:   "%database_name%"
        user:     "%database_user%"
        password: "%database_password%"
        charset:  UTF8
        # if using pdo_sqlite as your database driver, add the path in parameters.yml
        # e.g. database_path: "%kernel.root_dir%/data/data.db3"
        # path:     "%database_path%"
        types:
            json: Sonata\Doctrine\Types\JsonType
        mapping_types:
            enum: string                    

    orm:
        auto_generate_proxy_classes: "%kernel.debug%"
        auto_mapping: true
        
stof_doctrine_extensions:
    default_locale: %locale%
    translation_fallback: true    
    orm:
        default:
            translatable: true
    uploadable:
        validate_writable_directory: true 
```

Monolog config for log on files

```yaml
monolog:
    handlers:
        main:
            type:   stream
            path:   "%kernel.logs_dir%/%kernel.environment%.log"
            level:  debug
        console:
            type:   console
            bubble: false
        # uncomment to get logging in your browser
        # you may have to allow bigger header sizes in your Web server configuration
        #firephp:
        #    type:   firephp
        #    level:  info
        #chromephp:
        #    type:   chromephp
        #    level:  info
```

Monolog config for log on email(params 'from' and 'to' are required)


```yaml
monolog:
    handlers:
        main:
            type:         fingers_crossed
            action_level: error
            handler:      nested
        nested:
            type:  stream
            path:  "%kernel.logs_dir%/%kernel.environment%.log"
            level: debug
        console:
            type:  console

elao_error_notifier:
    from: 
    to: 
    handle404: true
    mailer: mailer
    handlePHPErrors: true
    handlePHPWarnings: false
    ignoredClasses: ~
    repeatTimeout: 3600   
```

SonataUser
==========
```yaml
php app/console sonata:easy-extends:generate SonataUserBundle --dest src
```
Añadir a AppKernel:
```yaml
new Application\Sonata\UserBundle\ApplicationSonataUserBundle()
```
Security (Optional)
===================

```yaml
security:
    encoders:
        FOS\UserBundle\Model\UserInterface: sha512

    role_hierarchy:
        ROLE_ADMIN:       ROLE_USER
        ROLE_SUPER_ADMIN: [ROLE_USER, ROLE_ADMIN, ROLE_ALLOWED_TO_SWITCH]

    providers:
        fos_userbundle:
            id: fos_user.user_provider.username

    firewalls:
        main:
            pattern: ^/
            form_login:
                provider: fos_userbundle
                login_path: /login
                check_path: /login_check 
                default_target_path: /panel
                always_use_default_target_path: true
                csrf_provider: form.csrf_provider
            logout:       true
            anonymous:    true

    access_control:
        - { path: ^/login$, role: IS_AUTHENTICATED_ANONYMOUSLY }       
        - { path: ^/register, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/resetting, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin/, role: ROLE_ADMIN }
```
