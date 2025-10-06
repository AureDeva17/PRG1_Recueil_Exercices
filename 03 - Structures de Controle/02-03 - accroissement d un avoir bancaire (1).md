# Accroissement d'un avoir bancaire (1)

Ecrire un programme C++ qui, après avoir demandé à l'utilisateur de saisir 
- un montant initial 
- un montant cible
- un taux d'intérêt annuel (en %)

détermine et affiche combien d'années (entières) sont nécessaires pour atteindre ou dépasser le montant cible. Notons que 
- Les saisies utilisateur sont supposées correctes
- Le taux d'intérêt annuel est supposé rester constant au cours du temps

Exemples d'exécution : 

~~~
Entrez le montant initial > 1000
Entrez le montant cible > 1000000
Entrez le taux d'interet annuel en % > 5
Le montant cible est atteint apres 142 ans.
~~~

~~~
Entrez le montant initial > 1000
Entrez le montant cible > 1030
Entrez le taux d'interet annuel en % > 5
Le montant cible est atteint apres 1 an.
~~~

~~~
Entrez le montant initial > 1000
Entrez le montant cible > 900
Entrez le taux d'interet annuel en % > 5
Le montant cible est atteint apres 0 an.
~~~

~~~
Entrez le montant initial > 1000
Entrez le montant cible > 2000
Entrez le taux d'interet annuel en % > -2
Le montant ne sera jamais atteint
~~~

~~~cpp
#include <iostream>
#include <cstdlib>

using namespace std;

int main() {
   //demande et reçois le montant initial
   cout << "Entrez le montant initial > ";
   double montant_initial = 0; 
   cin >> montant_initial;
   
   //demande et reçois le montant cible
   cout << endl << "Entrez le montant cible > ";
   double montant_cible = 0; 
   cin >> montant_cible;

   //demande et reçois le taux d'intérets annuel
   cout << endl << "Entrez le taux d'interet annuel en % > ";
   int taux_annuel = 0; 
   cin >> taux_annuel;

   //test si le taux est valable
   if (taux_annuel >= 0 && montant_cible >= montant_initial || taux_annuel <= 0 && montant_cible <= montant_initial){
      int nombre_annee = 0;
      double montant_actuel = montant_initial;

      //ajoute le taux une fois par année jusqu'à ce que le montant atteint ou dépasse la cible
      while (montant_cible > montant_actuel && montant_cible >= montant_initial || montant_cible < montant_actuel && montant_cible <= montant_initial){
         montant_actuel += montant_actuel * taux_annuel / 100
         ++nombre_annee;
      }

      cout << endl << "Le montant cible est atteint apres" << nombre_annee << "an"  << (nombre_annee > 1 ? "s" : "") << ".";

   } else{
      cout << endl << "Le montant ne sera jamais atteint";
   }

   return EXIT_SUCCESS;

}
~~~

<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>
#include <cstdlib>

using namespace std;

int main() {
   cout << "Entrez le montant initial > ";
   double montant_initial; // en CHF
   cin >> montant_initial;

   cout << "Entrez le montant cible > ";
   double montant_cible; // en CHF
   cin >> montant_cible;

   cout << "Entrez le taux d'interet annuel en % > ";
   double taux_interet_annuel; // en %
   cin >> taux_interet_annuel;

   // cas particulier
   if (montant_initial < montant_cible and taux_interet_annuel <= 0.0) {
      cout << "Le montant cible ne sera jamais atteint" << endl;
      return EXIT_SUCCESS;
   }
   
   double montant = montant_initial;
   int nb_annees = 0;
   while (montant < montant_cible) {
      ++nb_annees;
      montant = montant * (1.0 + taux_interet_annuel / 100.0);
   }

   cout << "Le montant cible est atteint apres "
        << nb_annees << " an" << (nb_annees > 1 ? "s" : "") << "." << endl;

   return EXIT_SUCCESS;
}
~~~
</details>

