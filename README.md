# Parameters manager

[![Build Status](https://travis-ci.org/WebChemistry/Parameters.svg?branch=master)](https://travis-ci.org/WebChemistry/Parameters)

## Co to umí?
- Importovat výchozí hodnoty parametrů z konfigu.
- Cache parametrů z databáze
- Invalidaci cache parameterů při změně nebo v debug baru
- Import změněných parametrů
- Zobrazit aktuální a výchozí hodnoty v debug baru
- Import nových parametrů z debug baru

## Konfigurace

```yaml
extensions:
    params: WebChemistry\Parameters\DI\ParametersExtension

params:
    paramsSettings:
        cache: yes
        bar: %debugMode%
        database: Doctrine # Vlastní třída nebo NetteDatabase
        entity: Entity\Parameters
```

Použití:
```yaml
params:
    boolean: yes
    float: 1.0
    int: 5
    empty: # NULL
    array:
        first: first
        second: second
        array:
            third: third
```

## Presenter, latte

```php
<?php

namespace App\Presenters;

use Nette;
use WebChemistry\Parameters\Traits\TPresenter;

class BasePresenter extends Nette\Application\UI\Presenter {
    
    use TPresenter;
    
    // Použití v presenteru přes $this->parametersProvider
}
```

```html
Můj parameter: {$parameters['first']}
Můj parameter: {$parameters->first}
Můj parameter: {$parameters->array->first}
Můj parameter: {$parameters->array['first']}
```

## Úprava parametrů

```php
$parametersProvider->myVariable = 'new value';

$parametersProvider->merge(); // Invalidace cache a provede změny v databazi
```

## Debug
![Debug bar](https://ctrlv.cz/shots/2016/01/06/5x5z.png "Debug bar")
