# publish-find-bind
De functionale API voor het vinden van datasets en dataservices met een keuze voor welke catalogus en welke zoekterm.
Beschikbaar als OpenApi YAML specificatie met een aanroep naar een end-point waarin de logica ingevuld is met nodered. 

Het endpoint is: https://client.data-ambassade.nl/product/pfb

Voorbeeld van een aanroep: 
https://client.data-ambassade.nl/product/pfb?catalogus="open data rotterdam"&zoekterm=TIR

De werking van de nodered flow is onderstaand weergegeven. De aanroep komt links binnen op de http node en wordt vervolgens via een switch naar de specifieke catalogus geleid. Daar wordt met de API van de applicatie een zoekopdracht uitgevoerd. Uit het resultaat worden de velden gehaald die met de url die verwijst naar de daadwerkelijke databron. Resultaat gaat als JSON terug.

De opties voor de te kiezen catalogus zijn in de node 'catalogus' zichtbaar. 

<img width="1031" alt="image" src="https://github.com/data-ambassade/publish-find-bind/assets/66671799/cf9fcef7-5c98-41a8-9fa2-e76bd81aef42">

<img width="502" alt="image" src="https://github.com/data-ambassade/publish-find-bind/assets/66671799/2d55b12d-551f-4844-93c9-a06d3735d51f">
