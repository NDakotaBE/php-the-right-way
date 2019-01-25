---
title:   Datum en tijd
isChild: true
anchor:  date_and_time
---

## Datum en tijd {#date_and_time_title}

PHP heeft een klasse DateTime die je helpt met het lezen, schrijven, vergelijken of rekenen met datums en tijd.
Er zijn veel datum- en tijdgerelateerde functies beschikbaar in PHP naast DateTime, maar deze voorziet een object-oriented interface voor de meeste gevallen.
Het handelt tijdzones af, maar dit is niet het doel van deze korte inleiding.

Om te starten met DateTime kun je een datum en tijds string converteren naar een object met de `createFromFormat()` methode.
Je kunt ook gebruik maken van `new DateTime`om de huidige datum en tijd te verkrijgen. Door hierna gebruik te maken van de `format()` methode kun je een DateTime object omzetten naar een string die bruikbaar is voor output.

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start datum: ' . $start->format('Y-m-d') . "\n";
{% endhighlight %}

Rekenen met DateTime is ook mogelijk met de DateInterval klasse. DateTime stelt methodes zoals `add()` en `sub()` beschikbaar die een DateInterval aannemen als argument.
Schrijf geen code die hetzelfde aantal seconden per dag verwacht, aangezien mechanismes zoals zomeruur/winteruur of wisselen van tijdzones dit patroon zullen verbreken.
Gebruike DateIntervals in de plaats.
Om het verschil tussen datums te bereken kun je de `diff()` methode gebruiken.
Deze zal een nieuw DateInterval object teruggeven die je gemakkelijk kan weergeven.

{% highlight php %}
<?php
// Creëer een kopie van $start en voeg een maand en 6 dagen toe
$end = clone $start;
$end->add(new DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Verschil: ' . $diff->format('%m maand, %d dagen (total: %a dagen)') . "\n";
// Verschil: 1 maand, 6 dagen (total: 37 dagen)
{% endhighlight %}

Op DateTime objecten kun je standaard vergelijkingen toepassen:

{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is voor het eind!\n";
}
{% endhighlight %}

Een laatste voorbeeld geef weer hoe je de DatePeriod klasse kan gebruiken. 
Deze wordt gebruikt om over terugkerende events te lopen/itereren.
DatePeriod neemt 2 verschillende DateTime objecten in, start en eind, en een interval waarvoor het alle events tussen beide zal teruggeven.

{% highlight php %}
<?php
// output all thursdays between $start and $end
$periodInterval = DateInterval::createFromDateString('first thursday');
$periodIterator = new DatePeriod($start, $periodInterval, $end, DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // output each date in the period
    echo $date->format('Y-m-d') . ' ';
}
{% endhighlight %}

Een populaire PHP API extensie is [Carbon](https://carbon.nesbot.com/). Het laat alles toe wat mogelijk is in de DateTime klasse, waardoor je weinig aanpassingen dient te doen, en voegt ook extra features toe zoals ondersteuning voor Localisatie, meer opties om op te tellen, af te trekken en DateTime objecten op te maken. 
Het bied ook mogelijkheden aan om code te testen door datums en tijdstippen te simuleren naar eigen wens.

* [Lees over DateTime][datetime]
* [Lees over datum opmaak][dateformat] (mogelijke datum formatting opties)

[datetime]: https://secure.php.net/book.datetime
[dateformat]: https://secure.php.net/function.date
