# AWS SSM Parameters loader for PHP

[![Latest](https://poser.pugx.org/sunaoka/aws-ssm-parameters-loader-php/v)](https://packagist.org/packages/sunaoka/aws-ssm-parameters-loader-php)
[![License](https://poser.pugx.org/sunaoka/aws-ssm-parameters-loader-php/license)](https://packagist.org/packages/sunaoka/aws-ssm-parameters-loader-php)
[![PHP](https://img.shields.io/packagist/php-v/sunaoka/aws-ssm-parameters-loader-php)](composer.json)
[![Test](https://github.com/sunaoka/aws-ssm-parameters-loader-php/actions/workflows/test.yml/badge.svg)](https://github.com/sunaoka/aws-ssm-parameters-loader-php/actions/workflows/test.yml)
[![codecov](https://codecov.io/gh/sunaoka/aws-ssm-parameters-loader-php/branch/main/graph/badge.svg?token=PK3P6j6Jrz)](https://codecov.io/gh/sunaoka/aws-ssm-parameters-loader-php)

----

Load values from AWS SSM Parameter store into environment variables for Laravel

## Installation

```bash
composer require sunaoka/aws-ssm-parameters-loader-php
```

## Usage

### Create a SSM Parameter

```bash
aws ssm put-parameter --name '/path/to/value' --type String --value 'my secret value'
```

### Example 1

```php
use Aws\Ssm\SsmClient;
use Sunaoka\SsmParametersLoader\ParametersLoader;

putenv('MY_PARAMETER=ssm:/path/to/value')

$client = new SsmClient([
    // arguments
]);

$loader = new ParametersLoader($client, 'ssm:');
$loader->load();

echo env('MY_PARAMETER');
// my secret value
```

### Example 2

```php
use Aws\Ssm\SsmClient;
use Sunaoka\SsmParametersLoader\ParametersLoader;

putenv('MY_PARAMETER=ssm:/path/to/value')

$client = new SsmClient([
    // arguments
]);

$loader = new ParametersLoader($client, 'ssm:');
$result = $loader->getParameters();

var_dump($result);
// array(1) {
//   'MY_PARAMETER' =>
//   string(15) "my secret value"
// }
```
