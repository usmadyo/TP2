**RSQA - Indice de la qualité de l’air (IQA)**

****

Étape 1  Importation (lecture URL) et nettoyage de toutes les données

****

- Ajouter les 3 fichiers Excel suivants avec un CSV READER

****

IQA détaillé par station en temps réel (Quotidien) - <https://donnees.montreal.ca/dataset/3e9f7b96-3f25-4404-a5ad-22d9a31060e6/resource/a25fdea2-7e86-42ac-8301-ca77db3ff17e/download/rsqa-indice-qualite-air.csv>

****

IQA par station en temps réel (Quotidien) - 

<https://donnees.montreal.ca/dataset/3e9f7b96-3f25-4404-a5ad-22d9a31060e6/resource/ccd5a4b7-cbca-4f5f-a746-ad8c576af374/download/rsqa-indice-qualite-air-station.csv>

****

IQA par secteur en temps réel (Quotidien) - 

<https://donnees.montreal.ca/dataset/3e9f7b96-3f25-4404-a5ad-22d9a31060e6/resource/9c7434e9-f5af-4154-991c-293fbd5cb626/download/rsqa-indice-qualite-air-secteur.csv>

****

RSQA - Secteurs géographiques en format GEOJSON avec un _GEOJSON READER -_ 

<https://donnees.montreal.ca/dataset/ab112a84-0661-4360-9573-652eed16beeb/resource/a90678ac-7ea7-464c-b615-e8f5cb9f527b/download/rsqa_secteurs.geojson>

Îlots de chaleur 2016 (images aéroportées) en format GEOTIFF (ou GEOJSON) avec un _GEOTIFF READER -_ <https://donnees.montreal.ca/dataset/dbdfbdba-0725-470d-a23e-da69dbedc4e6/resource/b8aff0f2-2c7b-48f5-b937-2aef5d253e22/download/ilots-de-chaleur-2016.zip>

