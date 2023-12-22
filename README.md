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

De OpenApi kan je direct aanroepen, bijvoorbeeld via Swagger (gebruik data-ambassade account van github). 
https://app.swaggerhub.com/apis/Data-Ambassade9/publish-find_bind/v1#/default/get_product_pfb

De OpenApi is tevens ontsloten als GraphQL endpoint via Wundergraph. Met Wundergraph kan je meerdere technische API's publiceren als GraphQL endpoint. Te bereiken via: https://scaapidata.scamanderhost.com/graphql

Daarin kan je deze query uitproberen waarbij je een dataset zoekt in de catalogus van het Open Urban Platform.

\query publish_find_bind ($catalogus: String!, $zoekterm: String!) {
  product_pfb_getProductPfb(catalogus: $catalogus, zoekterm: $zoekterm) {
    catalog
    title
    description
    accessurl
    format
  }
}\

Met als variabelen:

\{
  "catalogus": "oup.rotterdam.nl",
  "zoekterm": "drinkwater"
}\


## Qgis plugin.

In Qgis kan je een zogenaamde plug-in installeren. Installeer via het menu 'Plugins' van Qgis de CKAN plug-in en configureer deze zodanig dat je daarmee een eigen catalogus kan aanroepen in plaats van een CKAN catalogus. 

<img width="563" alt="image" src="https://github.com/data-ambassade/publish-find-bind/assets/66671799/63b7377e-3636-436e-aa43-c68c25e2f93b">

Open via het menu van de Plugins de CKAN browser en kies 'Select CKAN server'.

<img width="808" alt="image" src="https://github.com/data-ambassade/publish-find-bind/assets/66671799/3ad678dc-4a12-46e4-86a5-02065e647ccf">

Maak hierin twee nieuwe verwijzingen aan ('Add CKAN server to list') voor het aanroepen van 
- het open data portaal (data.rotterdam.nl): https://client.data-ambassade.nl/opendatarotterdam/api/3
- het Open Urban Platform: https://client.data-ambassade.nl/oup/api/3

Druk op Test om te kijken of ze werken. Selecteer het open data portaal van Rotteram. En daarna onderaan op Save om de instelling te bewaren.

Dit is het resultaat bijvoorbeeld bij het zoeken op TIR in het opendata portaal van Rotterdam
<img width="803" alt="image" src="https://github.com/data-ambassade/publish-find-bind/assets/66671799/194bf833-d9cb-4781-9eb7-d5c49c171eca">
