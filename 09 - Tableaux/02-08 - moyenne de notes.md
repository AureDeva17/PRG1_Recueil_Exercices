# Moyennes de notes
Ecrire un programme C++ qui :

1. demande à l'utilisateur de saisir une série de notes
2. calcule la moyenne de ces notes
3. affiche la moyenne de ces notes avec 2 chiffres après la virgule

Exemple d'exécution : 

~~~
Entrez la liste de vos notes, 0 pour quitter :
5 6 5.5
4 3.5 0
nb de notes saisies = 5
La moyenne des notes saisies = 4.80
~~~

~~~cpp
#include <vector>
#include <iostream>
#include <iomanip>
#include <cstdlib>

using namespace std;

bool is_in(const vector<double>& v, double value){
   for (int i : v){
      if (i == value)
         return true;
   }

   return false;
}

double sum(const vector<double>& v){
   double sum = 0;

   for (double val : v){
      sum += val;
   }

   return sum;
}

int main(){

   constexpr double exit_value = 0d;

   cout << "Entrez la liste de vos notes, 0 pour quitter : ";

   vector<double> marks;
   double value = 0;

   while(true){
      cin >> value;
      if (value != exit_value)
         marks.push_back(value);
      else{
         break;
      }
   }

   cout << "nb de notes saisies = " << marks.size();
   cout << "La moyenne des notes saisies = " << setprecision(2) << sum(marks)/marks.size();

   return EXIT_SUCCESS;
}
~~~

<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>
#include <iomanip>
using namespace std;

vector<double> lireNotes();
double moyenne(vector<double> const& notes);

int main() {
   vector<double> notes = lireNotes();

   cout << "nb de notes saisies = " << notes.size() << endl;
   if (notes.empty()) {
      cout << "Moyenne non calculable car aucune note saisie !" << endl;
   } else {
      cout << fixed << setprecision(2)
           << "La moyenne des notes saisies = " << moyenne(notes) << endl;
   }
}

vector<double> lireNotes() {
   cout <<  "Entrez la liste de vos notes, 0 pour quitter :" << endl;

   vector<double> v;

   double note;
   while(cin >> note and note != 0) {
         v.push_back(note);
   }

   return v;
}

double moyenne(vector<double> const & v) {
   double somme = 0;
   for (double d : v) {
      somme += d;
   }
   return somme / static_cast<double>(v.size());
   // cast sinon warning
   // retourne nan si v.empty()
}
~~~

</details>

