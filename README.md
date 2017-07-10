# Laravel-CampaignMonitor
A Laravel 5 wrapper for CampaignMonitor APIs

- [Laravel-CampaignMonitor on Packagist](https://packagist.org/packages/bashy/laravel-campaignmonitor)
- [Laravel-CampaignMonitor on GitHub](https://github.com/bbashy/Laravel-CampaignMonitor)


## Installation

Pull in the package through Composer;
```
composer require bashy/laravel-campaignmonitor
```

Register the service provider by opening up `config/app.php` and finding the `providers` key;
```php
'providers' => [
    Bashy\CampaignMonitor\CampaignMonitorServiceProvider::class,
]
```

Laravel-CampaignMonitor also ships with a facade. You can register the facade in the `aliases` key of your `config/app.php` file;
```php
'aliases' => [
    'CampaignMonitor' => Bashy\CampaignMonitor\Facades\CampaignMonitor::class,
]
```

Publish the config file;
```
$ php artisan vendor:publish --provider="Bashy\CampaignMonitor\CampaignMonitorServiceProvider"
```

And set your own API key and Client ID via .env or similar to match these;
```php
return [

    'api_key' => env('CAMPAIGNMONITOR_API_KEY'),

    'client_id' => env('CAMPAIGNMONITOR_CLIENT_ID'),

];
```

## Usage

You can find all the methods in the original [campaignmonitor/createsend-php package](https://github.com/campaignmonitor/createsend-php).

Some examples;
```php
// Add an user to a List ID:
$result = CampaignMonitor::subscribers('LIST_ID')->add([
    'EmailAddress' => 'example@gmail.com',
    'Name' => 'Ben',
]);

// Create a list for a Client:
$result = CampaignMonitor::lists()->create(config('campaignmonitor.client_id'), [
    'Title' => 'List name',
]);
```

To send classic transactional emails:
```php
$data = [
    'From' => 'from@example.org',
    'To' => 'to@example.org',
    'ReplyTo' => 'replyto@example.org',
    'CC' => 'cc@example.org',
    'BCC' => 'bcc@example.org',
    'HTML' => '<p>Hello there!</p>',
    'Text' => 'Hello there!',
];

CampaignMonitor::classicSend('CLIENT_ID')->send($data);
```
