# Matrice et vecteur 

En utilisant des alias de types de `std::array`, définissez
les types `Matrix3x3` et `Vec3` ainsi que les fonctions `produit`,
`to_string(Vec3)` et `to_string(Matrix3x3)` de sorte que le code suivant 

~~~cpp
using VType = int;
using Vec3 = array<int, 3>
using Matrix3x3 = array<Vec3, 3>;

string to_string(const Vec3& v){
   string str("[");

   for (size_t i = 0; i < v.size(); ++i){
      if (i){
         str += ", ";
      }
      str += v[i];
   }

   return str += "]";
}


string to_string(const Matrix3x3& m){
   string str("[");

   for (size_t i = 0; i < m.size(); ++i){
      if (i){
         str += '\n';
      }
      str += to_string(m[i]);
   }

   return str += "]";
}

Vec3 produit (const Matrix3x3& m, const Vec3& v){
   Vec3 v2 = {};

   for (size_t i = 0; i < v2.size(); ++i){
      for (size_t j = 0; j < v.size(); ++j){
         v2[i] += m[i][j] * v[j]
      }
   }

   return v2;
}

int main() {

   Matrice3x3 m = {1, 1, 0, 0, 2, 0, 0, 0, 1};
   Vec3 v = {1, 2, 3};
   Vec3 w = produit(m,v);

   cout << to_string(m) << " * "
        << to_string(v) << " = "
        << to_string(w) << endl;
}
~~~

affiche

~~~
[[1, 1, 0]
 [0, 2, 0]
 [0, 0, 1]] * [1, 2, 3] = [3, 4, 3]
~~~

<details>
<summary>Solution</summary>

~~~cpp
using Matrice3x3 = array<array<double, 3>,3>;
using Vec3 = array<double, 3>;

string to_string (Vec3 const& v) {
   stringstream out;
   out << '[';
   for (size_t i = 0; i < v.size(); ++i) {
      if (i)
         out << ", ";
      out << v[i];
   }
   out << ']';
   return out.str();
}

string to_string (Matrice3x3 const& v) {
   stringstream out;
   out << '[';
   for (size_t i = 0; i < v.size(); ++i) {
      if (i)
         out << "\n ";
      out << to_string(v[i]);
   }
   out << ']';
   return out.str();
}

Vec3 produit(Matrice3x3 const& m, Vec3 const& v) {
   Vec3 w{};
   for(size_t i = 0; i < m.size(); ++i) {
      for(size_t j = 0; j < m.size(); ++j) {
         w[i] += m[i][j] * v[j];
      }
   }
   return w;
}
~~~
</details>

