# home-assistant-energy-tariff-templates
An aggregation of all of the energy tarriff templates

# Electric Energy companies by country

Source:  https://query.wikidata.org/
```
SELECT ?company ?companyLabel ?countryLabel ?website WHERE {
  ?company wdt:P31 wd:Q4830453;        # Instance of business
           wdt:P452 wd:Q2316331;        # Industry: Electric power industry
  OPTIONAL { ?company wdt:P17 ?country. } # Country
  OPTIONAL { ?company wdt:P856 ?website. } # Official website

  SERVICE wikibase:label { 
    bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en".
  }
}
LIMIT 1000
```
