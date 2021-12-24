# Trentino territory

This page aims to describe a bit the process used for the development of the project "Trentino Territory" for the course "Knowledge and data integration" 2021/2022 of the University of Trento. In this page you can find all the links to the resources used for the development, and also the link to the report of the project.

## Project purpose
The purpose of our project is the development of an application that provides natural places in function of their category, name or location. The application will provide some information as name, description, category, company, location. With the usage of third-party services, the application will also be capable of calculating a route to arrive at the attraction from the user's position. It will be possible to order the results by distance or name. The application will also suggest some interesting activities or places near the point of interest (for example a "malga" in the mountain where the user wants to hike).

## Datasets
For the data collection we searched for different datasets in Open Data Trentino and on the web. Our criteria was to find datasets containing some of the categories from the CQ. 

It has not been easy to find many datasets, because the information about naturalistic places are not as many as for example restaurants and similar point of interest.
Talking about the different datasets listed in the previous chapter, we found out that the JSON file (Trentino) is well structured and has a lot of information, but it does not contain many objects (145) which match  interesting categories  (for example: 'rifugio','attrazione naturale'...).

For the csv files, each one of them has been defined by a commune, the information that they contain are good for our purpose. Most of them share the same schema. The problem we encountered with these datasets is that some of them have different schema, some have also missing fields in some objects or are encoded in a different way, making it difficult to integrate the data from these different datasets. 

The last JSON (Valsugana) has the same structure as the first JSON (trentino) but it seems to have data that are present also in the other JSON file, we are keeping it for now, but it could be useless if it does not contain any more information than the other datasets.

One weakness of this process is the number of different datasets that we collected, like said before it is difficult to find information about naturalistic point of interest. From the datasets collected we can find almost all the core information that we need, but for some objects, contextual categories are missing  (many are blank).

The links are the following:
Trentino-JSON: https://dati.trentino.it/en_GB/dataset/punti-di-interesse-del-trentino

CSV:https://dati.trentino.it/en_GB/dataset?tags=luoghi+e+punti+di+interesse

Valsugana-JSON:https://dati.trentino.it/en_GB/dataset/punti-di-interesse-valsugana

## Reference schemas
We chose the schema Place and its children because  they are used in the geospace domain. Place has a lot of categories which feats our needs like address, latitude, longitude, telephone number…. The other schemas have these properties but also other one like touristType or openingHours which could be needed for our database.
Landform and LandmarksOrHistoricalBuildings don't have any other properties but could be still interesting since they inherited from Place and are linked to our DoI. 
We also added a schema called organization, because we think that splitting the database in two tables, one for the point of interest and the other one for organizations, could be a good idea. Using this schema, we could add other useful information like the email or the name of the company, but for now  we are not certain of this.

The links are the following:
Place:https://schema.org/Place

TouristicDestination:https://schema.org/TouristDestination

TouristicAttraction:https://schema.org/TouristAttraction

LandmarksOrHistoricalBuildings:https://schema.org/LandmarksOrHistoricalBuildings

CivicStructure:https://schema.org/CivicStructure

Landform:https://schema.org/Landform

Organization:https://schema.org/Organization

## ETG
To create our ETG we used our ER MODEL and the software protégé to define for each class the object and data properties associated. During this process we also tried to modify the name of our data properties by the names inside of the ontology as much as we could and without modifying the meaning that we gave them. For example we modified website by url or PhoneNumber by telephone or CAP by postal code which comes from the schema PLACE which comes from our knowledge resources (look part 2.4). But we didn't modify location by geocoordinates because for us it's too precise and not clear. We did this because it improves the reusability and sharebility.

For our classes Attraction and Company we defined a new section called non living being which could be defined as things which are lifeless. In fact we thought that our classes were real kind but were not living being since we talk about places. 

For our object property "has company" we indicate that it is the inverse of "has attraction" so that from a company we can get all its attractions and from an attraction get its company.

For each classes that we have created we had to define it's data properties and the meanings of each data property (Language alignment) thanks to UKC.

The link to the ETG file is the following:
https://github.com/AndreFrigo/Trentino-territory/blob/main/Teleologies/Formal%20Modeling/ETG.owl

## KG
In the end we have 4 Etypes : company, attraction, location and address. In total we have 18 properties inside our KG.For company we have 243 entities, for attraction we have 956 entities, for location we have 505 entities, for address we have 221 entities.
We have 4 object properties: has_location, has_address, has_company and has_attraction. 

The link to the KG file is the following:
https://github.com/AndreFrigo/Trentino-territory/blob/main/Datasets/Data%20Integration/EG%20(RDF).rdf

## Project repository
The link to the project repository is the following:
https://github.com/AndreFrigo/Trentino-territory

In particular, the to the project report is:
https://github.com/AndreFrigo/Trentino-territory/blob/main/Documentation/Project%20Report.pdf
