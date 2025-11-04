# Note ECTS

L'université de Genève utilise le barème suivant pour convertir ses notes au quart de point entre 0 et 6 en notes ECTS entre F et A.

| Note UNIGE  | Note ECTS |
|-------------|---- |
| 5.25 - 6.00 | A |
| 4.75 - 5.00 | B |
| 4.50        | C |
| 4.25        | D |
| 4.00        | E |
| 0.00 - 3.75 | F |

Ecrire un programme qui demande la note à convertir à l'utilisateur, la stocke dans une variable de type `double`, et indique la note ECTS équivalente

- si l'utilisateur entre une note en dehors de la plage 0-6, il faut signaler une erreur.
- si l'utilisateur entre une note qui n'est pas arrondie au quart de point, on la considère comme la note arrondie au quart de point inférieur. Par exemple, si l'utilisateur entre la note 4.60, on indique une note ECTS de C.

Evitez absolument de dupliquer les tests. 

Exemples d'exécution : 

~~~
Entrez la note UNIGE : 5.25
La note ECTS est : A
~~~

~~~
Entrez la note UNIGE : 4.3
La note ECTS est : D
~~~

~~~
Entrez la note UNIGE : 7
Erreur
~~~

~~~cpp
#include <iostream>

using namespace std;

int main() {
    
    cout << "Entrez la note UNIGE : ";
    double note_UNIGE; cin >> note_UNIGE;
    
    if (note_UNIGE <= 6 && note_UNIGE >= 0){
        char note_ECTS = 'G';
    
        if (note_UNIGE >= 5.25){
            note_ECTS = 'A';
        } else if (note_UNIGE >= 4.75){
            note_ECTS = 'B';
        }else if (note_UNIGE >= 4.50){
            note_ECTS = 'C';
        }else if (note_UNIGE >= 4.25){
            note_ECTS = 'D';
        }else if (note_UNIGE >= 4.00){
            note_ECTS = 'E';
        }else
            note_ECTS = 'F';
        }
        
        cout << "Votre note est " << note_ECTS
    }else{
        cout << "La note doit être contenue entre 0-6.";
    }
    
    return EXIT_SUCESS;
}
~~~


<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>

using namespace std;

int main() {

   cout << "Entrez la note UNIGE : ";
   double note;
   cin >> note;

   if (note < 0. or note > 6.) {
      cout << "Erreur";
   } else {
      cout << "La note ECTS est : ";
      if (note < 4.) {
         cout << 'F';
      } else if (note < 4.25) {
         cout << 'E';
      } else if (note < 4.50) {
         cout << 'D';
      } else if (note < 4.75) {
         cout << 'C';
      } else if (note < 5.25) {
         cout << 'B';
      } else {
         cout << 'A';
      }
   }
   cout << endl;
}
~~~

</details>
