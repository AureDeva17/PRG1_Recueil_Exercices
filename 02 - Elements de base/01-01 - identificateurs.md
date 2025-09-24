# Identificateurs (noms des variables) en c++
Pour chacun des cas ci-dessous, indiquez s'il s'agit d'un identificateur C++ légal ou non. Justifiez votre réponse si celle-ci est "Non"

|  #  | Identificateur | Oui / Non | Explication | 
| --- | -------------- | --------- | ----------- |
| 1 | `007` |Non |commence par chiffre |
| 2 | `james_bond_007`  |oui | |
| 3 | `james_bond__007`  |oui | |
| 4 | `james bond` |non |espace |
| 5 | `sOs` |oui | |
| 6 | `SOS` |non |tout en maj |
| 7 | `_007` |oui | |
| 8 | `__007` |oui | |
| 9 | `_007_` |oui | |
| 10 | `bond-007` |non |- |
| 11 | `tom&jerry` |non |& |
| 12 | `int` |non |mots réservé |
| 13 | `INT` |OUI |mais découseillé |
| 14 | `André` |non |é |
| 15 | `_` |oui | |



<details>
<summary>Solution</summary>

|  #  | Identificateur | Oui / Non | Explication | 
| --- | -------------- | --------- | ----------- |
|1 | `7` | Non | Un identificateur ne peut pas commencer par un chiffre |
|2 | `james_bond_007` | Oui |  |
|3 | `james_bond__007` | Oui | Plusieurs _ peuvent se suivre |
|4 | `james bond` | Non | Pas d'espace dans un identificateur |
|5 | `sOs` | Oui |  |
|6 | `SOS` | Oui | Vu que C++ tient compte de la casse, 5) est un identificateur différent de 6) |
|7 | `_007` | Oui | Un identificateur peut commencer par _ |
|8 | `__007` | Oui |  |
|9 | `_007_` | Oui |  |
|10 | `bond-007` | Non | Le caractère '-' n'est pas autorisé |
|11 | `tom&jerry` | Non | Le caractère '&' n'est pas autorisé |
|12 | `int` | Non | Mot réservé |
|13 | `INT` | Oui | Déconseillé toutefois ! |
|14 | `André` | Non | Les lettres accentuées ne sont pas autorisées |
|15 | `_` | Oui | … mais pas des plus parlants (!) |


</details>