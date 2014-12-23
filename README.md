risicokaart
===========


risicokaart.nl maar dan toegankelijk en met oog voor privacy...

[risicokaart.nl](http://risicokaart.nl) maakt gebruik van Google maps in plaats van de door de Rijksoverheid opgetuigde PDOK infrastuctuur, [Google is recentelijk op de vingers getikt](https://www.bof.nl/2013/11/28/google-beslissing-cbp-vaag-privacybeleid-niet-voldoende/) vanwege het niet naleven van de Nederlands wetgeving met betrekking tot bescherming van persoonsgegevens. Overigens zet risicokaart.nl ook tracking cookies in zonder daar toestemming voor te vragen.
risicokaart.nl negeert de [open standaarden zoals die zijn voorgeschreven voor de overheid](https://lijsten.forumstandaardisatie.nl/) en geeft daar ook geen uitleg over. Al met al geen beste beurt voor een [overheids website](http://www.infomil.nl/onderwerpen/hinder-gezondheid/veiligheid/register-en/).

Deze applicatie is gebouwd met [CBSviewer](https://github.com/MinELenI/CBSviewer), een project om een generieke toegankelijke kaart viewer te bouwen.

~~Een live (beta) preview is tijdelijk beschikbaar op een [demonstratie server](http://gisdemo.agro.nl/risicokaart/) om te laten zien hoe het beter kan.~~

![logo](http://staff.washington.edu/tft/a11ylogo/images/a11ylogo150.png)

[![Stories in Ready](https://badge.waffle.io/GeoDienstenCentrum/risicokaart.png?label=ready)](http://waffle.io/GeoDienstenCentrum/risicokaart)

## bouwen en draaien

Om de risicokaart webapp te draaien/bouwen moet je eerst even de [CBSviewer webapp](https://github.com/GeoDienstenCentrum/CBSviewer) bouwen omdat dit de basis is; er is een [uitgebreide handleiding]( https://mineleni.github.io/CBSviewer/ontwikkelhandleiding.html) beschikbaar. Daat staat ook de toolchain beschreven, in essentie git, phantomjs en Maven 3.

De essentie is van het bouwproces is:
```
git clone https://github.com/MinELenI/CBSviewer.git CBSviewer
cd CBSviewer
mvn -Popenlayers,developer install
```

Mogelijk moet je in de web.xml nog de WMS service endpoint van de achtergrondkaart aanpassen (de pdok achtergrond wms is alleen voor selecte afnemers) er staat een voorbeeld in voor de WhereGroup WMS, maar je kunt ook openbasiskaart gebruiken (zoals te zien is in https://github.com/MinELenI/NOKviewer/blob/master/src/main/webapp/WEB-INF/web.xml)

Vervolgens de code van de risicokaart webapp uitpakken en bouwen:

```
git clone https://github.com/GeoDienstenCentrum/risicokaart.git risicokaart
cd risicokaart
mvn install
```

Ook hier voor het bouwen mogelijk eerst de brtachtergrondkaar wms omhangen naar iets anders. de .war in de target directory kun je zo in een tomcat 7 droppen.

met een commando als:

`mvn -Dhttp.proxyHost=wpad.agro.nl -Dhttp.proxyPort=8080 -Pdeveloper -Ddebug=true jetty:run`

wordt een lokale webserver gestart voor http://localhost:8020/

_De app crashed momenteel op het onbreken van de url http://nederland.deegree.risicokaart.nl/ogc_wms_wfs/services?REQUEST=GetCapabilities&VERSION=1.3.0&SERVICE=WMS die moet ook aangepast in de web.xml_


