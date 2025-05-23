# home-assistant-energy-tariff-templates
An aggregation of all of the energy tarriff templates, addons and similar.

Missing one? Send in a PR!

Recommended structure: Create two template sensors, one for current tarriff, one for the price of the tarriff.



# Generate with ChatGPT or similar

## Template sensor for current tarriff

The easiest way to quickly generate a [Template](https://www.home-assistant.io/docs/configuration/templating/) is via a LLM.

[Example](https://chat.openai.com/?model=gpt-4&prompt=Generate%20a%20Home%20Assistant%20template%20sensor%20for%20the%20following%20energy%20rate%20tarriffs%0A01%3A00%20to%2006%3A00%20is%20%22offpeak%22%0A10%3A00%20to%2015%3A00%20is%20%22shoulder%22%0AAll%20other%20times%20are%20%22peak%22
)

You should end up with a YAML template such as:
```
template:
  - sensor:
      - name: "Energy Tariff"
        unique_id: energy_tariff
        state: >
          {% set now = now().time() %}
          {% if now >= today_at("01:00") and now < today_at("06:00") %}
            offpeak
          {% elif now >= today_at("10:00") and now < today_at("15:00") %}
            shoulder
          {% else %}
            peak
          {% endif %}
        icon: mdi:clock-time-three
```

When translating into the UI.

![image](https://github.com/user-attachments/assets/c3844044-80e4-4157-b292-0ee755812fb8)

https://my.home-assistant.io/redirect/developer_template/


## Template sensor for current price



# Electricity Tarriff Addons or Templates for Home Assistant

## Australia

- https://community.home-assistant.io/t/guide-australian-electricity-demand-tariffs-e-g-agl/436298
- [AusGrid TOU Tarrifs](https://community.home-assistant.io/t/energy-sensor-price-to-handle-changing-energy-tariff-rates/349080) (2021)
  - [Powershop EV NSW](https://community.home-assistant.io/t/energy-sensor-price-to-handle-changing-energy-tariff-rates/349080/2?u=clockwerx) (2021)
  - [SRP Energy Tariff EZ-3](https://community.home-assistant.io/t/energy-sensor-price-to-handle-changing-energy-tariff-rates/349080/17?u=clockwerx) (2024)
  - [Globird TOU 3-tariff plan](https://community.home-assistant.io/t/energy-sensor-price-to-handle-changing-energy-tariff-rates/349080/18?u=clockwerx) (2024)
- [Ovo](https://www.reddit.com/r/homeassistant/comments/193j204/comment/khbb4xe/)

## Slovenian Network Tariff (Omrežnina)

- https://github.com/frlequ/home-assistant-network-tariff

## UK

### Octopus Energy

- [HomeAssistant-OctopusEnergy](https://github.com/BottlecapDave/HomeAssistant-OctopusEnergy) by [@BottlecapDave](https://github.com/BottlecapDave/)
- https://www.speaktothegeek.co.uk/2023/02/off-peak-tariffs-in-home-assistants-energy-dashboard/

## Spain

- [Datadis](https://github.com/uvejota/homeassistant-edata?tab=readme-ov-file#Configurar-la-tarificaci%C3%B3n)

# Other Electric Energy companies by country

Source:  https://query.wikidata.org/
```
SELECT DISTINCT ?company ?companyLabel ?countryLabel ?website ?description WHERE {
  ?company wdt:P31 ?type;
           wdt:P452 ?industry;        # Industry: Electricity generation
  OPTIONAL { ?company wdt:P17 ?country. } # Optional: Country
  OPTIONAL { ?company wdt:P856 ?website. } # Official website
  OPTIONAL { 
    ?company schema:description ?description. 
    FILTER(LANG(?description) = "en") # Only English description
  }
  FILTER NOT EXISTS { ?company wdt:P576 ?endDate. } # Exclude companies with an industry end date

  VALUES ?type { wd:Q4830453 wd:Q43229 } # Business (Q4830453) or Organization (Q43229)
  VALUES ?industry { wd:Q2316331 wd:Q2356921 wd:Q2316331 }

  SERVICE wikibase:label { 
    bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en".
  }
}
ORDER BY ?countryLabel ?companyLabel
LIMIT 1000
```

### Is your electricity supplier missing?

Head to wikidata, look them up and make sure they have an *industry* set of wd:Q2316331; as well as being an business or organization.

###


<html><head><meta charset="utf-8"></head><body><table><thead><tr><th>company</th><th>companyLabel</th><th>countryLabel</th><th>website</th><th>description</th></tr></thead><tbody><tr><td>http://www.wikidata.org/entity/Q5800734</td><td>Forces Elèctriques d'Andorra</td><td>Andorra</td><td>https://www.feda.ad/</td><td>Forces Elèctriques d'Andorra (English: Andorran Electric Forces, FEDA) is the company in charge of Andorra's electricity supply.</td></tr><tr><td>http://www.wikidata.org/entity/Q292374</td><td>AGL Energy</td><td>Australia</td><td>https://www.agl.com.au/</td><td>Australian energy utilities company</td></tr><tr><td>http://www.wikidata.org/entity/Q4726783</td><td>Alinta Energy</td><td>Australia</td><td>https://www.alintaenergy.com.au</td><td>Australian electricity generating and gas retailing private company</td></tr><tr><td>http://www.wikidata.org/entity/Q5014458</td><td>CS Energy</td><td>Australia</td><td>https://www.csenergy.com.au/</td><td>Australian electricity generating company</td></tr><tr><td>http://www.wikidata.org/entity/Q5254617</td><td>Delta Electricity</td><td>Australia</td><td>http://www.de.com.au/</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q5376876</td><td>EnergyAustralia</td><td>Australia</td><td>https://www.energyaustralia.com.au/</td><td>Australian energy company</td></tr><tr><td>http://www.wikidata.org/entity/Q847931</td><td>Origin Energy</td><td>Australia</td><td>https://www.originenergy.com.au</td><td>Australian energy company, selling gas and electricity supply</td></tr><tr><td>http://www.wikidata.org/entity/Q7122497</td><td>Pacific Blue</td><td>Australia</td><td>https://www.pacificblue.com.au/</td><td>Chinese-owned renewable energy company headquartered in Melbourne, Australia</td></tr><tr><td>http://www.wikidata.org/entity/Q7520994</td><td>Simply Energy</td><td>Australia</td><td>https://engie.com.au/</td><td>Australian electricity and natural gas company</td></tr><tr><td>http://www.wikidata.org/entity/Q7548740</td><td>Snowy Hydro</td><td>Australia</td><td>https://www.snowyhydro.com.au/</td><td>electricity generating company owned by the states and Commonwealth of Australia</td></tr><tr><td>http://www.wikidata.org/entity/Q306740</td><td>Österreichs E-Wirtschaft</td><td>Austria</td><td>http://oesterreichsenergie.at/</td><td>advocacy group in Austria</td></tr><tr><td>http://www.wikidata.org/entity/Q6467328</td><td>Laborelec</td><td>Belgium</td><td>http://www.laborelec.com/</td><td>Belgian enterprise</td></tr><tr><td>http://www.wikidata.org/entity/Q9555634</td><td>AES Tietê</td><td>Brazil</td><td>http://www.aestiete.com.br/</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q13636760</td><td>Hrvatska elektroprivreda</td><td>Croatia</td><td>http://www.hep.hr/</td><td>national power company in Croatia</td></tr><tr><td>http://www.wikidata.org/entity/Q67810270</td><td>CARTHAMUS</td><td>Czech Republic</td><td>https://www.carthamus.cz/</td><td>Czech company</td></tr><tr><td>http://www.wikidata.org/entity/Q134305926</td><td>Elektrárna Dukovany II</td><td>Czech Republic</td><td>https://www.cez.cz/cs/o-cez/skupina-cez/vyznamne-spolecnosti-skupiny-cez/elektrarna-dukovany-ii</td><td>Czech company</td></tr><tr><td>http://www.wikidata.org/entity/Q58567679</td><td>Teplárna Strakonice, a.s.</td><td>Czech Republic</td><td>http://www.tst.cz</td><td>Czech company</td></tr><tr><td>http://www.wikidata.org/entity/Q23045237</td><td>Nivos Energy</td><td>Finland</td><td>https://www.nivos.fi/</td><td>Finnish energy company</td></tr><tr><td>http://www.wikidata.org/entity/Q116437045</td><td>Solarigo Oy</td><td>Finland</td><td>https://www.solarigo.fi/</td><td>Finnish electric power company</td></tr><tr><td>http://www.wikidata.org/entity/Q116437045</td><td>Solarigo Oy</td><td>Finland</td><td>https://www.solarigo.com/</td><td>Finnish electric power company</td></tr><tr><td>http://www.wikidata.org/entity/Q116435586</td><td>Solarigo Systems Oy</td><td>Finland</td><td>https://www.solarigo.fi/</td><td>Finnish designer, provider and operator of photovoltaic power systems</td></tr><tr><td>http://www.wikidata.org/entity/Q116435586</td><td>Solarigo Systems Oy</td><td>Finland</td><td>https://www.solarigo.com/</td><td>Finnish designer, provider and operator of photovoltaic power systems</td></tr><tr><td>http://www.wikidata.org/entity/Q101520653</td><td>East Prussian Power Company</td><td>German Reich</td><td></td><td>German enterprise</td></tr><tr><td>http://www.wikidata.org/entity/Q16943596</td><td>Kesco</td><td>India</td><td>https://kesco.co.in/</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q3805077</td><td>Electric Power Development Company</td><td>Japan</td><td>https://www.jpower.co.jp/</td><td>Japanese company</td></tr><tr><td>http://www.wikidata.org/entity/Q88941917</td><td>TEPCO Renewable Power</td><td>Japan</td><td>https://www.tepco.co.jp/rp/</td><td>Japanese energy company</td></tr><tr><td>http://www.wikidata.org/entity/Q1525124</td><td>Kenya Electricity Generating Company</td><td>Kenya</td><td>http://www.kengen.co.ke/</td><td>Energy company in Kenya</td></tr><tr><td>http://www.wikidata.org/entity/Q1584297</td><td>Tenaga Nasional</td><td>Malaysia</td><td>https://www.tnb.com.my/</td><td>Malaysian electricity company</td></tr><tr><td>http://www.wikidata.org/entity/Q126405534</td><td>City Charging</td><td>Netherlands</td><td>https://citycharging.nl/</td><td>Dutch car charging company</td></tr><tr><td>http://www.wikidata.org/entity/Q4700651</td><td>Akershus Energi</td><td>Norway</td><td>http://www.akershusenergi.no</td><td>Norwegian power company that produces hydroelectricity</td></tr><tr><td>http://www.wikidata.org/entity/Q4807253</td><td>Askøy Energi</td><td>Norway</td><td>http://www.askoy-energi.no</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q4937054</td><td>Bodø Energi</td><td>Norway</td><td>https://bodoenergi.no/</td><td>electricity company in Norway</td></tr><tr><td>http://www.wikidata.org/entity/Q4891601</td><td>Eviny</td><td>Norway</td><td>https://www.eviny.no/</td><td>Norwegian power company based in Bergen</td></tr><tr><td>http://www.wikidata.org/entity/Q5438258</td><td>Fauske Lysverk</td><td>Norway</td><td>http://www.flv.no</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q5499570</td><td>Fredrikstad Energi</td><td>Norway</td><td>https://fredrikstadenergi.no/</td><td>Norwegian power company</td></tr><tr><td>http://www.wikidata.org/entity/Q5321386</td><td>Hafslund Kraft</td><td>Norway</td><td>https://www.hafslund.no</td><td>Norwegian electric power company</td></tr><tr><td>http://www.wikidata.org/entity/Q5321386</td><td>Hafslund Kraft</td><td>Norway</td><td>https://hafslund.no/en</td><td>Norwegian electric power company</td></tr><tr><td>http://www.wikidata.org/entity/Q117833084</td><td>Hardanger Energi</td><td>Norway</td><td>https://www.hardangerenergi.no/</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q11974449</td><td>Haugaland Kraft</td><td>Norway</td><td>https://hkraft.no</td><td>Norwegian energy company</td></tr><tr><td>http://www.wikidata.org/entity/Q6028100</td><td>Industrikraft Midt-Norge</td><td>Norway</td><td>http://www.industrikraft.no/</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q6088497</td><td>Istad</td><td>Norway</td><td>http://www.istad.no</td><td>Istad AS is a power company based in the town of Molde in Møre og Romsdal county, Norway.</td></tr><tr><td>http://www.wikidata.org/entity/Q7050849</td><td>NEAS</td><td>Norway</td><td>https://www.neas.mr.no/</td><td>power company based in Kristiansund, Norway</td></tr><tr><td>http://www.wikidata.org/entity/Q6981005</td><td>Naturkraft</td><td>Norway</td><td></td><td>Naturkraft is a Norwegian power company that operates one natural gas powered thermal power station located at Kårstø.</td></tr><tr><td>http://www.wikidata.org/entity/Q7050523</td><td>Nord-Trøndelag Elektrisitetsverk</td><td>Norway</td><td>https://nte.no/</td><td>power company serving Nord-Trøndelag in Norway</td></tr><tr><td>http://www.wikidata.org/entity/Q7391964</td><td>SN Power</td><td>Norway</td><td>http://www.snpower.com/</td><td>defunct company</td></tr><tr><td>http://www.wikidata.org/entity/Q7406074</td><td>Salten Kraftsamband</td><td>Norway</td><td>http://www.sks.no</td><td>Norwegian HPS company</td></tr><tr><td>http://www.wikidata.org/entity/Q7533726</td><td>Skagerak Energi</td><td>Norway</td><td>http://www.skagerakenergi.no/</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q7554545</td><td>Sognekraft</td><td>Norway</td><td>http://www.sognekraft.no</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q7845389</td><td>Troms Kraft</td><td>Norway</td><td>http://www.tromskraft.no</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q7849188</td><td>TrønderEnergi</td><td>Norway</td><td>https://tronderenergi.no/</td><td>power company serving Sør-Trøndelag in Norway</td></tr><tr><td>http://www.wikidata.org/entity/Q7915448</td><td>Varanger Kraft</td><td>Norway</td><td>https://varangerkraft.no</td><td>power company in Norway</td></tr><tr><td>http://www.wikidata.org/entity/Q4355084</td><td>Å Energi</td><td>Norway</td><td>https://www.aenergi.no/</td><td>Norwegian energy company</td></tr><tr><td>http://www.wikidata.org/entity/Q4580656</td><td>Østfold Energi</td><td>Norway</td><td>https://ostfoldenergi.no</td><td>Norweigan energy producer</td></tr><tr><td>http://www.wikidata.org/entity/Q28223503</td><td>Islamabad Electric Supply Company</td><td>Pakistan</td><td>https://www.iesco.com.pk/</td><td>Pakistani public utility</td></tr><tr><td>http://www.wikidata.org/entity/Q113882432</td><td>Cabanatuan Electric Corporation</td><td>Philippines</td><td>https://celcor.com.ph/</td><td>electric company based in Cabanatuan City</td></tr><tr><td>http://www.wikidata.org/entity/Q5175263</td><td>Cotabato Light and Power Company</td><td>Philippines</td><td>https://www.cotabatolight.com/</td><td>electric company based in Cotabato City, Philippines</td></tr><tr><td>http://www.wikidata.org/entity/Q5228152</td><td>Davao Light and Power Company</td><td>Philippines</td><td>https://davaolight.com</td><td>electric company based in Davao City, Philippines</td></tr><tr><td>http://www.wikidata.org/entity/Q6817918</td><td>Meralco</td><td>Philippines</td><td>https://www.meralco.com.ph</td><td>Philippine electric company</td></tr><tr><td>http://www.wikidata.org/entity/Q7935617</td><td>Visayan Electric Company</td><td>Philippines</td><td>https://visayanelectric.com/</td><td>power distribution utility in the Philippines</td></tr><tr><td>http://www.wikidata.org/entity/Q8062935</td><td>Zamboanga City Electric Cooperative</td><td>Philippines</td><td>https://www.zamcelco.com.ph</td><td>electric cooperative in Zamboanga City, Philippines</td></tr><tr><td>http://www.wikidata.org/entity/Q86664251</td><td>City Power</td><td>South Africa</td><td>https://www.citypower.co.za</td><td>Regional, municipal electricity utility in Johannesburg, South Africa</td></tr><tr><td>http://www.wikidata.org/entity/Q6431646</td><td>Korea Hydro &amp; Nuclear Power</td><td>South Korea</td><td>https://www.khnp.co.kr/eng/</td><td>energy company in South Korea</td></tr><tr><td>http://www.wikidata.org/entity/Q6431646</td><td>Korea Hydro &amp; Nuclear Power</td><td>South Korea</td><td>http://www.khnp.co.kr/</td><td>energy company in South Korea</td></tr><tr><td>http://www.wikidata.org/entity/Q63533453</td><td>Unión Fenosa Distribución</td><td>Spain</td><td></td><td>electric grid provider in Spain</td></tr><tr><td>http://www.wikidata.org/entity/Q49094894</td><td>Godel</td><td>Sweden</td><td></td><td>Swedish power company</td></tr><tr><td>http://www.wikidata.org/entity/Q17151766</td><td>Chiahui Power Corporation</td><td>Taiwan</td><td></td><td>independent power producer of Taiwan</td></tr><tr><td>http://www.wikidata.org/entity/Q16241616</td><td>Ever Power IPP Co., Ltd.</td><td>Taiwan</td><td>http://www.everpoweripp.com.tw</td><td>independent power producer of Taiwan</td></tr><tr><td>http://www.wikidata.org/entity/Q17005109</td><td>Hsin Tao Power Corporation</td><td>Taiwan</td><td></td><td>an independent power producer company in Taiwan</td></tr><tr><td>http://www.wikidata.org/entity/Q4875034</td><td>Baywind Energy Co-operative</td><td>United Kingdom</td><td>http://www.baywind.coop</td><td>wind power generating co-operative</td></tr><tr><td>http://www.wikidata.org/entity/Q16971845</td><td>Brighton Energy Co-operative</td><td>United Kingdom</td><td>http://www.brightonenergy.org.uk/</td><td>co-operative renewable energy producer</td></tr><tr><td>http://www.wikidata.org/entity/Q1256028</td><td>Drax Group</td><td>United Kingdom</td><td>http://www.draxgroup.plc.uk</td><td>power generation business</td></tr><tr><td>http://www.wikidata.org/entity/Q5205934</td><td>AES Ohio</td><td>United States</td><td>https://www.aes-ohio.com/</td><td>subsidiary of AES Corporation serving Ohio, United States</td></tr><tr><td>http://www.wikidata.org/entity/Q4852862</td><td>Baltimore Gas and Electric</td><td>United States</td><td>https://www.bge.com</td><td>gas and electric utility</td></tr><tr><td>http://www.wikidata.org/entity/Q5012733</td><td>CLECO</td><td>United States</td><td>http://www.Cleco.com</td><td>electric power company headquartered in Pineville, Louisiana, United States</td></tr><tr><td>http://www.wikidata.org/entity/Q18355653</td><td>Florida Municipal Electric Association</td><td>United States</td><td>http://www.publicpower.com</td><td></td></tr><tr><td>http://www.wikidata.org/entity/Q2045479</td><td>PacifiCorp</td><td>United States</td><td>http://www.pacificorp.com</td><td>electric power company in the western United States</td></tr><tr><td>http://www.wikidata.org/entity/Q117074748</td><td>Union Electric Power Company</td><td>United States</td><td></td><td>former electric utility in Illinois, United States</td></tr><tr><td>http://www.wikidata.org/entity/Q8039462</td><td>Wyandotte Municipal Services</td><td>United States</td><td>http://www.wyan.org/</td><td>not-for-profit service provider in Michigan</td></tr><tr><td>http://www.wikidata.org/entity/Q10831591</td><td>Vietnam Rubber Group</td><td>Vietnam</td><td>https://rubbergroup.vn</td><td>manufacturing company of Vietnam</td></tr></tbody></table></body></html>
