# home-assistant-energy-tariff-templates
An aggregation of all of the energy tarriff templates

# Electric Energy companies by country

Source:  https://query.wikidata.org/ -> https://w.wiki/D$Jn
```
SELECT ?company ?companyLabel ?countryLabel ?website ?description WHERE {
  ?company wdt:P31 ?type;
           wdt:P452 wd:Q2316331;        # Industry: Electricity generation
  OPTIONAL { ?company wdt:P17 ?country. } # Optional: Country
  OPTIONAL { ?company wdt:P856 ?website. } # Official website
  OPTIONAL { ?company schema:description ?description. } # Description
  FILTER NOT EXISTS { ?company wdt:P576 ?endDate. } # Exclude companies with an industry end date

  VALUES ?type { wd:Q4830453 wd:Q43229 } # Business (Q4830453) or Organization (Q43229)

  SERVICE wikibase:label { 
    bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en".
  }
}
LIMIT 1000
```
