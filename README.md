# Megàlits del massís de les Gavarres
Pàgina web estàtica per visualitzar en un mapa diferents megàlits o dòlmens del massís de les Gavarres (Girona).


## Tecnologia utilitzada
- Leaflet.js
- Google Sheets API

La pàgina web utilitza la llibreria Leaflet.js per ubicar els marcadors al mapa segons la longitud i latitud. 

Les dades i algunes configuracions s'obtenen d'un fitxer [Google Sheets](https://docs.google.com/spreadsheets/d/1Rrh6RR9WYCzp7R3_ZSvWOFK1mARYhLokK6t8zVz8MEs/edit#gid=0) i mitjançant l'API es connecta al fitxer. 

## Dades dels megàlits i la seva ubicació
Les dades s'han obtingut mitjançant l'ús de tecnologia OCR per extreure el llistat de dòlmens de les Gavarres que es disposa aldocument "[Els Monuments Megalítics](https://issuu.com/ddgi/docs/monuments_megalitics)" de la Revista Quadern de Girona publicat per la Diputació de Girona l'any 1992.

|  Monument Megalític                                         | Municipi                                               |
|-------------------------------------------------------------|--------------------------------------------------------|
|  Menhir de Montagut (Traslladat la vila de Llagostera)      | Llagostera                                             |
|  Menhir de l'Avi                                            | Tossa de Mar                                           |
|  Menhir de Montllor                                         | Tossa de Mar                                           |
|  Menhir d'en Llach                                          | Llagostera                                             |
|  Menhir del Terme Gros                                      | Solius/ Santa Cristina d'Aro                           |
|  Menhir de Pedrafita                                        | Sta. Cristina d'Aro                                    |
|  Menhir de Can Llaurador                                    | Solius/ Santa Cristina d'Aro                           |
|  Menhir de la Ramera                                        | Santa Cristina d'Aro                                   |
|  Cista amb túmul del Suro del Rei                           | Romanyà de la Selva/ Santa Cristina d'Aro              |
|  Cista amb túmul del Bosc d'en Roquet                       |  Romanyà de la Selva/Santa Cristina d'Aro              |
|  Cista amb túmul de la Carretera de Calonge                 | Romanyà de la Selva/Santa Cristina d'Aro               |
|  Menhir de la Murtra                                        | Romanyà de la Selva/Santa Cristina d'Aro               |
|  Galeria catalana de les Pedres Dretes d'en Lloveres        | Santa Cristina d'Aro                                   |
|  Galeria catalana de la Cova d'en Daina                     | Romanyà de la Selva/Santa Cristina d'Aro               |
|  Cista amb túmul de la Finca d'en Guitó                     | Romanyà de la Selva/Santa Cristina d'Aro               |
|  Cista amb túmul del Puig d'Arques o de l'Abel              | Sant Sadurní de l'Heura                                |
|  Sepulcre de corredor del Mas Bou-serenys                   | Santa Cristina d'Aro                                   |
|  Galeria catalana del Puig d'Arques                         | Sant Cebrià dels Alls/ Camós de les Gavarres/ Cruïlles |
|  Galeria catalana del Dr Pericot                            | Fitor-Fonteta                                          |
|  Galeria catalana del Mas Estanyet                          | Fitor-Fonteta                                          |
|  Sepulcre de corredor de Serra Mitjana                      | Fitor-Fonteta                                          |
|  Sepulcre de corredor o galeria catalana  de la Vinya Gran  | Fitor-Fonteta                                          |
|  Sepulcre de corredor del Llobinar                          | Fitor-Fonteta                                          |
|  Galeria catalana d'en Botey                                | Fitor-Fonteta                                          |
|  Menhir de Cala Pedrosa                                     | Castell/Platja d'Aro                                   |
|  Galeria catalana dels Tres Caires                          | Fitor-Fonteta                                          |
|  Galeria catalana de la Roca de la Gla                      | Fitor-Fonteta                                          |
|  Menhir del Mas Ros                                         | Castell/Platja d'Aro                                   |
|  Menhir del Terme de Belliu                                 |  Castell/Platja d'Aro/ Calonge                         |
|  Menhir de Sa Pedra Aguda o de les Goges                    | Vallbanera/Castell/ Platja d'Aro                       |
|  Sepulcre de corredor o galeria catalana dels Tres Peus     | Fitor-Fonteta                                          |
|  Sepulcre de corredor del Puig ses Forques                  | Calonge                                                |
|  Menhir del Puig ses Forques                                | Calonge                                                |
|  Menhir del Mas del Mont                                    | Calonge                                                |
|  Galeria catalana de la Carena Jonquet-Vidal                | Torrent                                                |
|  Galeria catalana de Montagut                               |  Vila-romà/Sant Joan de Palamós, Palamós               |
|  Sepulcre de corredor de Can Mina dels Torrents             | Llafranc-Palafrugell                                   |
|  Galeria catalana del Cementiri dels Moros                  | Torrent                                                |
|  Galeria catalana dels Revolts de Torrent                   | Sant Climent de PeraltaPeratallada                     |
|  Galeria catalana de la Serra de Cals                       | Fitor-Fonteta                                          |
|  Galeria catalana de la Taula dels Tres Pagesos             | Fitor-Fonteta                                          |
|  Galeria catalana del Clot de la Tina                       | Sant Pol -la Bisbal                                    |
|  Menhir de la Pedra Dreta de Sant Sadurní                   | Sant Sadurní de l'Heura                                |
|  Cista amb túmul del Cim del Clot del Llorer                | FitorFonteta                                           |
|  Cista amb túmul de la Cadira del Bisbe                     | Sant Pol -la Bisbal                                    |
|  Cista amb túmul de les Pedres Dretes de Ruàs               | Calonge                                                |

Les dades s'han netejat i preparat utilitzant el mateix Google Sheets, obtenint-ne el nom, la població i les coordenades.

La geocodificació de les ubicacions s'ha fet mitjançant un script de Google Apps Script que utilitza les cadenes de text de cada cel·la de la 1a columna del fitxer, i retorna les coordenades del primer resultat obté de Google Maps per cada cel·la.

Script de geocodificació:
```
function myFunction() {
  var sheet = SpreadsheetApp.getActiveSheet();
   
  var range = sheet.getDataRange();
  var cells = range.getValues();
   
  var latitudes = [];
  var longitudes = [];
   
  for (var i = 0; i < cells.length; i++) {
    var address = cells[i][0];
    var geocoder = Maps.newGeocoder().geocode(address);
    var res = geocoder.results[0];
 
    var lat = lng = 0;
    if (res) {
      lat = res.geometry.location.lat;
      lng = res.geometry.location.lng;
    }
   
    latitudes.push([lat]);
    longitudes.push([lng]);
  }
   
  sheet.getRange('B1')
  .offset(0, 0, latitudes.length)
  .setValues(latitudes);
  sheet.getRange('C1')
  .offset(0, 0, longitudes.length)
  .setValues(longitudes);
}
```

S'han revisat les coordenades per cada element del llistat, en cas que els resultats obtinguts per l'script no concordin o faltin s'han recercat manualment. S'han eliminat les entrades les quals no s'ha obtingut ubicació.

TODO: 
- [] Script que obtingui mitjançant XML _l'enllaç a Wikipedia_ per cada entrada
- [] Un cop disposable l'enllaç a Wikipedia estirar: _url del fitxer .jpg de la imatge principal_, _1r paràgraf de l'entrada_
- [] Base de dades amb altres fonts. 



