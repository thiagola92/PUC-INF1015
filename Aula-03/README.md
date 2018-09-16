# Funções Recursivas Primitivas

## Funções básicas (iniciais)
* **Zero**: Z(n) = 0 para todo n
  * Uma função que recebe qualquer valor e retorn 0
    * Z(999999896785678) = 0
* **Sucessor**: S(n) = o número que sucede n na sequência dos números naturais
  * Uma função que pega o número depois de n
    * S(0) = 1
    * S(1) = 2
    * ...
    * S(n) = n+1
* **Projeções**: P<sub>k</sub><sup>i</sup>(x<sub>1</sub>, ... , x<sub>k</sub>) = x<sub>i</sub> para 1 ≤ i ≤ k
  * Uma função que recebe k valores e você quer selecionar o i-ésimo
    * P<sub>6</sub><sup>4</sup>(5,6,7,8,9,10) = 8
      * São 6 valores: 5,6,7,8,9,10
      * Você quer o quarto: 5,6,7,**8**
  * Pode ser chamada de função de seleção

## Operações básicas
Primeira coisa que vou avisar é que como você pode ver, escrever x<sub>1</sub>, ... , x<sub>k</sub> para mim é um saco **e** eu não sei como escrever um vetor aqui no computador (eu queria ter uma tecla que botasse um x com uma seta na cabeça).  
De agora em diante:  
x<sub>1</sub>, ... , x<sub>k</sub> = ẍ  
Isso é um x com dois pontos em cima, aquele acento que fica na tecla 6 (shift 6 + x) (espero que seu teclado seja igual ao meu). Com isso dito, vamos continuar...  

* **Composição**: g(h<sub>1</sub>(ẍ), ..., h<sub>k</sub>(ẍ)) = f(ẍ)
  * A maneira mais fácil de entender é pensar que não tem vetores: g(h(x)) = f(x)
    * Básicamente a função f(x) é uma função que é a execução da h(x) primeiro e depois de g(x)
      * h(x) = S(x)
      * g(x) = S(S(x))
      * f(x) = g(h(x)) = g(S(x)) = S(S(S(x)))
      * Ex: f(2) = g(h(2)) = g(3) = 5
    * Você talvez reconheca por g∘h(x) = f(x)  
  * Agora considere que x é um vetor: g(h(ẍ)) = f(ẍ)
    * Para cada um dos valores do vetor o h aplica a função dele
    * Para cada um dos resultados do vetor o g aplica a função dele
    * Isso funciona que nem a lógica anterior
      * h(ẍ) = S(ẍ)
      * g(ẍ) = S(S(ẍ))
      * f(ẍ) = g(h(ẍ)) = g(S(ẍ)) = S(S(S(ẍ)))
      * Ex: f(2, 10, 3) = g(h(2, 10, 3)) = g(3, 11, 4) = 5, 13, 6
  * Agora considere que f é uma função que aplica uma função para o primeiro valor, outra função para o segundo, outra para o terceiro...
    * g(h<sub>1</sub>(ẍ), ..., h<sub>k</sub>(ẍ)) = f(ẍ)
      * h<sub>1</sub>(ẍ) = S(ẍ)
      * h<sub>2</sub>(ẍ) = Z(ẍ)
      * g(ẍ) = S(S(ẍ))
      * f(ẍ) = g(h<sub>1</sub>(ẍ), h<sub>2</sub>(ẍ)) = g(S(ẍ), Z(ẍ)) = S(S(S(ẍ), Z(ẍ)))
      * Ex: f(2, 10) = g(h<sub>1</sub>(2, 10), h<sub>2</sub>(2, 10)) = g([3, 11], [0, 0]) = [5, 13], [2, 2]
    * Outra maneira de escrever:
      * g∘<h<sub>1</sub>, ..., h<sub>k</sub>>(ẍ) = g(h<sub>1</sub>(ẍ), ..., h<sub>k</sub>(ẍ))
