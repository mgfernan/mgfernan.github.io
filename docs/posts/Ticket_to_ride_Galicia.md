---
draft: true
date: 2023-12-24
categories:
  - Jocs de taula
---

# Enginyeria inversa: Aventureros al Tren

Fa uns dies vaig saber d'una sèrie de manifestacions coordinades pel
[Bloque Nacionalista Galego](https://www.bng.gal) per tal de recuperar les
línies nocturnes de tren cap a Galicia. Ràpidament vaig pensar: per què no
fer una *customització* del joc [Aventureros al tren](https://boardgamegeek.com/boardgame/9209/ticket-ride)?

La idea es pot titllar quasi bé de reivindicació...

Com sabeu, "Aventureros al Tren" és un joc en el que els jugadors competeixen
per completar rutes de tren de la manera més eficient possible. La primera versió
del joc se situa als Estats Units d'Amèrica, a finals del segle XIX, en plena
expansió del ferrocarril.

![Aventureros al tren USA](../assets/Ticket_to_ride_USA.png)

<!-- more -->

Donat que fer el *playtesting* és un procès molt laboriòs, he pensat que el podria
escurçar bastant fent enginyeria inversa per tal d'extreure la informació necessària
per crear una *costumització*:

- Quina és la distribució de vies per color i longitud?
- Com es distribueixen els tiquets de trajectes?

Amb aquesta informació es pot tenir una bona base per crear una versió pròpia
de l'Aventureros al Tren.

Veient el mapa ja podeu fer el primer pas (tot i que us faltarien les cartes
de ticket de ruta). Per facilitar-vos la feina, us deixo aquí els enllaços a un seguit de fitxers CSV que donen precisament la informació que necessitem

- [Tracks](../assets/Ticket_to_ride%20-%20Tracks.csv)
- [Tickets](../assets/Ticket_to_ride%20-%20Tickets.csv)
- [Stations](../assets/Ticket_to_ride%20-%20Stations.csv)

Teniu el [Google Sheet](https://docs.google.com/spreadsheets/d/1DrTWc_W_NuV-JlYGM8i6ZygJZyPB_Ag4Lp8eN25kk50) amb el que s'han creat aquests fitxers.

Abans de continuar, fixem algunes definicions:

- **enllaç** fa referencia a les vies entre dues estacions
- **ruta** és un seguit d'enllaços
- **longitud** és el nombre de vagons que es necessiten per completar un enllaç.

Us resumeixo els aspectes clau:

- El joc té 36 estacions
- Té un total de 100 enllaços
- Cada color té 7 enllaços distribuits en diverses longituds: 6-5-4-4-3-3-2. Els colors
verd i blanc tenen els enllaços distribuits amb una petita diferència: 6-5-5-4-3-2-2.
Els enllaços grisos són comodins.

## Teoria de grafs?

Un cop fet el primer anàlisi del model del joc es pot veure que, de fet, estem
davant d'un [*graf*](https://ca.wikipedia.org/wiki/Graf_(matem%C3%A0tiques)), o
una "representació abstracta d'un conjunt d'objectes on alguns parells dels objectes estan connectats per enllaços". En un graf hi han *nodes* i *enllaços*. En el cas del
joc Aventureros al Tren, els nodes són les estacions i els vertex (o enllaços)
són els enllaços.

Fer aquest paral·lelisme ens serà de gran utilitat per utilitzar llibreries
d'anàlisi de graf i **buscar el camí més curt entre dues estacions**. D'aquesta manera
no ens caldrà reinventar la roda quan haguem de construir els tickets de ruta.
