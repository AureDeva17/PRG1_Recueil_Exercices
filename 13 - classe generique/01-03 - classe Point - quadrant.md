# classe générique Point - quadrant 

Reprendre l'exercice précédant [01-02 - classe Point](01-02%20-%20classe%20Point.md)

Soit le dessin

~~~cpp
template <typename T>
class Coord{
private:
   T x;
   T y;
public:
   Coord(const T& x, const T& y) : x(x), y(y){}
   Coord() : Coord(T(),T()){}
   T getX() const;
   T getY() const;
   void afficher() const;
   void setCoord(const T& x, const T& y);
   void deplacer(const T& x, const T& y);
};

template <typename T>
T Coord<T>::getX() const{
   return x;
}

template <typename T>
T Coord<T>::getY() const{
   return y;
}

template <typename T>
void Coord<T>::afficher() const{
   cout << "("<< x << ", " << y <<")";
}

template <typename T>
void Coord<T>::setCoord(const T& x, const T& y){
   this->x = x;
   this->y = y;
}

template <typename T>
void Coord<T>::deplacer(const T& x, const T& y){
   this->x += x;
   this->y += y;
}

template<typename T>
class Point{
   public:
   enum class Quadrant {I, II, III, IV, none};
   
   Point(const string& name, const Coord<T>& coord = Coord<T>()) : name(name), coord(coord) {}
   Point(const string& name, const T& x, const T& y) : name(name), coord(Coord<T>(x,y)) {}
   Point() : Point(string(), Coord<T>()) {} 
   void afficher() const;
   void deplacer(T x, T y);
   void setCoord(const Coord<T>& coord);
   void setNom(const string& name);
   const string& getNom() const {return name;}
   const Coord<T>& getCoord() const;

   Quadrant getQuadrant() const;

   static size_t countInQuadrant(Quadrant q, const vector<Point>& v);

private:
   string name;
   Coord<T> coord;
};

template<typename T>
void Point<T>::afficher() const{
   cout << name;
   coord.afficher();
}

template<typename T>
void Point<T>::deplacer(T x, T y){
   coord.deplacer(x,y);
}

template<typename T>
void Point<T>::setCoord(const Coord<T>& coord){
   this->coord.setCoord(coord.getX(), coord.getY());
}

template<typename T>
void Point<T>::setNom(const string& name){
   this->name = name;
}

template<typename T>
const Coord<T>& Point<T>::getCoord() const{
   return coord;
}

template<typename T>
Quadrant Point<T>::getQuadrant() const{
   if (coord.getX() == T() || coord.getY() == T()){
      return Quadrant::none;
   }

   if (coord.getX() > T()){
      if (coord.getY() > T()){
         return Quadrant::I;
      }else{
         return Quadrant::II;
      }
   }else{
      if (coord.getY() > T()){
         return Quadrant::IV;
      }else{
         return Quadrant::III;
      }
   }
}

template <typename T>
size_t Point<T>::countInQuadrant(Quadrant q, vector<Point<T>> v){
   return count_if(v.begin(), v.end(), [&q](const Point<T>& p) {return q == p.getQuadrant});
}


vector<Point<int>> dessin {{"p1",  1,  2},
                           {"p2",  4,  2},
                           {"p3",  9,  8},
                           {"p4", -1,  5},
                           {"p5",  3, -1},
                           {"p6",  7,  0}};

cout << "I : " << Point<int>::countInQuadrant(Point<int>::Quadrant::I, dessin) << endl;
cout << "II : " << Point<int>::countInQuadrant(Point<int>::Quadrant::II, dessin) << endl;
cout << "III : " << Point<int>::countInQuadrant(Point<int>::Quadrant::III, dessin) << endl;
cout << "IV : " << Point<int>::countInQuadrant(Point<int>::Quadrant::IV, dessin) << endl;
~~~

Ecrire le code permettant de compter combien de `point` se trouvent dans l'un des quandrants `I`, `II`, `III`, `IV` choisi.<br>
**NB** : Une coordonnée sur un axe, voire les deux, n'est sur aucun quadrant.

Donner un exemple d'appel.

<details>
<summary>Solution avec foncteur générique</summary>

~~~cpp
enum class Quadrant {I=1, II, III, IV};

template <typename T>
struct DansQuadrant {
   Quadrant q;
   bool operator() (const Point<T>& p) {
      switch (q) {
         case Quadrant::I   : return p.getCoord().getX() > T() and p.getCoord().getY() > T();
         case Quadrant::II  : return p.getCoord().getX() < T() and p.getCoord().getY() > T();
         case Quadrant::III : return p.getCoord().getX() < T() and p.getCoord().getY() < T();
         case Quadrant::IV  : return p.getCoord().getX() > T() and p.getCoord().getY() < T();
         default            : return false;
      }
   }
};

cout << count_if(dessin.begin(), dessin.end(), DansQuadrant<int>{Quadrant::I});
~~~

</details>


<details>
<summary>Solution alternative avec fonction générique</summary>

~~~cpp
enum class Quadrant { I, II, III, IV };

template<typename T, Quadrant q>
bool est_dans_quadrant (Point<T> const& p) {
   switch (q) {
      case Quadrant::I :
         return p.getCoord().getX() > 0 and p.getCoord().getY() > 0;
      case Quadrant::II :
         return p.getCoord().getX() < 0 and p.getCoord().getY() > 0;
      case Quadrant::III :
         return p.getCoord().getX() < 0 and p.getCoord().getY() < 0;
      case Quadrant::IV :
         return p.getCoord().getX() > 0 and p.getCoord().getY() < 0;
      default:
         return false;
   }
}

cout << count_if(dessin.begin(), dessin.end(),est_dans_quadrant<int,Quadrant::I>);
~~~

</details>

