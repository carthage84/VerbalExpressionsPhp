# VerbalExpressionsPhp

PHP port of [jehna/VerbalExpressions][1].

## Example usage

```` php
<?php

require_once 'vendor/autoload.php';

use MarkWilson\VerbalExpression;

// initialise verbal expression instance
$verbalExpression = new VerbalExpression();

// URL matcher
$verbalExpression->startOfLine()
                 ->then('http')
                 ->maybe('s')
                 ->then('://')
                 ->maybe('www.')
                 ->anythingBut(' ')
                 ->endOfLine();

// compile expression - returns ^(http)(s)?(\:\/\/)(www\.)?([^\ ]*)$
$verbalExpression->compile();

// perform match
preg_match($verbalExpression, 'http://www.google.com');
````

## Nesting expressions

```` php
<?php

require_once 'vendor/autoload.php';

use MarkWilson\VerbalExpression;

$innerExpression = new VerbalExpression();
$innerExpression->word();

$outerExpression = new VerbalExpression();
$outerExpression->startOfLine()
                ->then($innerExpression)
                ->then($innerExpression)
                ->endOfLine();

// returns ^(\w+)(\w+)$
$outerExpression->compile();
````



  [1]: https://github.com/jehna/VerbalExpressions "jehna/VerbalExpressions"
