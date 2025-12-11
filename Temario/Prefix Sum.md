<div align="center">
  
# Prefix Sum  
Prefix sum es una tecnica que crea una nueva secuencia donde cada elemento es la suma de todos los elementos anteriores en la secuencia original 
  
</div>

## Caracteristicas
- De la forma en la que se aplica en este codigo, el primer indice es exclusivo y el segundo indice es inclusivo.
- Complejidad O(1)
## Como aplicarlo
El ejemplo mas básico para entender su aplicación, es suponer que requieres saber la suma de todos los valores que hay en un intervalo de l a r en un arreglo de n numeros.
Para ello deberemos tener un vector extra el cual llamaremos prefixSum

```cpp
int solve(){
  int n; cin >> n; // Tamaño del arreglo original
  vector<int> array(n+1);
  vector<int> prefixSum(n+1);
}
```

Por cuestiones de practicidad, vamos a crear el arreglo original y el PrefixSum con una unidad mas del tamaño que debe ser, y declaramos en ambos que el indice 0 es igual a 0

```cpp
int solve(){
  int n; cin >> n; // Tamaño del arreglo original
  vector<int> array(n+1);
  vector<int> prefixSum(n+1);

  array[0] = 0;
  prefixSum[0] = 0;

}
```

Ahora para crear nuestro prefix sum, debemos sumar lo que esa en el indice actual y el anterior mientras recibimos los valores del usuario
```cpp
  for(int i = 1; i <= n; i++){
  cin >> array[i];
  prefixSum[i] = prefixSum[i-1] + array[i]; 
  }
```

Para saber la suma de los valores que hay entre un rango de indices, bastaria con restar el prefixSum[r] - prefixSum[l] para saberlo
```cpp
  // Suponiendo que ya recibimos los indices l y R
  cout << "La suma de los valores que hay entre los indices l y R son: " << prefixSum[r] - prefixSum[l];
```

El código completo quedaria de esta forma:
```cpp
#include <bits/stdc++.h>
using namespace std;

int solve(){
  int n; cin >> n; // Tamaño del arreglo original
  int l, r; cin >> l >> r; // Indices
  vector<int> array(n+1);
  vector<int> prefixSum(n+1);

  array[0] = 0;
  prefixSum[0] = 0;

  for(int i = 1; i <= n; i++){
    cin >> array[i];
    prefixSum[i] = prefixSum[i-1] + array[i]; 
  }

  cout << "La suma de los valores que hay entre los indices l y R son: " << prefixSum[r] - prefixSum[l];
  return 0;
}

int main(){
  ios_base::sync_with_stdio(0);cout.tie(0);cin.tie(0);
  solve();

}

```

## Ejercicios realizados
A. Minimise Sum
time limit per test1.5 seconds
memory limit per test256 megabytes
This problem differs from problem G. In this problem, you must output the minimum sum of prefix minimums after at most one operation.

You are given an array a
 of length n
, with elements satisfying 0≤ai≤n
. You can perform the following operation at most once:

Choose two indices i
 and j
 such that i<j
. Set ai:=ai+aj
. Then, set aj=0
.
Output the minimum possible value of min(a1)+min(a1,a2)+…+min(a1,a2,…,an)
 that you can get.

Input
Each test contains multiple test cases. The first line contains the number of test cases t
 (1≤t≤104
). The description of the test cases follows.

The first line of each test case contains an integer n
 (2≤n≤2⋅105
) — the length of a
.

The following line contains n
 space-separated integers a1,a2,…,an
 (0≤ai≤n
) — denoting the array a
.

It is guaranteed that the sum of n
 over all test cases does not exceed 2⋅105
.

Output
For each test case, output an integer on a new line, the minimum possible value of min(a1)+min(a1,a2)+…+min(a1,a2,…,an)

Example:
input
3
2
1 2
3
1 2 3
4
3 0 2 3

output
2
2
2

Note
In the second test case, it is optimal to perform the operation with i=2 and j=3
In the third test case, it is optimal to not perform any operations. The answer is 3
## Solución
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
 
ll propiedadNoBroAquiPuroCocoYahir(vector<ll> &prefix, int x, int y, int i)
{
    ll suma = 0;
    ll numero = prefix[i];
    ll actualMin = prefix[i + 1] - prefix[i];
    if (i == 0)
    {
        return x + y;
    }
    else if (actualMin >= x + y)
    {
        suma = numero + (x + y);
    }
    else
    {
        suma = numero + actualMin;
    }
 
    return suma;
}
 
ll solve()
{
    ll sumOriginal = 0, n;
    cin >> n;
    vector<ll> array(n);
    vector<ll> prefix(n + 1);
 
    prefix[0] = 0;
    cin >> array[0];
    ll mini = array[0];
    sumOriginal += mini;
    prefix[1] = mini;
 
    for (int i = 1; i < n; i++)
    {
        cin >> array[i];
        mini = min(mini, array[i]);
        sumOriginal += mini;
        prefix[i + 1] = sumOriginal;
    }
 
    ll bestSum = sumOriginal;
    for (int i = 0; i < n - 1; i++)
    {
        ll x = array[i], y = array[i + 1];
        bestSum = min(bestSum, propiedadNoBroAquiPuroCocoYahir(prefix, x, y, i));
    }
 
    cout << bestSum << "\n";
 
    return 0;
}
 
int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    ll t;
    cin >> t;
 
    while (t--)
    {
        solve();
    }
}
```
Nota: Este ejercicio se resuelve con una propiedad matematica pero se puede realizar a fuerza bruta con prefix sum. Ademas es ejercicio privado por lo que si quieres probar
si hiciste bien el codigo o no, lo suyo seria que pruebes casos con este codigo que fue aceptado por el juez virtual.
