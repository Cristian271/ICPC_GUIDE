<div align="center">
  
# Busqueda binaria
La busqueda binaria es un algoritmo de programación que trata de ir "partiendo" a la mitad un arreglo ordenado para encontrar la existencia un valor. 

</div>

## Caracteristicas 
- El arreglo debe estar ordenado
- Complejidad O(log(n))
## Como aplicarlo
Supongamos que queremos saber si un numero k se encuentra en un arreglo de n elementos, el programa va a recibir primero un numero k a encontrar y un numero n que es el tamaño del arreglo
```cpp
#include <bits/stdio.h>
using namespace std;
  
int main(){
  int k, n; cin >> k >> n;
  vector<int> array(n);
  for(int i = 0; i < n; i++) cin >> array[i];
}

```
Como no sabemos si el arreglo esta ordenado en esta ocasión, lo debemos ordenar 

```cpp
  int x = 0;
  int y = n - 1;
sort(array.begin(), array.end());
```
Ahora creamos el ciclo que se encarga de ir "partiendo" el arreglo, el cual seguira siempre y cuando x <= y

```cpp
  while(x <= y){
    int mitad = (x + y)/2;
    // Evaluamos si el numero que estamos buscando es igual al valor que se encuentra en la mitad
    if(k == array[mitad]){
      cout << "Numero encontrado\n";
      return 0;
    }
  }
```
Como no se cumplio esta condición, debemos implementar 2 condiciones mas para ubicar en que mitad se encuentra el valor que estamos buscando para actualizar nuestros 2 punteros que apuntan al inicio y final del area donde estamos buscando
Si k < array[mitad] entonces esta en la izquierda
Si k > array[mitad] entonces esta en la derecha
Esta lógica implementada quedaria como:

```cpp
  while(x <= y){
    int mitad = (x + y)/2;
    // Evaluamos si el numero que estamos buscando es igual al valor que se encuentra en la mitad
    if(k == array[mitad]){
      cout << "Numero encontrado\n";
      return 0;
    }
    if(k < array[mitad]){
      y = mitad - 1;  // Recorremos uno porque ya sabemos que justo el valor de la mitad NO ES
    } else{
      x = amitad + 1;
    }

  }
```
En caso de no existir, saldra del while y imprimimos que no existe, de tal forma que el codigo completo quedaria asi:
```cpp
#include <bits/stdc++.h>
using namespace std;
  
int main(){
  int k, n; cin >> k >> n;
  vector<int> array(n);
  for(int i = 0; i < n; i++) cin >> array[i];

  int x = 0;  // Puntero inicial del area a buscar
  int y = n - 1;  // Puntero final del area a buscar
  sort(array.begin(), array.end());

  while(x <= y){
    int mitad = (x + y)/2;
    // Evaluamos si el numero que estamos buscando es igual al valor que se encuentra en la mitad
    if(k == array[mitad]){
      cout << "Numero encontrado\n";
      return 0;
    }
    if(k < array[mitad]){
      y = mitad - 1;  // Recorremos uno porque ya sabemos que justo el valor de la mitad NO ES
    } else{
      x = mitad + 1;
    }
  }

  cout << "El valor K no existe dentro del arreglo\n";
  
}

```
<div align="center">

# Ejercicios realizados

</div>

## Ejercicio 1
- https://codeforces.com/problemset/problem/2008/C
  
### Solución
Lo que sabemos es lo siguiente
- t casos de prueba
- Nuestro arreglo imaginario esta ordenado y la diferencia entre cada valor con su adyacente tambien debe ser creciente, es decir no es valido 1 2 3 porque entre 1 y 2 la diferencia es 1 y entre 2 y 3 tambien, lo valido es 1 2 4
- Nos dan el valor l que es el valor mas pequeño del arreglo y r que es el valor mas grande del arreglo
- Nos piden la longitud del arreglo mas grande posible

```cpp
#include <bits/stdc++.h>
using namespace std;

int solve(){
    long long l, r; cin >> l >> r;
    r -= l; 

    long long left = 2, right = 1000000000;

    while (left < right){
        long long m = (left + right) / 2;
        if (m * (m - 1) / 2 <= r){
            left = m + 1;
        } else {
            right = m;
        }
    }
    cout << left - 1 << "\n";
    return 0;
}

int main(){
    ios_base::sync_with_stdio(0);cin.tie(0);cout.tie(0);
    int t;cin >> t;
    while (t--){
        solve();
    }
}
```











