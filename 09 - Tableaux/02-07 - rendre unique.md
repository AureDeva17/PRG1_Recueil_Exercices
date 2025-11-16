# Rendre unique 

Sans faire usage de `vector::erase`, écrire une fonction C++ qui supprime tout élément égal à l'élément qui les précède dans le `vector`. Avec la fonction `to_string` de l'exercice 02-03, le programme ci-dessous

~~~cpp
vector<int>& supprimer_une_valeur(vector<int>& v, size_t index){
   if (index > v.size()-1)
      return v;

   for (size_t i = index; i < v.size() - 1; ++i){
      v[i] = v[i + 1];
   }

   v.resize(v.size()-1);

   return v;
}

bool is_in(vector<int>& v, int value){
   for (int i : v){
      if (i == value)
         return true;
   }

   return false;
}

vector<int>& rendre_unique_vrai(vector<int>& v){

   vector<int> v2;

   for (size_t i = 0; i < v.size(); ++i){
      if (is_in(v2,v[i])){
         supprimer_une_valeur(v, i);
      }
      else{
         v2.push_back(v[i]);
      }
   }

   return v;
}

vector<int>& rendre_unique(vector<int>& v){
   size_t write_idx = 0;

   for (size_t read_idx = 1; read_idx < v.size(); ++read_idx){
      if (v[read_idx] != v[write_idx]){
         v[++write_idx] = v[read_idx];
      }
   }

   v.resize(write_idx + 1);

   return v;
}

int main() {
   for (vector<int> v: {vector<int>{},
                        {2},
                        {1, 2, 2, 2, 3, 1, 2, 4},
                        {2, 3, 3, 2, 2, 1},
                        {2, 2, 2},
                        {5, 4, 4, 3, 2, 2, 2, 3}}) {
      cout << to_string(v) << " -> ";
      rendre_unique(v);
      cout << to_string(v) << endl;
   }
}
~~~ 

doit afficher 

~~~
[] -> []
[2] -> [2]
[1, 2, 2, 2, 3, 1, 2, 4] -> [1, 2, 3, 1, 2, 4]
[2, 3, 3, 2, 2, 1] -> [2, 3, 2, 1]
[2, 2, 2] -> [2]
[5, 4, 4, 3, 2, 2, 2, 3] -> [5, 4, 3, 2, 3]
~~~

<details>
<summary>Solution</summary>

Le principe de la meilleure solution est similaire à celui de l'exercice précédent. Il faut utiliser
deux indices, l'un en lecture et l'autre en écriture. La boucle commence à l'élément d'indice 1, 
celui d'indice 0 n'étant jamais supprimé. 

~~~cpp
void rendre_unique(vector<int>& v) {
   if(v.empty()) return;

   size_t write_idx = 0;
   for(size_t read_idx = 1; read_idx < v.size(); ++read_idx) {
      if (v[read_idx] != v[write_idx]) {
         v[++write_idx] = v[read_idx];
      }
   }
   v.resize(write_idx + 1);
}
~~~

</details>