Ortho mosaïque 2022 pour l’île de Montréal au complet en utilisant le lien suivant avec un _WMS READER -_ [_http://sirius/erdas-iws/ogc/wms/?_](http://sirius/erdas-iws/ogc/wms/?)

Bâtiments 2D 2016 - Tous les arrondissements (COTE et TOIT) en format Shapefile avec un _ESRI SHAPEFILE READER -_ [https://donnees.montreal.ca/dataset/fab160ae-c81d-46f8-8f92-4a01c10d4390/resource/183866d5-9027-456a-b0af-36b2e45c8aac/download/batiments\_2d\_2016\_arrondissements.zip __](https://donnees.montreal.ca/dataset/fab160ae-c81d-46f8-8f92-4a01c10d4390/resource/183866d5-9027-456a-b0af-36b2e45c8aac/download/batiments_2d_2016_arrondissements.zip)

Canopée 2019 (données vectorielles avec une variable 3D) avec un _GEOJSON READER -_ <https://donnees.montreal.ca/dataset/36f48854-474b-43d2-a16d-a433da8a1447/resource/77e44cc1-56b1-4e83-871d-e3990565563f/download/canopee-2019.zip>

Nuage de points Lidar en format. Laz pour la station 55 avec _LAS READER -_ <http://depot.ville.montreal.qc.ca/geomatique/lidar_aerien/2015/299-5056_2015.laz>

****

Étape 2 Reprojection vers le EPSG:3857 avec Reprojector ou EsriReprojector

****

![](https://lh7-us.googleusercontent.com/Xi6GilID9fpfJ_QryL7kEWbu6HE62uQOHYdwU4KIynBiXOX1UmxtLHb59TZoEf17j4C4bJ7WW--j9Gew3tLg4m-KcaOsIsvsm6ovXjkreZgE-lZeKJjlpxsYmHRUb7zIm40aWo0UYzpmwJHI_oCfEDc)

****

![](https://lh7-us.googleusercontent.com/qHN4fawGKfbcNVBUqb57n7KeKaJ_QJIMj_-DFqxYF06uh1P9JfCTkQAgHAsR2hWCbianfwB07LcRfRu6L-N2X93LzSWrzfK3IMRJHXkD8KwpQTgrECVNMXjrWjK4SYrFq9YOneS4U4ul7_TirV5FvvU)

****

Étape 3 Traitement sur les données reprojectées

Étape 4 Publication vers PostgreSQL (PostGIS ou PostGIS Raster)

****

1. Pour les IQA et secteurs géographiques

****

- **Pour les IQA par station en temps réel (Quotidien)**, ajouter un _AttributeManager_ (facultatif) pour faire un peu de ménage; 

- Ajouter un _AttributeRangeMapper_ pour catégoriser les valeurs en trois catégories (selon les informations données par la Ville de Montréal;

- Ensuite publier avec un _Writer_ PostGIS (Table Qualifier KA791969).

****

![](https://lh7-us.googleusercontent.com/yjl8XceZgL2vG9ehBLrC08ioS6FV-xHHQNg2kR4Qd5-k2FBMWD_7TLQV1_WSjG7etDqMN31aJIi3AwV3ID0bmVwnsagAkmaun3zi2UHTZZspyR874Cnc7bhlE4cspp_u6zaIfjbmXrWZtwLGUqBnnuY)

****

- **Pour les IQA détaillé par station en temps réel (Quotidien)**, ajouter un _FeatureMerger_ pour ajouter la géométrie (coordonnées) du IQA par station en temps réel (Quotidien). Cette étape doit être faite avant _Reprojetor;_

__![](https://lh7-us.googleusercontent.com/kU3h6--arAzV5OUIlyj3oAOv6sWwQimmz0fhqlLTFwINBtkcVVZwBPLSw7V-otm1V09NY-fFmcnHnBaBTayJyq0tzMTfACife7dK50HVB8dliHn4MKGwEGXYVQymKaEkPr9AwTeBbH4fzqs05W9om6U)__

__![](https://lh7-us.googleusercontent.com/3kp5wjZvAa0A_PSKAQAKKm-vL8EzXtBtMp9bnGdOfZG_-OkAwi2WVHV2exfLUlBklAfZsEzTbYWYIXb0w7tPWmu8fGZ5_izxFdox_DZyQshV4doF9glp3p2GBwTc_F2jJWj49KL_sRuUevPzwNlqsew)__

****

- Ajouter un _AttributeManager_ (facultatif) pour faire un peu de ménage;

- Ajouter un _AttributeRangeMapper_ avec les mêmes paramètres; 

- Ensuite publier avec un _Writer_ PostGIS (Table Qualifier KA791969).

- **Pour les secteurs géographiques**, ajouter un FeatureMerger pour combiner avec les IQA par secteur en temps réel (Quotidien). Cette étape doit être faite avant _Reprojetor_. 

- Ajouter un _AttributeManager_ (pour nettoyer les colonnes au besoin). 

- Ajouter un _AttributeFilter_ pour filtrer les secteurs __et des _StatisticsCalculator_ pour calculer l’IQA maximale par secteur.

- Ajouter un _AttributeRangeMapper_ avec les mêmes paramètres que les autres utilisés auparavant.

- Ensuite publier avec un _Writer_ PostGIS (Table Qualifier KA791969)

**![](https://lh7-us.googleusercontent.com/mt2S3XLDZLBdqRN1Kfbb_AtEpwKJtuKLJcxIPuah8pG4fo2JHj6xIc67do3qaw9DFJJ5EbF9UwssA2za3KngMT80wo0oDioOmO94zhyOPS-FTwTBYl-mcphtlb0V1-zwUxGceqeSv7I29rEEvCIcyYg)**

![](https://lh7-us.googleusercontent.com/F2z41BDa48-yAB2zhAN8iLA0FvyR7qVScdqalkcUQfnJph6zYxgdRMkE4ow8A0UGRO1VH-wrqmUtKHIDPeFgrUUFoWXrNdmlB_Yh9uHqMoos-nVCfDiiVHsJDLKyjDuqmC7gVlsEc6PvLe-8TKazqHY)

****

- **Pour l’ortho mosaïque 2022**, ajouter un reader WMS, _Reprojecter_ et publier avec _PostGIS Raster_ (Table Qualifier KA791969).

- **Pour les bâtiments 2D**, ajouter les shapefiles avec un _Esri Shapefile reader_ (sélectionner seulement COTE et TOIT). Ensuite _Reprojector_ et publier avec PostGIS (Table Qualifier KA791969).

- **Pour la canopée 2019** (Données vectorielles avec une variable 3D), ajouter les données avec un _GEOJSON Reader._ Ensuite, __utiliser un _ESRI Reprojector_ (important) pour aller vers EPSG::3857 __et publier avec PostGIS (Table Qualifier KA791969).

- **Pour les îlots de chaleur 2016**, ajouter le raster avec un _GEOTIFF Reader,_ Ensuite, __utiliser un _Reprojector_;

- Ajouter un _RasterToPolygonCoercer_ (_Label_ = classification). Puis, publier avec un _PostGIS Writer_;

![](https://lh7-us.googleusercontent.com/0d-Ab6cUqpcf9QlOghLrG7yiGNl1UQDENmQyenHZNSZxo2i5a5h2KJEIlL-d07zTCxHek-SVF8BX5lJ3uN2AdrdwVDOtcXreBcTnL9N_Z0SpaaCPIeomPCKnp2JGUS2ZCz6ecFxlGI5qR0VJ9GjvTI4)

****

- Ajouter ensuite un Raster Sharpener (lier avec la donnée reprojectée), ensuite un _RasterCellValueRounder_ et un _RasterToPolygonCoercer (label = classification)_. Laisses les paramètres par défaut pour ces transformateurs.Puis, publier avec un _PostGIS Writer._

![](https://lh7-us.googleusercontent.com/Fnu0sLnam8shj8e9Lvi0_Bo5jAM9q2bkWQzXvvObTEE-gzSj00h1ybTeS_hb5bt6XrbWCX2u6PLvVd4Eq6jl7q4eBVMur2TAKPPS31ovuIXZCAF2qgR15JekYqdP7WZRcbyfGt_ExJxnf4jyBewMiT0)

- Ajouter _RasterCellCoercer (Extract Band Values As = Z values)._ Puis publier les îlots de chaleur en points  avec un _PostGIS Writer_ (Table Qualifier KA791969). 

- Visualisation QGIS

![](https://lh7-us.googleusercontent.com/9VCM7bFxu8Wwz0D1VstGmEbTMnvk8xrIQGF386AwDWMyefG_M20qt5jbYJHHYaouGac5Q3qeLBdMrySpaIcKhfxWvsK_u-ug1_mQ-Qk2WE4bCWQZgN_qEfScyMQcV06fTMpexeZBWQPI9xxakq_tWic)

- **Pour les données LIDAR 2015**, ajouter un _LAS Reader_ pour lire le nuage de points de la station #55;

- Ajouter un _PointCloudThinner transformer_ (interval =  30), Ensuite, _Esri Reprojector. Puis un autre PointCloudThinner transformer_ (interval =  5);

- Ajouter un _PointCloudPropretyExtractor_ et un _attributeManager;_

- Ajouter un _PointCloudstatsRasterizer_ pour transformer le _point cloud to raster avec de publier avec un PostGIS Raster Writer_ (Table Qualifier KA791969).   

![](https://lh7-us.googleusercontent.com/9qh7ywj5lich-oa7iv-Dq3Nrx87hm__BZafUsolg2_VJnLYr8wAT-rNSoprMbzdR60NYronR2TMxulRh9q9HtuzVgidTTF-UNeVxW7_hvMAF01Bn5dRzXn_-bYoAl3_8Jg_epJuvbypKZgboefe5k1Q)

****

**Visualisation QGIS**

****

****![](https://lh7-us.googleusercontent.com/XlJNsVp_0xbMRJ4r5aHa8b7sNlitc-F3QkVtzI2VphGispvmHtuVJFNGp7Xeazo7AMIzrZvwBOfZ5U3FeRzwits-8HRVuRK0MwYHUBfaSy03Elu_Io8FNP-ml9C4scM6OjYZ48lMkM51gpRRUhAPAn4)****

**Prochaine étape : publication vers ArcGIS Online (AGOL) pour créer un tableau de bord (service web) avec _Dashboard_ ou avec _Experience Builder_.__** 
