# 🅰️ Busca de Palavras
[Link do Repositório](https://github.com/usuário/repositório)

## 1️⃣ Questão 1.1
> **Quantas vezes a palavra  AAA  ocorre no texto  AAAAA ?**

![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/funcao.png)
![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/questao1.png)
![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/output1.png)

## 1️⃣ Questão 1.2
> **Quais são os bytes que representam os caracteres  A, C, G, e T?**

![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/questao2.png)
![Imagem](https://github.com/eumorales/BuscaDePalavras/raw/main/assets/output2.png)

## 1️⃣ Questão 2.1
> **A função inocente está correta quando m > n?  Que acontece se tentarmos executar a função com argumento m igual a 0?**
> 
```
typedef unsigned char byte;

// Recebe vetores a[1..m] e b[1..n],
// com m >= 1 e n >= 0, e devolve
// o número de ocorrências de a em b.

int 
inocente (byte a[], int m, byte b[], int n) 
{
   int ocorrs = 0;
   for (int k = m; k <= n; ++k) {
      // a[1..m] casa com b[k-m+1..k]?
      int i = m, j = k;
      while (i >= 1 && a[i] == b[j]) 
         --i, --j;   
      if (i < 1) ++ocorrs;
   }
   return ocorrs;
}
```


A função inocente não está correta quando 𝑚 > 𝑛, pois não é possível encontrar um vetor maior dentro de um menor. Nesse caso, o laço nunca é executado, e a função sempre retorna 0.

