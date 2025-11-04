# Nombre de jours dans un mois

Soient les déclarations ci-dessous et la fonction `est_bissextile(..)` d'un exercice précédant.

~~~cpp
using Jour  = uint8_t;
using Mois  = uint8_t;
using Annee = uint16_t;

struct Date {
   Jour  jour;
   Mois  mois;
   Annee annee;
};

bool est_bissextile(Annee annee){
   return !(annee % 400) || !(annee % 4) && annee % 100
}

int jour_dans_mois(Mois mois, Annee annee){
   if (mois == 2){
      if (est_bissextile(annee)){
         return 29;
      }else{
         return 28;
      }
   }
   else{
      if (mois % 2){
         return 30;
      }
      else{
         return 31;
      }
   }
}
~~~


Ecrire une fonction qui retourne le nbre de jours pour un mois et une année donnés.

La fonction reçoit en paramètre le *mois* et l'*année* et retourne le nombre de jours correspondant ou la valeur `0` en cas d'erreur.

**NB** Utiliser un *enum* pour cette question

<details>
<summary>Solutions</summary>

~~~cpp
uint8_t nbre_jours_mois (Mois m, Annee a) {

   enum Liste_Mois {JANVIER = 1, FEVRIER, MARS, AVRIL, MAI, JUIN, JUILLET,
                    AOUT, SEPTEMBRE, OCTOBRE, NOVEMBRE, DECEMBRE};

   // NB : "enum" et non "enum class" => pas d'opérateur d'appartenance "::" dans le case
   // si c'était "enum class T_Mois {..}" alors "case T_Mois::JANVIER : .."

   switch (m) {
      case FEVRIER   : return 28 + est_bissextile(Date{1, m, a});
      case JANVIER   :
      case MARS      :
      case MAI       :
      case JUILLET   :
      case AOUT      :
      case OCTOBRE   :
      case DECEMBRE  : return 31;
      case AVRIL     :
      case JUIN      :
      case SEPTEMBRE :
      case NOVEMBRE  : return 30;
      default        : return 0;
   }
}
~~~
</details>

