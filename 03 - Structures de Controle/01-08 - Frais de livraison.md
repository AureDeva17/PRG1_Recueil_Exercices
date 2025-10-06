# Frais de livraison

Une société suisse tarife ses frais de livraison comme suit :

- 5.00 CHF si livraison en Suisse, à l'exception des cantons des Grisons et du Tessin où les frais de livraison se monte à 7.00 CHF
- 7.00 CHF si livraison au Liechtenstein. 
- 10.00 CHF partout ailleurs dans le monde

Complétez le programme qui suit pour qu'il détermine et affiche le tarif de livraison. Il ne peut poser que des questions auxquelles l'utilisateur répond que par "O" (oui) ou "N" (non)

~~~cpp
#include <iostream>

using namespace std;

int main() {
    const double tarife_suisse = 5.0;
    const double tarife_grisons_tessin_liechtenstein = 7.0; //faux
    const double world = 10.0;

   cout << "Livraison en Suisse ? (O/N) ";
   char reponse1; cin >> reponse1;
   
   if (response1 == 'O'){
        cout << Livraison aux Grisons ou Tessin? (O/N) ;
        char response2; cin >> response2;
        
        if (response2 == 'O'){
            cout << "Le tarife de livraison est " << tarife_grisons_tessin_liechtenstein;
        } else {
            cout << "Le tarife de livraison est " << tarife_suisse;
        }
   } else{
       cout << Livraison au Lichtenstein? (O/N) ;
       char response2; cin >> response2;
       
       if (response2 == 'O'){
            cout << "Le tarife de livraison est " << tarife_grisons_tessin_liechtenstein;
       } else{
            cout << "Le tarife de livraison est " << tarife_world;
       }
   }
   
   return EXIT_SUCCESS
   
   // votre code vient ici
}
~~~

<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>

using namespace std;

int main() {

   const double frais_suisse_sauf_exception =  5.00;
   const double frais_tessin_grison         =  7.00;
   const double frais_liechtenstein         =  7.00;
   const double frais_international         = 10.00;

   double frais; // frais calculés

   cout << "Livraison en Suisse ? (O/N) ";
   char reponse1; cin >> reponse1;

   if (reponse1 == 'O') {
      cout << "Livraison au GR ou TI ? (O/N) ";
      char reponse2; cin >> reponse2;
      frais = (reponse2 == 'O') ?
              frais_tessin_grison :
              frais_suisse_sauf_exception;
   } else {
      cout << "Livraison au Liechtenstein ? (O/N) ";
      char reponse2; cin >> reponse2;
      frais = (reponse2 == 'O') ?
              frais_liechtenstein :
              frais_international;
   }

   cout << "Frais : " << frais << " CHF" << endl;
}
~~~
</details>
