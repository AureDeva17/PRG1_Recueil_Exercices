# Constructeurs de la classe string

Indiquer ce que va afficher chacune des séquences d'instructions suivantes : 

_Il se peut qu'une séquence provoque une erreur à la compilation ou à l'exécution, voire ait un comportement indéfini. Le cas échéant, répondez "Erreur à la compilation", "Erreur à l'exécution" ou "Comportement indéfini"_




1.
~~~cpp
string s1 = "ABC";
string s2(s1, 1);
cout << '|' << s2 << '|' << endl; //BC
~~~

2.
~~~cpp
string s1 = "ABC";
string s2(s1, 2, 3);
cout << '|' << s2 << '|' << endl; //C
~~~

3.	
~~~cpp
string s1 = "ABC";
string s2(s1, 3, 2);
cout << '|' << s2 << '|' << endl; //
~~~

4.	
~~~cpp
string s1 = "ABC";
string s2(s1, 4, 1);
cout << '|' << s2 << '|' << endl;//erreur exec
~~~

5.	
~~~cpp
string s("ABC", 3);
cout << '|' << s << '|' << endl;//ABC
~~~

6.	
~~~cpp
string s("ABC", 4);
cout << '|' << s << '|' << endl;//ABC\0
~~~

7.	
~~~cpp
string s("ABC", 5);
cout << '|' << s << '|' << endl;//unknown
~~~

8.	
~~~cpp
string s(3, 'A');
cout << '|' << s << '|' << endl;//AAA
~~~


<details>
<summary>Solution</summary>

1. |BC|
2.	|C|
3.	||
4.	Erreur à l'exécution
5.	|ABC|
6.	|ABC\0|
7.	Comportement indéfini
8.	|AAA|

</details>