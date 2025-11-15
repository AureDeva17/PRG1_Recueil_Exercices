# Prénom, nom et acronyme
Ecrire un programme C++ qui après avoir demandé à l'utilisateur de saisir son prénom et son nom (sur la même ligne), affiche à l'écran son prénom, son nom ainsi que son acronyme.
**NB**  L'acronyme s'obtient en concaténant la première lettre du prénom, la première lettre du nom et la dernière lettre du nom, le tout mis entièrement en majuscules.
IMPORTANT
On supposera :
- que l'utilisateur n'entre qu'un seul prénom et qu'un seul nom
- que le nom ne contient aucun espace blanc

Il n'est pas demandé ici de tenir compte des cas où l'utilisateur n'entrerait que son prénom, que son nom, voire ni son prénom, ni son nom.

Exemple d'exécution
~~~
Entrez votre prenom et votre nom : Alexandre Dumas

Votre prenom est   : Alexandre
Votre nom est      : Dumas
Votre acronyme est : ADS
~~~

~~~cpp
#include <string>
#include <iostream>
#include <cstdlib>
#include <cctype>

using namespace std;

int main(){

    string prenom;
    string nom;
    cout << "Entrez votre prenom et votre nom : ";
    cin >> prenom;
    cin >> nom;

    cout << "Votre prénom est : " << prenom;
    cout << "Votre nom est : " << nom;
    cout << "Votre acronyme est : " << nom.front() << prenom.front() << toupper(prenom.back());

    return EXIT_SUCCESS;
}
~~~

<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

string toupper_str(string_view input){
    string result(input);
    for (char& c : result) {
        c = toupper(c);
    }
    return result;
}

int main() {

    string prenom, nom;
    cout << "Entrez votre prenom et votre nom : ";
    cin >> prenom >> nom;

    string acronyme{prenom.at(0), nom.at(0), nom.at(nom.length() - 1)};

    acronyme = toupper_str(acronyme);

    cout << endl
         << "Votre prenom est   : " << prenom << endl
         << "Votre nom est      : " << nom << endl
         << "Votre acronyme est : " << acronyme << endl;

    return EXIT_SUCCESS;
}
~~~



</details>