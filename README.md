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





### Made with ❤️ for open source
