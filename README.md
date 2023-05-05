# GeoSPARQL Data
https://opengeospatial.github.io/ogc-geosparql/geosparql11/spec.html

https://github.com/opengeospatial/ogc-geosparql

Demo-dataset:
https://github.com/opengeospatial/ogc-geosparql/blob/master/1.1/examples/demo-dataset.ttl

## Triple Store

I am using GraphDB 10.2 in a Docker image:

`docker pull khaller/graphdb-free:10.2.0`

The GraphDB GeoSPARQL plugin has been activated using:
```
PREFIX geoSparql: <http://www.ontotext.com/plugins/geosparql#>
INSERT DATA { [] geoSparql:enabled "true" . }
```

## Quartiers in Laval 
Data from https://www.donneesquebec.ca/recherche/dataset/limites-des-anciennes-municipalites


## Use Case
The data from the old municipal regions in Laval is to be used to group events by region.  To know which event is in which region by using the longitude and latitude of the event's venue.

Example: I would like find the region of the event venue Église St-Jean-Gualbert with coordinates 45.5242132,-73.885465.  My query would look something like this:

```
PREFIX geo: <http://www.opengis.net/ont/geosparql#>
PREFIX geof: <http://www.opengis.net/def/function/geosparql/>
PREFIX adr: <http://kg.artsdata.ca/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
SELECT *
WHERE {
  ?region a geo:Feature ; rdfs:label ?name .
  ?region geo:hasGeometry ?geo .
  ?geo geo:sfContains '''
        <http://www.opengis.net/def/crs/OGC/1.3/CRS84>
            Point (-73.885465 45.5242132) 
        '''^^geo:wktLiteral .
}
```

When I load the turtle file with the 2 regions in Laval and try this SPARQL it does not work.

Can you figure out how to make this work?
