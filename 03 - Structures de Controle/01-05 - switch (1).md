# switch -> if ... else 
 
Réécrivez les extraits de code suivants en remplaçant le `switch` par des instructions `if else`. Notez que 
la variable `a` est de type `int`. 

~~~cpp 
switch (a) {
    case 0 : cout << "A"; break;
    case 1 : cout << "Z"; break;
    case 2 : cout << "a"; break; 
    default : cout << "b"; break;
}

if (a == 0){
    cout << "A";
} else if (a == 1){
    cout << "Z";
} else if (a == 2){
    cout << "a";
}else{
    cout << "b";
}
~~~

<details>
<summary>Solution</summary>

~~~cpp 
if (a == 0) {
   cout << "A";
} else if (a == 1) {
   cout << "Z";
} else if (a == 2) {
   cout << "a";
} else {
   cout << "b";
}          
~~~
</details>

~~~cpp 
switch (a) {
   case 0 : cout << "0"; 
   default : cout << "D"; break;
}

if (a == 0){
   cout << "0";
}
cout << "D";

~~~


<details>
<summary>Solution</summary>

~~~cpp 
if (a == 0) {
   cout << "0";
}
cout << "D";    
~~~
</details>

~~~cpp 
switch (a) {
   case 0 : 
   case 1 : 
   case 2 : 
   case 3 : 
   case 4 : 
   case 5 : cout << "A"; break;
   case 6 : cout << "3"; 
   case 7 : cout << "4"; break; 
   default : cout << "D"; 
}

if (a >= 0 and a =< 5){
   cout << "A";
}else if (a == 6 || a == 7){
   if (a == 6)
      cout << "3";

   cout << "4";
} else{
   cout << "D";
}
~~~

<details>
<summary>Solution</summary>

~~~cpp 
if (a >= 0 and a <= 5) {
   cout << "A";
} else if (a == 6) {
   cout << "34";
} else if (a == 7) {
   cout << "4";
} else {
   cout << "D";
}             
~~~
</details>
