UPGRADE FROM 4.3 to 4.4
=======================
# Table of Contents
- [Cache](#cache)
- [Console](#console)
- [Debug](#debug)
- [DependencyInjection](#dependencyinjection)
- [DoctrineBridge](#doctrinebridge)
- [Filesystem](#filesystem)
- [Form](#form)
- [FrameworkBundle](#frameworkbundle)
- [HttpClient](#httpclient)
- [HttpFoundation](#httpfoundation)
- [HttpKernel](#httpkernel)
- [Lock](#lock)
- [Messenger](#messenger)
- [Mime](#mime)
- [MonologBridge](#monologbridge)
- [Process](#process)
- [PropertyAccess](#propertyaccess)
- [Routing](#routing)
- [Security](#security)
- [Serializer](#serializer)
- [Stopwatch](#stopwatch)
- [Translation](#translation)
- [TwigBridge](#twigbridge)
- [TwigBundle](#twigbundle)
- [Validator](#validator)
- [WebProfilerBundle](#webprofilerbundle)
- [WebServerBundle](#webserverbundle)
- [Yaml](#yaml)

Cache
-----

 * Added argument `$prefix` to `AdapterInterface::clear()`

Console
-------

 * Deprecated finding hidden commands using an abbreviation, use the full name instead
 * Deprecated returning `null` from `Command::execute()`, return `0` instead

Debug
-----

 * Deprecated the `Debug` class, use the one from the `ErrorRenderer` component instead
 * Deprecated the `FlattenException` class, use the one from the `ErrorRenderer` component instead
 * Deprecated the component in favor of the `ErrorHandler` component

DependencyInjection
-------------------

 * Made singly-implemented interfaces detection be scoped by file
 * Deprecated support for short factories and short configurators in Yaml

   Before:
   ```yaml
   services:
       my_service:
           factory: factory_service:method
   ```

   After:
   ```yaml
   services:
       my_service:
           factory: ['@factory_service', method]
   ```

 * Deprecated `tagged` in favor of `tagged_iterator`

   Before:
   ```yaml
   services:
       App\HandlerCollection:
           arguments: [!tagged my_tag]
   ```

   After:
   ```yaml
   services:
       App\HandlerCollection:
           arguments: [!tagged_iterator my_tag]
   ```

 * Passing an instance of `Symfony\Component\DependencyInjection\Parameter` as class name to `Symfony\Component\DependencyInjection\Definition` is deprecated.

   Before:
   ```php
   new Definition(new Parameter('my_class'));
   ```

   After:
   ```php
   new Definition('%my_class%');
   ```

DoctrineBridge
--------------
 * Deprecated injecting `ClassMetadataFactory` in `DoctrineExtractor`, an instance of `EntityManagerInterface` should be
   injected instead.
 * Deprecated passing an `IdReader` to the `DoctrineChoiceLoader` when the query cannot be optimized with single id field.
 * Deprecated not passing an `IdReader` to the `DoctrineChoiceLoader` when the query can be optimized with single id field.
 * Deprecated `RegistryInterface`, use `Doctrine\Common\Persistence\ManagerRegistry`.
 * Added a new `getMetadataDriverClass` method to replace class parameters in `AbstractDoctrineExtension`. This method
   will be abstract in Symfony 5 and must be declared in extending classes.

Filesystem
----------

 * Support for passing a `null` value to `Filesystem::isAbsolutePath()` is deprecated.

Form
----

 * Using different values for the "model_timezone" and "view_timezone" options of the `TimeType` without configuring a
   reference date is deprecated.
 * Using `int` or `float` as data for the `NumberType` when the `input` option is set to `string` is deprecated.
 * Overriding the methods `FormIntegrationTestCase::setUp()`, `TypeTestCase::setUp()` and `TypeTestCase::tearDown()` without the `void` return-type is deprecated.

FrameworkBundle
---------------

 * Deprecated booting the kernel before running `WebTestCase::createClient()`.
 * Deprecated support for `templating` engine in `TemplateController`, use Twig instead
 * The `$parser` argument of `ControllerResolver::__construct()` and `DelegatingLoader::__construct()`
   has been deprecated.
 * The `ControllerResolver` and `DelegatingLoader` classes have been marked as `final`.
 * The `controller_name_converter` and `resolve_controller_name_subscriber` services have been deprecated.
 * Deprecated `routing.loader.service`, use `routing.loader.container` instead.
 * Not tagging service route loaders with `routing.route_loader` has been deprecated.
 * Overriding the methods `KernelTestCase::tearDown()` and `WebTestCase::tearDown()` without the `void` return-type is deprecated.

HttpClient
----------

 * Added method `cancel()` to `ResponseInterface`

HttpFoundation
--------------

 * `ApacheRequest` is deprecated, use `Request` class instead.
 * Passing a third argument to `HeaderBag::get()` is deprecated since Symfony 4.4, use method `all()` instead
 * `PdoSessionHandler` now precalculates the expiry timestamp in the lifetime column,
    make sure to run `CREATE INDEX EXPIRY ON sessions (sess_lifetime)` to update your database
    to speed up garbage collection of expired sessions.

HttpKernel
----------

 * The `DebugHandlersListener` class has been marked as `final`
 * Added new Bundle directory convention consistent with standard skeletons:

    ```
    └── MyBundle/
        ├── config/
        ├── public/
        ├── src/
        │   └── MyBundle.php
        ├── templates/
        └── translations/
    ```

   To make this work properly, it is necessary to change the root path of the bundle:

    ```php
    class MyBundle extends Bundle
    {
        public function getPath(): string
        {
            return \dirname(__DIR__);
        }
    }
    ```

   As many bundles must be compatible with a range of Symfony versions, the current
   directory convention is not deprecated yet, but it will be in the future.

 * Deprecated the second and third argument of `KernelInterface::locateResource`
 * Deprecated the second and third argument of `FileLocator::__construct`
 * Deprecated loading resources from `%kernel.root_dir%/Resources` and `%kernel.root_dir%` as
   fallback directories. Resources like service definitions are usually loaded relative to the
   current directory or with a glob pattern. The fallback directories have never been advocated
   so you likely do not use those in any app based on the SF Standard or Flex edition.
 * Getting the container from a non-booted kernel is deprecated

Lock
----

 * Deprecated `Symfony\Component\Lock\StoreInterface` in favor of `Symfony\Component\Lock\BlockingStoreInterface` and
   `Symfony\Component\Lock\PersistingStoreInterface`.
 * `Factory` is deprecated, use `LockFactory` instead

Messenger
---------

 * Deprecated passing a `ContainerInterface` instance as first argument of the `ConsumeMessagesCommand` constructor,
   pass a `RoutableMessageBus`  instance instead.

Mime
----

 * Removed `NamedAddress`, use `Address` instead (which supports a name now)

MonologBridge
--------------

 * The `RouteProcessor` has been marked final.

Process
-------

 * Deprecated the `Process::inheritEnvironmentVariables()` method: env variables are always inherited.

PropertyAccess
--------------

 * Deprecated passing `null` as 2nd argument of `PropertyAccessor::createCache()` method (`$defaultLifetime`), pass `0` instead.

Routing
-------

 * Deprecated `ServiceRouterLoader` in favor of `ContainerLoader`.
 * Deprecated `ObjectRouteLoader` in favor of `ObjectLoader`.

Security
--------

 * The `LdapUserProvider` class has been deprecated, use `Symfony\Component\Ldap\Security\LdapUserProvider` instead.
 * Implementations of `PasswordEncoderInterface` and `UserPasswordEncoderInterface` should add a new `needsRehash()` method
 * Deprecated returning a non-boolean value when implementing `Guard\AuthenticatorInterface::checkCredentials()`. Please explicitly return `false` to indicate invalid credentials.
 * Deprecated passing more than one attribute to `AccessDecisionManager::decide()` and `AuthorizationChecker::isGranted()` (and indirectly the `is_granted()` Twig and ExpressionLanguage function)

   **Before**
   ```php
   if ($this->authorizationChecker->isGranted(['ROLE_USER', 'ROLE_ADMIN'])) {
       // ...
   }
   ```

   **After**
   ```php
   if ($this->authorizationChecker->isGranted(new Expression("has_role('ROLE_USER') or has_role('ROLE_ADMIN')"))) {}

   // or:
   if ($this->authorizationChecker->isGranted('ROLE_USER')
      || $this->authorizationChecker->isGranted('ROLE_ADMIN')
   ) {}
   ```

Serializer
----------

 * Deprecated the `XmlEncoder::TYPE_CASE_ATTRIBUTES` constant. Use `XmlEncoder::TYPE_CAST_ATTRIBUTES` instead.

Stopwatch
---------

 * Deprecated passing `null` as 1st (`$id`) argument of `Section::get()` method, pass a valid child section identifier instead.

Translation
-----------

 * Deprecated support for using `null` as the locale in `Translator`.
 * Deprecated accepting STDIN implicitly when using the `lint:xliff` command, use `lint:xliff -` (append a dash) instead to make it explicit.

TwigBridge
----------

 * Deprecated to pass `$rootDir` and `$fileLinkFormatter` as 5th and 6th argument respectively to the
   `DebugCommand::__construct()` method, swap the variables position.
 * Deprecated accepting STDIN implicitly when using the `lint:twig` command, use `lint:twig -` (append a dash) instead to make it explicit.

TwigBundle
----------

 * Deprecated `twig.exception_controller` configuration option, set it to "null" and use `framework.error_controller` instead:

   Before:
   ```yaml
   twig:
       exception_controller: 'App\Controller\MyExceptionController'
   ```

   After:
   ```yaml
   twig:
       exception_controller: null

   framework:
       error_controller: 'App\Controller\MyExceptionController'
   ```

   The new default exception controller will also change the error response content according to
   https://tools.ietf.org/html/rfc7807 for `json`, `xml`, `atom` and `txt` formats:

   Before:
   ```json
   {
       "error": {
           "code": 404,
           "message": "Sorry, the page you are looking for could not be found"
       }
   }
   ```

   After:
   ```json
   {
       "title": "Not Found",
       "status": 404,
       "detail": "Sorry, the page you are looking for could not be found"
   }
   ```

 * Deprecated the `ExceptionController` and `PreviewErrorController` controllers, use `ErrorController` from the HttpKernel component instead
 * Deprecated all built-in error templates, use the error renderer mechanism of the `ErrorRenderer` component
 * Deprecated loading custom error templates in non-html formats. Custom HTML error pages based on Twig keep working as before:

   Before (`templates/bundles/TwigBundle/Exception/error.jsonld.twig`):
   ```twig
   {
       "@id": "https://example.com",
       "@type": "error",
       "@context": {
           "title": "{{ status_text }}",
           "code": {{ status_code }},
           "message": "{{ exception.message }}"
       }
   }
   ```

   After (`App\ErrorRenderer\JsonLdErrorRenderer`):
   ```php
   class JsonLdErrorRenderer implements ErrorRendererInterface
   {
       public static function getFormat(): string
       {
           return 'jsonld';
       }

       public function render(FlattenException $exception): string
       {
           return json_encode([
               '@id' => 'https://example.com',
               '@type' => 'error',
               '@context' => [
                   'title' => $exception->getTitle(),
                   'code' => $exception->getStatusCode(),
                   'message' => $exception->getMessage(),
               ],
           ]);
       }
   }
   ```

  Configure your rendering service tagging it with `error_renderer.renderer`.

Validator
---------

 * Deprecated passing an `ExpressionLanguage` instance as the second argument of `ExpressionValidator::__construct()`.
 * Deprecated using anything else than a `string` as the code of a `ConstraintViolation`, a `string` type-hint will
   be added to the constructor of the `ConstraintViolation` class and to the `ConstraintViolationBuilder::setCode()`
   method in 5.0.
 * Deprecated passing an `ExpressionLanguage` instance as the second argument of `ExpressionValidator::__construct()`.
   Pass it as the first argument instead.
 * The `Length` constraint expects the `allowEmptyString` option to be defined
   when the `min` option is used.
   Set it to `true` to keep the current behavior and `false` to reject empty strings.
   In 5.0, it'll become optional and will default to `false`.
 * Overriding the methods `ConstraintValidatorTestCase::setUp()` and `ConstraintValidatorTestCase::tearDown()` without the `void` return-type is deprecated.
 * deprecated `Symfony\Component\Validator\Mapping\Cache\CacheInterface` and all implementations in favor of PSR-6.
 * deprecated `ValidatorBuilder::setMetadataCache`, use `ValidatorBuilder::setMappingCache` instead.
 * The `Range` constraint has a new message option `notInRangeMessage` that is used when both `min` and `max` values are set.
   In case you are using custom translations make sure to add one for this new message.

WebProfilerBundle
-----------------

 * Deprecated the `ExceptionController` class in favor of `ExceptionErrorController`
 * Deprecated the `TemplateManager::templateExists()` method

WebServerBundle
---------------

 * The bundle is deprecated and will be removed in 5.0.

Yaml
----

* Deprecated accepting STDIN implicitly when using the `lint:yaml` command, use `lint:yaml -` (append a dash) instead to make it explicit.
