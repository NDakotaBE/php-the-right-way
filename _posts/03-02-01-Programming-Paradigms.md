---
title: Programming Paradigms
isChild: true
anchor:  programming_paradigms
---

## Programming Paradigms {#programming_paradigms_title}

PHP is een flexibele, dynamische programeertaal die een verscheidenheid aan programmeertechnieken 
ondersteunt.
Ze is drastisch geëvolueerd over de jaren heen, in het bijzonder door de toevoeging van een 
solide object-oriented model in PHP5.0 (2004), anonieme functies en namespaces in PHP5.3 (2009) 
en traits in PHP5.4 (2012).

### Object-oriented programmeren

PHP heeft een complete set van object-oriented programming features inclusief ondersteuning voor 
klasses, abstracte klasses, interfaces, inheritance, constructors, klonen, exceptions en meer

* [Lees over Object-oriented PHP][oop]
* [Lees over Traits][traits]

### Functional programmeren

PHP ondersteund eerste-class functies. Dit wil zeggen dat een functie geassigneerd kan worden
aan een variabele. 
Zowel gebruikers gedefinieerde en ingebouwde functies kunnen naar een variable verwezen worden en
dynamisch opgeropen worden. 
Functies kunnen ook doorgegevens worden als argumenten aan andere fucties. (Een feature genoemt _Higher-order Functions_) en functies kunnen andere functies teruggeven.

Recursie, een feature die toelaat dat een functie zichzelf aanroept, wordt ondersteund door de taal, maar de meeste PHP code is gefocused op iteratie.

Nieuwe anonieme functies (met ondersteuning voor closures) zijn beschikbaar sinds PHP5.3 (2009).

PHP 5.4 voegde de mogelijk om closures vast te hangen aan de scope van een object en voegde ook ondersteuning voor callabes toe, opdat deze gebruikt kunnen worden met anonieme functies in de meeste gevallen.

* Lees verder over [functioneel programmeren in PHP](/pages/Functional-Programming.html)
* [Lees over Anonymous Functions][anonymous-functions]
* [Lees over the Closure class][closure-class]
* [More details in the Closures RFC][closures-rfc]
* [Lees over Callables][callables]
* [Lees over dynamically invoking functions with `call_user_func_array()`][call-user-func-array]

### Meta programmeren

PHP ondersteund verschillende manieren van meta-programmeren door mechanismes zoals de 
Reflections API en Magic Methods.
Er zijn veel Magic Methods beschikbaar zoals `__get()`, `__set()`, `__clone()`, `__toString()`, 
`__invoke()`, ed. die ontwikkelaars toelaten om aanpassingen door te voeren in de gedraging van 
een klasse.
Ruby ontwikkelaars zeggen vaak dat PHP de `method_missing` functie mist, maar deze is beschikbaar 
als  `__call()` en `__callStatic()`.

* [Lees over Magic Methods][magic-methods]
* [Lees over Reflection][reflection]
* [Lees over Overloading][overloading]


[oop]: https://secure.php.net/language.oop5
[traits]: https://secure.php.net/language.oop5.traits
[anonymous-functions]: https://secure.php.net/functions.anonymous
[closure-class]: https://secure.php.net/class.closure
[closures-rfc]: https://wiki.php.net/rfc/closures
[callables]: https://secure.php.net/language.types.callable
[call-user-func-array]: https://secure.php.net/function.call-user-func-array
[magic-methods]: https://secure.php.net/language.oop5.magic
[reflection]: https://secure.php.net/intro.reflection
[overloading]: https://secure.php.net/language.oop5.overloading

