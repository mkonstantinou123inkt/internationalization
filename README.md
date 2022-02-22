[![Minimum PHP Version](https://img.shields.io/badge/php-%3E%3D%208.0-8892BF)](https://php.net/)

# Digital revolution Internationalization

Library to format Numbers, Dates, \Money\Money objects and currencies to string according to the locale.

## Getting Started

```bash
composer require digitalrevolution/intl
```

## Usage

### NumberFormatService
Format number and currencies
```php
use DR\Internationalization\Currency\CurrencyFormatOptions;use DR\Internationalization\Number\NumberFormatOptions;use DR\Internationalization\NumberFormatService;use Money\Money;

// set default configuration
$currencyOptions = (new CurrencyFormatOptions())
    ->setLocale('nl_NL')
    ->setCurrencyCode('EUR')
    ->setGrouping(false);
$numberOptions = (new NumberFormatOptions())
    ->setLocale('nl_NL')
    ->setDecimals(2)
    ->setTrimDecimals(true); 
$service = new NumberFormatService($currencyOptions, $numberOptions);

// format currencies
$service->currency(1500.5);                                                       
// output: € 1500,50

$service->currency(new Money('150050', new Currency('EUR')));                    
// output: € 1500,50

$service->currency(1500.5, (new CurrencyFormatOptions())->setGrouping(true));
// output: € 1.500,50


// format numbers
$service->number(1500.5);                                                        
// output: 1500,50

$service->number(1500.5, (new NumberFormatOptions())->setGrouping(true));   
// output: 1.500,50

$service->number(1500.0, (new NumberFormatOptions())->setTrimDecimals(NumberFormatOptions::TRIM_DECIMAL_ALL_OR_NOTHING));  
// output: 1500

$service->number(1500.5, (new NumberFormatOptions())->setTrimDecimals(NumberFormatOptions::TRIM_DECIMAL_ALL_OR_NOTHING));  
// output: 1500.50

$service->number(1500.5, (new NumberFormatOptions())->setTrimDecimals(NumberFormatOptions::TRIM_DECIMAL_ANY));  
// output: 1500.5
```

### NumberParser
Parse float number from string determining the user's input for thousands and decimals separator.
```php
NumberParser::parseFloat('1050');
// output: 1050.0

NumberParser::parseFloat('1050.5');
// output: 1050.5

NumberParser::parseFloat('1050,5');
// output: 1050.5

NumberParser::parseFloat('1.050,5');
// output: 1050.5

NumberParser::parseFloat('1,050.5');
// output: 1050.5

NumberParser::parseFloat('1,000,050.5');
// output: 1000050.5
```

### DayOfTheWeekFormatter
Format the PHP Date day of the week to string

```php
use DR\Internationalization\Date\DayOfTheWeekFormatter;$formatter = new DayOfTheWeekFormatter('nl_NL');

$formatter->format(DayOfTheWeekFormatter::MONDAY);
// output: maandag

$formatter->format(DayOfTheWeekFormatter::MONDAY, 'en_US');
// output: monday
```


## Project structure

| Directory | Description                                                                                           |
|-----------|-------------------------------------------------------------------------------------------------------|
| Currency  | Format `int`, `float` or `Money` value to locale specific format. Use `NumberFormatService::currency` |
| Date      | Format ISO-8601 day of the week to user friendly names                                                | 
| Money     | Create `Money` object from `float`                                                                    |
| Number    | Format `int` or `float` value to locale specific format. Use `NumberFormatService::number`            |              

## Development

### Run code quality checks:

`composer run check`

### Run unit tests:

`composer run test`

## About us

At 123inkt (Part of Digital Revolution B.V.), every day more than 30 developers are working on improving our internal ERP and our several shops. Do
you want to join us? [We are looking for developers](https://www.werkenbij123inkt.nl/vacatures).
