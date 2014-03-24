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
    "minimum-stability": "dev",  
    "require": {
        "sopinet/composergeneric": "dev-master"
    }
}
```
AppKernel.php
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
    
doctrine:
    dbal:
        types:
            json: Sonata\Doctrine\Types\JsonType
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
