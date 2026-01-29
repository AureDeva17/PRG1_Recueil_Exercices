Une image couleur est composée d'une grille rectangulaire de couleurs codées avec trois composantes RGB (Red, Green, Blue) auxquels on accède via leurs coordonnées (x,y) dans le plan. Ecrivez les structures et classe 
suivantes

- une structure `Color` stockant les valeurs de `R`, `G` et `B` sous forme d'entiers non signés sur 8 bits

- ainsi qu'une structure `Coord` stockant les valeurs de `x` et `y` sous forme d'entiers non signés 
  - la constante `Coord::origin` contient les coordonnées d'origine (0,0) communes à toutes les `Coord`
  
- et une classe `Image` qui 
  - stocke sa dimension (hauteur `h` et largeur `w`) sous forme d'entiers non signés
  - stocke les `h * w` couleurs dans un tableau à 1 dimension
  - l'utilisateur spécifie `h` et `w` à l'initalisation, ainsi que la couleur unique servant à initialiser l'ensemble de l'image
  - permet de lire la dimension de l'image via des méthodes `getw` et `geth`
  - permet d'accéder en lecture (toujours) et en écriture (si l'image est variable) aux couleurs de l'image via leurs coordonnées. Pour un point de coordonnées `p`, l'indice correspondant dans le tableau 1D est `p.x + w * p.y`
    - lève une exception appropriée de la librairie `<stdexcept>` si la coordonnée fournie est en dehors de l'image 
  - fournit une méthode `subImage` qui reçoit la coordonnée minimale et les longueur et largeur qui décrivent un rectangle dans l'image, et retourne un image de la taille demandée contenant le contenu de ce rectangle
    - lève une exception appropriée de la librairie `<stdexcept>` si le rectangle demandé n'est pas entièrement dans l'image 
  
Seule la méthode `subImage` doit être définie séparément.<br>
Les autres peuvent être définie en ligne. 

~~~cpp
#ifndef IMAGE_H
#define IMAGE_H

#include <cstdint>
#include <stdexcept>
#include <vector>

struct Color{
   uint8_t R;
   uint8_t G;
   uint8_t B;
};

struct Coord{
   static const Coord origin = Coord{0,0}; 

   unsigned int x;
   unsigned int y;
};

class Image{
public:
   Image(unsigned int h, unsigned int w, Color col) : colors(h*w, col){}
   unsigned int getw() const {return w}
   unsigned int geth() const {return h}

   Color operator[](Coord p) const {return colors.at(p.x + w * p.y);}
   Color& operator[](Coord p) {return colors.at(p.x + w * p.y);}

   Image subImage(const Coord& p, unsigned int h, unsigned int w) const;

private:
   unsigned int h;
   unsigned int w;
   std::vector<Color> colors;
}
#endif
~~~

~~~cpp
#include "Image.h"

Image Image::subImage(const Coord& p, unsigned int h, unsigned int w) const{

   if (p.x+w > this->w || p.y+h > this->h) throw out_of_range("Sub image is too big for image");

   Image sub(h,w, Color{0,0,0});

   for (unsigned int y = 0; y < h; ++y){
      for (unsigned int x = 0; x < w; ++x){{
         sub[{x,y}] = (*this)[{p.x+x,p.y+y}];
      }
   }

   return sub;
}
~~~

~~~cpp
#include <iostream>
#include <cassert>

#include "Image.h"

using namespace std;

int main() {

   Color cyan{0, 255, 255};
   cout << "cyan codé comme (" << +cyan.R << "," << +cyan.G << "," << +cyan.B << ")" << endl;

   Coord p{10, 20};
   cout << "p(" << p.x << "," << p.y << ")" << endl;
   cout << "origin(" << Coord::origin.x << "," << Coord::origin.y << ")" << endl;

   Color black{0,0,0};
   Image imageHD(1280, 720, black);
   cout << "Image HD de taille " << imageHD.getw() << "x" << imageHD.geth() << endl;
   cout << "La composante G du pixel de coordonnée p est " << +imageHD[p].G << endl;

   imageHD[p] = cyan;
   cout << "La composante G du pixel de coordonnée p est " << +imageHD[p].G << endl;

   Image sub = imageHD.subImage(p,20,10);
   cout << "sub de taille " << sub.getw() << "x" << sub.geth() << endl;

   cout << "La composante B du pixel en (0,0) est " << +sub[Coord::origin].B << endl;
}
~~~

<details>
<summary>image.h</summary>

~~~cpp
#ifndef PRG1_EXAMEN_IMAGE_H
#define PRG1_EXAMEN_IMAGE_H

#include <vector>
#include <exception>
#include <cstdint>
#include <ostream>

struct Color {
   uint8_t R, G, B;
};

struct Coord {
   size_t x, y;
   static const Coord origin;
};

class Image {
   size_t w, h;
   std::vector<Color> data;
public:
   Image(size_t w, size_t h, Color c) : w(w), h(h), data(w * h, c) { }

   size_t getw() const { return w; }
   size_t geth() const { return h; }

   Color const& operator[](Coord const& p) const { return data[idx(p)]; }
   Color& operator[](Coord const& p) { return data[idx(p)]; }

   Image subImage(Coord p1, size_t w, size_t h) const;
private:
   size_t idx(Coord const& p) const {
      if (p.x >= w or p.y >= h) throw std::out_of_range("Image");
      return p.x + w * p.y;
   }
};

#endif //PRG1_EXAMEN_IMAGE_H
~~~

</details>

<details>
<summary>image.cpp</summary>

~~~cpp
#include "Image.h"

const Coord Coord::origin{};

Image Image::subImage(Coord p1, size_t w, size_t h) const {
   // validate input
   idx(p1);
   idx(Coord{p1.x + w - 1, p1.y + h - 1});

   Image out(w, h, Color{});
   for(Coord p{0, 0}, pi{p1}; p.y < h; ++p.y, ++pi.y)
      for(p.x = 0, pi.x = p1.x; p.x < w; ++p.x, ++pi.x)
         out[p] = (*this)[pi];
   return out;
}
~~~

</details>