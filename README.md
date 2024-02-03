 ### Aimeos - THE Laravel ecommerce platform with Added Cooke banner about GDRP European Law inside

 

✅ 100% GDPR compliant
✅ Fully customizable
✅ Works with and without JS


![Aimeos Cookie](https://github.com/chiarraeu/source/blob/main/aimeoscookie.png?raw=true "Aimeos Cookie")

## Features

The main advantage of using these alternatives is that you could avoid asking for explicit consent altogether since you would not use any cookies that aren't strictly necessary. This will always be better for your application's accessibility and user experience.

Nevertheless, this package provides all the tools you'll need to cover a proper EU-compliant cookies policy:

    Cookies registration & configuration
    Blade views & translation files for consent alerts & pop-ups
    Blade directives & Facade methods making your life easier
    JavaScript code that will enhance front-end user experience



## Installation
1. 
```bash
composer require whitecube/laravel-cookie-consent
```
2. `php artisan vendor:publish --tag=laravel-cookie-consent-service-provider` - This will publish the CookiesServiseProvider class in App/Providers

3. Add the Service Provider to the `providers` array in `config/app.php`:
```php

IMPORTANT: add the following line AFTER "App\Providers\RouteServiceProvider::class,"
       
   add this ->    App\Providers\CookiesServiceProvider::class,

```
4. Publish the configuration file: `php artisan vendor:publish --tag=laravel-cookie-consent-config`

5. Publish the customizable views: `php artisan vendor:publish --tag=laravel-cookie-consent-views`

6. Publish the translation files: `php artisan vendor:publish --tag=laravel-cookie-consent-lang`

7. register and configure the used cookies in the freshly published `App\Providers\CookiesServiceProvider::registerCookies()` method:

```php
namespace App\Providers;

use Whitecube\LaravelCookieConsent\Consent;
use Whitecube\LaravelCookieConsent\Facades\Cookies;
use Whitecube\LaravelCookieConsent\CookiesServiceProvider as ServiceProvider;

class CookiesServiceProvider extends ServiceProvider
{
    /**
     * Define the cookies users should be aware of.
     */
    protected function registerCookies(): void
    {
        // Register Laravel's base cookies under the "required" cookies section:
        Cookies::essentials()
            ->session()
            ->csrf();

        // Register all Analytics cookies at once using one single shorthand method:
        Cookies::analytics()
            ->google(env('GOOGLE_ANALYTICS_ID'));
    
        // Register custom cookies under the pre-existing "optional" category:
        Cookies::optional()
            ->name('darkmode_enabled')
            ->description('This cookie helps us remember your preferences regarding the interface\'s brightness.')
            ->duration(120);
            ->accepted(fn(Consent $consent, MyDarkmode $darkmode) => $consent->cookie(value: $darkmode->getDefaultValue()));
    }
}
```
Add 'GOOGLE_ANALYTICS_ID' in the .env file.

```
GOOGLE_ANALYTICS_ID=your_google_analytics_id
```

8. Add consent scripts and modals to the application's views using the following blade directives:

Put the followwing In /vendor/aimeos/aimeos-laravel/views/base.blade.php

Inside the `<head>` tag:
`@cookieconsentscripts:` used to add the package's default JavaScript and any third-party scripts you need to get the end-user's consent for.


Inside the `<body>` tag:
`@cookieconsentview:` used to render the alert or pop-up view.

## Contributing

We welcome contributions from the community. Here are some ways you can contribute to this project:

1. **Report Bugs**: If you find a bug in the source code, you can help us by submitting an issue to our GitHub repository. Even better, you can submit a Pull Request (PR) with a fix.

2. **Request Features**: If you have a feature request, please submit an issue to our GitHub repository. This will help us track the requests and prioritize their implementation.

3. **Improve Documentation**: If you find any errors, inconsistencies, or improvements in the documentation, you can help us by submitting an issue or a Pull Request with the necessary changes.

4. **Submit Pull Requests**: If you have improvements to the codebase, you can submit a Pull Request. Make sure to follow the guidelines below before submitting a Pull Request:

   - Fork the repository and create a new branch for your changes.
   - Ensure that your changes pass the existing tests and lint checks.
   - Add new tests or update existing tests to cover your changes.
   - Update the documentation to reflect your changes.
   - Submit a Pull Request with a clear description of your changes.

5. **Join the Community**: If you're interested in contributing regularly, consider joining our community. This will give you access to our chat platform, where you can ask questions, share ideas, and collaborate with other contributors.

By participating in this project, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md). We expect all contributors to follow this code and treat each other with respect.



### Made with ❤️ for open source
