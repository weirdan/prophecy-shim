# Prophecy Shim

Compatibility shim to be able to use ProphecyTrait with older PHPUnit versions.

## Motivation

Starting with PHPUnit 9.1 Prophecy integration that used to be provided by
PHPUnit itself is deprecated and is scheduled to be removed in PHPUnit 10.
There is `phpspec/prophecy-phpunit` package providing the integration now, but
what do you do if you need to run your tests with older PHPUnit versions like
7.x?

This package solves this by providing empty ProphecyTrait for those older
versions that you can import into your tests. For PHPUnit 9.1+ it just requires
`phpspec/prophecy-phpunit` that provides the same trait. As a result, you can
import the trait into your tests and it will work regardless of the PHPUnit
version.

## Installation

```console
composer require --dev psalm/prophecy-shim:'^1.0 || ^2.0'
```

## Usage

```php
<?php

namespace Your\Tests;

use PHPUnit\Framework\TestCase;

// The following trait it provided either by the shim or by phpspec/prophecy-phpunit
use Prophecy\PhpUnit\ProphecyTrait;

class YourTest extends TestCase
{
    use ProphecyTrait;

    public function testSomething(): void
    {
        // this won't throw warnings anymore in PHPUnit 9.1+
        $objectProphecy = $this->prophesize(SomeClass::class);
    }
}
```
