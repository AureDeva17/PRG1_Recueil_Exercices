# Point avec opérateurs
Reprenez la classe Point de l'exercice [03-01](03-01%20Point%20avec%20constructeurs.md) et faites les modifications / ajouts / suppressions nécessaires afin que le code ci-dessous s'exécute correctement et affiche le résultat ci-après.

~~~cpp
#include <iostream>

using namespace std;

class Point{

private:
   double x, y;

public:
   friend Point& operator+= (const Point& p);
   friend Point& operator*= (double d);
   friend bool operator== (const Point& p1, const Point& p2) const;
   friend ostream& operator<< (const ostream& os, const Point& p1) const;

    Point() : Point(0.,0.) {}
    Point(double x, double y) : x(x), y(y) {}
    Point(const Point& p) : x(p.x), y(p.y) {};

    double getX() const return x;
    double getY() const return y;
    double setX(double x) this->x = x;
    double setY(double y) this->y = y;

    void afficher() const;
    void deplacer(double x, double y);
}

Point& operator+= (const Point& p){
   this->x += p.x;
   this->y += p.y;

   return *this;
}

Point& operator*= (double d){
   this->x *= d;
   this->y *= d;

   return *this;
}

Point operator+ (const Point& p1, const Point& p2) const{
   return Point(p1) += p2;
}
Point operator* (const Point& p1, const Point& p2) const{
   return Point(p1.x * p2.x, p1.y * p2.y);
}
Point operator* (double d, const Point& p1) const{
   return Point(p1) * d;
}
Point operator* (Point& p1, double d) const{
   return d * p1;
}
bool operator== (const Point& p) const{
   return this->x == p.x && this->y == p.y;
}
ostream& operator<< (const ostream& os, const Point& p1) const{
   return os << "(" << p1.x << "," << p1.y << ")";
}

void Point::afficher() const{
   cout << p.x << " -- " << p.y << endl;
}

void Point::deplacer(double x, double y){
   this->x += x;
   this->y += y;
}

int main() {

   Point p1(1.2, 2.4);
   Point p2(3., 4.2);

   cout << "p1" << p1 << ", p2" << p2 << endl;

   cout << "p1 + p2 = " << p1 + p2 << endl;
   cout << "p2 + p1 = " << p2 + p1 << endl;

   cout << "p1 * 2. = " << p1 * 2. << endl;
   cout << "3. * p1 = " << 3. * p1 << endl;

   cout << (p1 == p2 ? "p1 == p2" : "p1 != p2") << endl;
   Point p3(p1);
   cout << (p1 == p3 ? "p1 == p3" : "p1 != p3") << endl;
}
~~~

~~~text
p1(1.2,2.4), p2(3.0,4.2)
p1 + p2 = (4.2,6.6)
p2 + p1 = (4.2,6.6)
p1 * 2. = (2.4,4.8)
3. * p1 = (3.6,7.2)
p1 != p2
p1 == p3
~~~

<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>

using namespace std;

class Point {
public:
   Point();
   Point(double x, double y);

   Point& operator+=(Point const& other);
   Point& operator*=(double d);

private:
   double x, y;

   friend ostream& operator<< (ostream& out, Point const& pt);
   friend bool operator == (Point const& lhs, Point const& rhs);
};

Point::Point() : Point(0., 0.) {}

Point::Point(double x, double y) : x(x), y(y) {}

ostream& operator<< (ostream& out, Point const& pt) {
   return out << "(" << pt.x << "," << pt.y << ")";
}

Point& Point::operator+=(const Point& other) {
   x += other.x;
   y += other.y;
   return *this;
}

Point operator+ (Point pt1, Point const& pt2) {
   return pt1 += pt2;
}

Point& Point::operator*=(double d) {
   x *= d; y *= d; return *this;
}

Point operator* (Point pt, double d) {
   return pt *= d;
}

Point operator* (double d, Point pt) {
   return pt *= d;
}

bool operator == (Point const& lhs, Point const& rhs) {
   return lhs.x == rhs.x and lhs.y == rhs.y;
}

int main() {

   Point p1(1.2, 2.4);
   Point p2(3., 4.2);

   cout << "p1" << p1 << ", p2" << p2 << endl;

   cout << "p1 + p2 = " << p1 + p2 << endl;
   cout << "p2 + p1 = " << p2 + p1 << endl;

   cout << "p1 * 2. = " << p1 * 2. << endl;
   cout << "3. * p1 = " << 3. * p1 << endl;

   cout << (p1 == p2 ? "p1 == p2" : "p1 != p2") << endl;
   Point p3(p1);
   cout << (p1 == p3 ? "p1 == p3" : "p1 != p3") << endl;
}
~~~

</details>
