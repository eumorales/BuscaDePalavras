# 🅰️ Busca de Palavras
[Exercícios](https://www.ime.usp.br/~pf/algoritmos/aulas/strma.html)

## 1️⃣ Questão 1.1
> **Quantas vezes a palavra  AAA  ocorre no texto  AAAAA ?**

![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/funcao.png)
![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/questao1.png)
![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/output1.png)

## 1️⃣ Questão 1.2
> **Quais são os bytes que representam os caracteres  A, C, G, e T?**

![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/questao2.png)
![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/output2.png)

## 2️⃣ Questão 2.1
> **A função inocente está correta quando m > n?  Que acontece se tentarmos executar a função com argumento m igual a 0?**

```
typedef unsigned char byte;

int inocente (byte a[], int m, byte b[], int n) {

   int ocorrs = 0;

   for (int k = m; k <= n; ++k) {

      int i = m, j = k;
      while (i >= 1 && a[i] == b[j])

         --i, --j;

      if (i < 1) ++ocorrs;

   }

   return ocorrs;
}
```


A função inocente não está correta quando 𝑚 > 𝑛, pois não é possível encontrar um vetor maior dentro de um menor. Nesse caso, o laço nunca é executado, e a função sempre retorna 0.

## 2️⃣ Questão 2.2
> **A função inocente está correta quando 𝑚 > 𝑛?  Que acontece se tentarmos executar a função com argumento 𝑚 igual a 0?**


O número máximo de comparações ocorre quando 𝑎 é totalmente repetido em 𝑏, criando sobreposição máxima.
Nesse caso, o total de comparações é 𝑚×(𝑛−𝑚+1) m×(n−m+1), onde: 𝑚 é o tamanho de 𝑎 & 𝑛 é o tamanho de b

## 2️⃣ Questão 2.3
> **Modifique a função inocente de modo que ela resolva a versão original do problema da busca: para cada ocorrência de a em b, imprima o índice j para o qual a[1..m] casa com b[j..m+j-1].**


```
typedef unsigned char byte;

void inocente (byte a[], int m, byte b[], int n) {

   for (int k = m; k <= n; ++k) {

      int i = m, j = k;
      while (i >= 1 && a[i] == b[j])

         --i, --j;

      if (i < 1)

         printf("Ocorrência encontrada no índice %d\n", j + 1);
   }
}
```

## 2️⃣ Questão 2.5
> **Escreva uma função que receba um vetor de bytes b[1..n] e um inteiro m e devolva a posição da primeira ocorrência de m espaços (bytes 32) consecutivos em b.  (Você pode imaginar que os elementos de b representam caracteres ASCII, embora isso seja irrelevante.) Procure examinar o menor número possível de elementos de b. Escreva um programa para testar sua função.**

```
typedef unsigned char byte;

int acharEspacos(byte b[], int n, int m) {

    int contador = 0;

    for (int i = 1; i <= n; ++i) {

        if (b[i] == 32) {

            contador++;

            if (contador == m) {

                return i - m + 1;

            }

        } else {

            contador = 0;

        }

    }

    return -1;

}
```

## 3️⃣ Questão 3.1
> **O seguinte fragmento de código funciona corretamente? for (byte f = 0; f < 256; ++f) ult[f] = 0;**

Não funciona, pois o byte vai somente até `127`.

## 3️⃣ Questão 3.3
> **Verifique que depois do pré-processamento da palavra temos 1 ≤ ult[f] ≤ f para cada f.**

Após o pré-processamento, para cada caractere `f`, o valor de ult[f] representa a última posição de f no padrão a. Isso garante que sempre teremos 1 ≤ ult[f] ≤ f.**

## 3️⃣ Questão 3.4
> **Prove que a fase de pré-processamento na função boyermoore1 preenche corretamente a tabela ult.**

No pré-processamento, o algoritmo percorre o padrão e salva a última posição de cada caractere em `ult`. Isso garente que `ult` está preenchida corretamente, indicando onde cada caractere aparece por último no padrão.

## 3️⃣ Questão 3.5
> **A seguinte versão do código da busca da palavra a no texto b está correta?**
```
ocorrs = 0; k = m;
while (k <= n) {
   i = m, j = k;
   while (i >= 1 && a[i] == b[j]) --i, --j;   
   if (i < 1) ++ocorrs;
   kk = k+1;                                 
   while (kk <= n && ult[b[kk]] == 0) ++kk;  
   if (kk > n) break;                       
   k += m - ult[b[kk]] + kk - k;
}
return ocorrs;
```

Não, o código está errado. O cálculo para avançar k pode pular posições erradas ou até entrar em loop infinito

## 3️⃣ Questão 3.6
> **Podemos eliminar o if (k == n) k += 1 se introduzirmos uma sentinela apropriada na posição b[n+1]. Escreva essa versão de boyermoore1.**

```
public int boyermoore(char[] a, char[] b, int m, int n) {

    b[n] = '\0'; // Assume que '\0' não está em 'a'

    int ocorrs = 0;
    int k = m;

    while (k <= n) {
        int i = m;
        int j = k;

        while (i >= 1 && a[i] == b[j]) {
            --i;
            --j;
        }

        if (i < 1) {
            ++ocorrs;
        }

        int kk = k + 1;
        while (kk <= n && ult[b[kk]] == 0) {
            ++kk;
        }

        if (kk > n) break;

        k += m - ult[b[kk]] + 1;
    }

    return ocorrs;
}
```

## 3️⃣ Questão 3.6
> **Mostre que a seguinte versão da função boyermoore1 está correta:**

```
int ult[256];
for (int i = 0; i < 256; ++i) ult[i] = 0;
for (int i = 1; i <   m; ++i) ult[a[i]] = i;
int ocorrs = 0, k = m;
while (k <= n) {
   int i = m, j = k;
   while (i >= 1 && a[i] == b[j]) 
      --i, --j;   
   if (i < 1) ++ocorrs;
   k += m - ult[b[k]];
}
return ocorrs;
```

Essa versão está correta pois faz o pré-processamento e o avanço de `k` do jeito esperado por Boyer-Moore.

