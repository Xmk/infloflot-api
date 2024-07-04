# infloflot-api

[![Latest Version](https://img.shields.io/packagist/v/cryptoweb/infoflot-api)](https://packagist.org/packages/cryptoweb/infoflot-api)
[![License](https://img.shields.io/packagist/l/cryptoweb/infoflot-api)](https://packagist.org/packages/cryptoweb/infoflot-api)

## ATTENTION!

⚠️ This package is at an early stage of development!

### basic docs:

https://restapi.infoflot.com/docs

## Installation

```bash
composer require cryptoweb/infoflot-api
```

## Usage

### client initialization
```php
require 'vendor/autoload.php';

use CryptoWeb\InfoflotApi\Client;
use CryptoWeb\InfoflotApi\ClientOptions;

$client = new Client(
	new GuzzleHttp\Client(),
	new ClientOptions(
		apiKey: 'your-api-key',
	)
);
```

### usage basic
```php
$result = $client->request('cruises', ['id' => 123]);
```

### builders
```php
use CryptoWeb\InfoflotApi\Builders\Cruises;
use CryptoWeb\InfoflotApi\Builders\CruisesId;
use CryptoWeb\InfoflotApi\Builders\CruisesIdCabins;
use CryptoWeb\InfoflotApi\Builders\CruisesIdCabinsSearch;

// get all cruises
$cruisesBuilder = new Cruises($client);
$cruisesBuilder->nights(5);
$cruisesResult = $cruisesBuilder->get();

// or
$cruisesResult = (new Cruises($client))
	->nights(5)
	->get();

// get cruise by id
$cruiseBuilder = new CitiesId($client);
$cruiseBuilder->id(123);
$cruiseResult = $cruiseBuilder->get();

// get cruise cabins by id
$cruiseCabinsResult = (new CruisesIdCabins($client))
	->id(123)
	->get();

// etc.
```

### factory
```php
use CryptoWeb\InfoflotApi\Infoflot;

$infoflot = new Infoflot($client);

$infoflot->cruises()
	->nights(5)
	->get();

$infoflot->cruises(100500)
	->get();

$infoflot->cruises(100500)
	->cabins()
	->get();

$infoflot->cruises(100500)
	->cabins()
	->search()
	->get();

// etc.
```

## License

The MIT License (MIT). Please see [LICENSE](LICENSE) for more information.
