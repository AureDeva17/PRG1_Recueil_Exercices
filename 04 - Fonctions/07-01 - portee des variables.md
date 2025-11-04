# Portée des variables
Déterminer "à la main" ce que va afficher, à l'exécution, le programme ci-dessous.

~~~cpp
#include <cstdlib>
#include <iostream>

using namespace std;

int a, b;

//------------------------------------------------------------
int f(int c) { //1
   int n = 0;
   a = c; //global a = 1
   if (n < c) { //true 0 < 1
      n = a + b; //1
   }
   return n; //1
}

//------------------------------------------------------------
int g(int c) { //1
   int n = 0; //0
   int a = c; //1
   if (n < f(c)) { //true 0 < 1
      n = a + b;     //1 + 0 = 1
   }
   return n;      //1
}

//------------------------------------------------------------
int main() {
   int i = 1;
   int b = g(i);
   cout << "resultat : " << a + b + i << endl; // resultat : 3

   return EXIT_SUCCESS;
}
~~~

<details>
<summary>Indice</summary>
Les variables globales, tout comme les statics valent "0" par défaut.
</details>

<details>
<summary>Solution</summary>
resultat : 3
</details>
