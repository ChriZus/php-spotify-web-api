> **Warning**
>
> This package is forked from [jwilsson/spotify-web-api-php](https://github.com/jwilsson/spotify-web-api-php) and adapted for my personal preference and use. I do **not** recommend using this package in your project, but use the 
> original project [jwilsson/spotify-web-api-php](https://github.com/jwilsson/spotify-web-api-php)
> 

# Spotify Web API PHP

[![Packagist](https://img.shields.io/packagist/v/chrizus/php-spotify-web-api.svg)](https://packagist.org/packages/chrizus/php-spotify-web-api)
![build](https://github.com/chrizus/php-spotify-web-api/workflows/build/badge.svg)

This is a PHP wrapper for [Spotify's Web API](https://developer.spotify.com/web-api/). It includes the following:

* Helper methods for all API endpoints:
    * Information about artists, albums, tracks, podcasts, audiobooks, and users.
    * List music featured by Spotify.
    * Playlist and user music library management.
    * Spotify catalog search.
    * User playback control.
* Authorization flow helpers.
* Automatic refreshing of access tokens.
* Automatic retry of rate limited requests.
* PSR-4 autoloading support.

## Requirements
* PHP 8.1 or later.
* PHP [cURL extension](http://php.net/manual/en/book.curl.php) (Usually included with PHP).

## Installation
Install it using [Composer](https://getcomposer.org/):

```sh
composer require chrizus/phpspotify-web-api
```

## Usage
Before using the Spotify Web API, you'll need to create an app at [Spotify’s developer site](https://developer.spotify.com/web-api/).

*Note: Applications created after 2021-05-27 [might need to perform some extra steps](https://developer.spotify.com/community/news/2021/05/27/improving-the-developer-and-user-experience-for-third-party-apps/).*

Simple example displaying a user's profile:
```php
require 'vendor/autoload.php';

$session = new SpotifyWebAPI\Session(
    'CLIENT_ID',
    'CLIENT_SECRET',
    'REDIRECT_URI'
);

$api = new SpotifyWebAPI\SpotifyWebAPI();

if (isset($_GET['code'])) {
    $session->requestAccessToken($_GET['code']);
    $api->setAccessToken($session->getAccessToken());

    print_r($api->me());
} else {
    $options = [
        'scope' => [
            'user-read-email',
        ],
    ];

    header('Location: ' . $session->getAuthorizeUrl($options));
    die();
}
```

For more instructions and examples, check out the [documentation](/docs/).

The [Spotify Web API Console](https://developer.spotify.com/web-api/console/) can also be of great help when trying out the API.

## Contributing
Contributions are more than welcome! See [CONTRIBUTING.md](/CONTRIBUTING.md) for more info.

## License
MIT license. Please see [LICENSE.md](LICENSE.md) for more info.
