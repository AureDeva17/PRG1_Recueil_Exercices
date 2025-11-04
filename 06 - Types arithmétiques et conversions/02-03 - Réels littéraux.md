# Littéraux constants

Pour chacune des lignes de code suivante, indiquez 
- si elle compile
- si oui
  - quel est le type de la variable
  - ce que la ligne affiche; 
  
  ~~~
  auto v1 = 1.5;        cout << v1 << endl;
  oui, 1.5
  
  auto v2 = 1E3;        cout << v2 << endl;
  oui, 1000

  auto v4 = 12.0u;      cout << v4 << endl;
  non, double pas en unsigned

  auto v6 = 1.0L;       cout << v6 << endl;
  long double 1

  auto v7 = .5;         cout << v7 << endl;
  0.5 double

  auto v8 = 5.;         cout << v8 << endl;
  double 5

  auto v14 = 0x0.2;     cout << v14 << endl;
  non, l'hexa c'est bizzare

  auto v17 = 0x1.p0;    cout << v17 << endl;
  oui double

  auto v18 = 0x1.8p+0f; cout << v18 << endl;
  float

  auto v19 = 0x1.p-2L;  cout << v19 << endl;
  long double

  auto v20 = 0x1.1p+2;  cout << v20 << endl; 
  double
  ~~~

<details>
<summary>Solution</summary>

~~~cpp
double v1 = 1.5;            // 1.5

double v2 = 1E3;            // 1000

// auto v4 = 12.0u;         un réel ne peut être non signé

long double v6 = 1.0L;      // 1

double v7 = .5;             // 0.5

double v8 = 5.;             // 5


~~~

</details>
