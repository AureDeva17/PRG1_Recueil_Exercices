# Tri à bulles

Effectuez le tri à bulles sur les tableaux suivants. 
Indiquez l'état du tableau après chaque échange.
<br>Les valeurs assurément triées sont représentées entre`()`.

~~~
1) 3 2 5 1 4
23514
23145
21345
12345
~~~

<details>
<summary>Solution</summary>

| 3 | 2 | 5 | 1 | 4 |
|:-:|:-:|:-:|:-:|:-:|
| 2 | 3 | 5 | 1 | 4 |
| 2 | 3 | 1 | 5 | 4 |
| 2 | 3 | 1 | 4 |(5)|
| 2 | 1 | 3 |(4)|(5)|
| 1 | 2 |(3)|(4)|(5)|

</details>


~~~
2) 4 3 2 5 1
32451
23451
2341(5)
231(45)
21(345)
12345
~~~

<details>
<summary>Solution</summary>

| 4 | 3 | 2 | 5 | 1 |
|:-:|:-:|:-:|:-:|:-:|
| 3 | 4 | 2 | 5 | 1 |
| 3 | 2 | 4 | 5 | 1 |
| 3 | 2 | 4 | 1 |(5)|
| 2 | 3 | 4 | 1 |(5)|
| 2 | 3 | 1 |(4)|(5)|
| 2 | 1 | 3 |(4)|(5)|
| 1 | 2 |(3)|(4)|(5)|

</details>

~~~
3) 5 4 2 3 1
45231
4231(5)
231(45)
21(345)
12345
~~~

<details>
<summary>Solution</summary>

| 5 | 4 | 2 | 3 | 1 |
|:-:|:-:|:-:|:-:|:-:|
| 4 | 5 | 2 | 3 | 1 |
| 4 | 2 | 5 | 3 | 1 |
| 4 | 2 | 3 | 5 | 1 |
| 4 | 2 | 3 | 1 |(5)|
| 2 | 4 | 3 | 1 |(5)|
| 2 | 3 | 4 | 1 |(5)|
| 2 | 3 | 1 |(4)|(5)|
| 2 | 1 |(3)|(4)|(5)|
| 1 | 2 |(3)|(4)|(5)|

</details>