* **Recursão primitiva**:
  * f(0) = d
  * f(n+1) = g(f(n), n)
    * Se a função f recebe 0, então retorna um número d
    * Se a função f recebe um valor diferente de 0
      * Executa a função g em cima da função f recebendo um valor anterior
      * Executa a função g em cima do valor anterior
        * g(x, y) = S(x)
        * f(0) = 10
        * f(n+1) = g(f(n), n)
        * Ex:
          * f(3)
          * g(f(2), 2)
          * g(g(f(1), 1), 2)
          * g(g(g(f(0), 0), 1), 2)
          * g(g(g(10, 0), 1), 2)
          * S(S(S(10), 1), 2)
          * S(S(11), 2)
          * S(12)
          * 13
  * Se a recursão for em cima de um vetor:
  * f(0, ẍ) = h(ẍ)
  * f(n+1, ẍ) = g(f(n, ẍ), n, ẍ)
    * Basicamente a única diferença é que você acrescentou o vetor em tudo... E a função base é em cima de um vetor.

## Exemplos
Usando as funções anteriores conseguimos definir muitas coisas

* **Constantes**: λx S(S( ... S(Z(x)) ... ))
  * Para todo número natural n, podemos definir ele como uma função chama a função zero Z e depois repete n vezes a função sucesso S  
    * 3 = S(S(S(Z(x))))
    * Não importa qual x você passe
  * Como pessoas querem evitar usar 3 pontos, vamos reescrever
    * C<sub>0</sub> = Z   
    * C<sub>n+1</sub>(x) = S(C<sub>n</sub>(x))
    * Estamos utilizando a idéia de recursão
  * λx S(S( ... S(Z(x)) ... )) = λx C<sub>n</sub>(x)


* **Adição**:
  * +(0, x) = P<sub>1</sub><sup>1</sup>(x)
  * +(n+1, x) = S(P<sub>1</sub><sup>1</sup>(+(n, x), n, x))
  * Como essa sintaxe pode ser difícil de entender, comece tirando P<sub>1</sub><sup>1</sup>.
    * +(0, x) = x
    * +(n+1, x) = S(+(n, x))
      * Lembre que o sinal de + aqui é apenas tratado como simbolo de função, igual a Z ou S
        * +(2, 3)
        * S(+(1, 3))
        * S(S(+(0, 3)))
        * S(S(3))
        * 5
  * O problema com o método escrito acima é que não segue a operação básica de recursão, pois requer passar o n e x
    * f(0, ẍ) = h(ẍ)
    * f(n+1, ẍ) = g(f(n, ẍ), n, ẍ)
  * Se escrevermos apenas
    * +(0, x) = x
    * +(n+1, x) = S(+(n, x), n, x)
    * Note que receberemos varios valores de saida
      * +(2, 3)
      * S(+(1, 3), 2, 3)
      * S(S(+(0, 3), 1, 3), 2, 3)
      * S(S(3, 1, 3), 2, 3)
      * S(4, 2, 4, 2, 3)
      * 5, 3, 5, 3, 4
    * Por isso utilizamos a função de projeção/seleção.
  * +(0, x) = P<sub>1</sub><sup>1</sup>(x)
  * +(n+1, x) = S(P<sub>1</sub><sup>1</sup>(+(n, x), n, x))
    * +(2, 3)
    * S(P<sub>1</sub><sup>1</sup>(+(1, 3), 2, 3))   `eu estou executando logo a função de projeção para ficar menor`
    * S(+(1, 3))
    * S(S(P<sub>1</sub><sup>1</sup>(+(0, 3), 1, 3)))   `eu estou executando logo a função de projeção para ficar menor`
    * S(S(+(0, 3)))
    * S(S(P<sub>1</sub><sup>1</sup>(3)))
    * S(S(3))
    * S(4)
    * 5




21:56
