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
  * +(n+1, x) = S(P<sub>3</sub><sup>1</sup>(+(n, x), n, x))
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
  * +(n+1, x) = S(P<sub>3</sub><sup>1</sup>(+(n, x), n, x))
    * +(2, 3)
    * S(P<sub>3</sub><sup>1</sup>(+(1, 3), 2, 3))   `eu estou executando logo a função de projeção para ficar menor`
    * S(+(1, 3))
    * S(S(P<sub>3</sub><sup>1</sup>(+(0, 3), 1, 3)))   `eu estou executando logo a função de projeção para ficar menor`
    * S(S(+(0, 3)))
    * S(S(P<sub>1</sub><sup>1</sup>(3)))
    * S(S(3))
    * S(4)
    * 5
* **Multiplicação**:
  * \*(0,x) = Z(x) = 0
  * \*(n+1, x) = +(P<sub>3</sub><sup>1</sup>(\*(n, x), n, x), x)
  * n é quantas vezes multiplicar, x é o número a ser multiplicado
  * Exemplo:
    * \*(2, 3)
    * +(P<sub>3</sub><sup>1</sup>(\*(1, 3), 1, 3), 3) `eu sempre faço primeiro a função projeção porque n afeta o calculo e diminui o tamanho`
    * +(\*(1, 3), 3)
    * +(+(P<sub>1</sub><sup>1</sup>(\*(0, 3), 0, 3), 3), 3)
    * +(+(\*(0, 3), 3), 3)
    * +(+(0, 3), 3) `já provamos a soma, então não vou escrever de novo`
    * +(3, 3)
    * 6
* **Exponenciação**:
  * Exp(0, x) = 1
  * Exp(n+1, x) = \*(P<sub>3</sub><sup>1</sup>(Exp(n, x), n, x), x)
  * n é o expoente, x é a base
  * Exemplo:
    * Exp(2, 3)
    * \*(P<sub>3</sub><sup>1</sup>(Exp(1, 3), 1, 3), 3)
    * \*(Exp(1, 3), 3)
    * \*(\*(P<sub>3</sub><sup>1</sup>(Exp(0, 3), 0, 3), 3), 3)
    * \*(\*(Exp(0, 3), 3), 3)
    * \*(\*(1, 3), 3)
    * \*(3, 3)
    * 9
* **Sinal**:
  * sn(0) = 0
  * sn(n+1) = P<sub>2</sub><sup>1</sup>(C<sub>1</sub>, n) = 1
  * É tipo verdadeiro e falso em linguagem de programação, 0 é falso e 1 é verdadeiro.  
* **Teste de zero**:
  * !sn(0) = 1
  * !sn(n+1) = P<sub>2</sub><sup>1</sup>(C<sub>0</sub>, n) = 0
  * Oposto da de cima
* **Predecessor**:
  * Pred(0) = 0
  * Pred(n+1) = P<sub>2</sub><sup>2</sup>(f(n), n)
  * A função f é indiferente, pois você pega o segundo valor (n)
* **Subtração limitada (Monus)**:
  * ∸(0, x) = P<sub>1</sub><sup>1</sup>(x)
  * ∸(n+1, x) = Pred(P<sub>3</sub><sup>1</sup>(∸(n, x), n, x))
  * É uma subtração limitada pois não pode ir abaixo de 0
    * Normalmente 5 - 7 = 2, nesse caso 5 ∸ 7 = 0
  * É o por quanto você está subtraindo x, ou seja, o calculo é x ∸ n
  * Exemplo:
    * ∸(2, 3)
    * Pred(P<sub>3</sub><sup>1</sup>(∸(1, 3), 1, 3))
    * Pred(∸(1, 3))
    * Pred(Pred(P<sub>3</sub><sup>1</sup>(∸(0, 3), 0, 3)))
    * Pred(Pred(∸(0, 3)))
    * Pred(Pred(3)) `sempre usando conhecimento anterior sem problema`
    * Pred(2)
    * 1
  * Exemplo 2:
    * ∸(2, 1)
    * Pred(P<sub>3</sub><sup>1</sup>(∸(1, 1), 1, 1))
    * Pred(∸(1, 1))
    * Pred(Pred(P<sub>3</sub><sup>1</sup>(∸(0, 1), 0, 1)))
    * Pred(Pred(∸(0, 1)))
    * Pred(Pred(1))
    * Pred(0)
    * 0
* **Menor Igual**:
  * MenorIgual(0, x) = !sn(x)
  * MenorIgual(n+1, x) = !sn(∸(S(P<sub>3</sub><sup>2</sup>(MenorIgual(n, x), n, x)), x))
  * A idéia é verificar se x ≤ n + 1, vai retornar 1 se for e 0 se não for.
  * Exemplo:
    * MenorIgual(3, 2)
    * !sn(∸(S(P<sub>3</sub><sup>2</sup>(MenorIgual(2, 2), 2, 2)), 2))
    * !sn(∸(S(2), 2))
    * !sn(∸(3, 2))
    * !sn(0)
    * 1
  * Exemplo 2:
    * MenorIgual(2, 3)
    * !sn(∸(S(P<sub>3</sub><sup>2</sup>(MenorIgual(1, 3), 1, 3)), 3))
    * !sn(∸(S(1), 3))
    * !sn(∸(2, 3))
    * !sn(1)
    * 0
  * Exemplo 3:
    * MenorIgual(3, 3)
    * !sn(∸(S(P<sub>3</sub><sup>2</sup>(MenorIgual(2, 3), 2, 3)), 3))
    * !sn(∸(S(2), 3))
    * !sn(∸(3, 3))
    * !sn(0)
    * 1
* **Estritamente Maior**:
  * Maior(0, x) = 0
  * Maior(n+1, x) = !sn(MenorIgual(S(P<sub>3</sub><sup>2</sup>(Maior(n, x), n, x)), x))
  * x > n + 1
  * Usa a lógica do menor igual, se for verdade que é menor igual então claramente não é maior, caso contrario é maior.
  * Exemplo:
    * Maior(3, 2)
    * !sn(MenorIgual(S(P<sub>3</sub><sup>2</sup>(Maior(2, 2), 2, 2)), 2))
    * !sn(MenorIgual(S(2), 2))
    * !sn(MenorIgual(3, 2))
    * !sn(1)
    * 0
  * Exemplo 2:
    * Maior(2, 3)
    * !sn(MenorIgual(S(P<sub>3</sub><sup>2</sup>(Maior(1, 3), 1, 3)), 3))
    * !sn(MenorIgual(S(1), 3))
    * !sn(MenorIgual(2, 3))
    * !sn(0)
    * 1
  * Exemplo 3:
    * Maior(3, 3)
    * !sn(MenorIgual(S(P<sub>3</sub><sup>2</sup>(Maior(2, 3), 2, 3)), 3))
    * !sn(MenorIgual(S(2), 3))
    * !sn(MenorIgual(3, 3))
    * !sn(1)
    * 0
* **Diferença Absoluta**:
  * DifAbs(0, x) = x
  * DifAbs(n+1, x) = +(∸(S(P<sub>3</sub><sup>2</sup>(DifAbs(n, x), n, x)), x), ∸(x, S(n)))
  * Isso faz nada mais que |a - b|
  * Usando subtração limitada, melhor maneira de fazer isso é (a ∸ b) + (b ∸ a)
  * Exemplo:
    * DifAbs(2, 3)
    * +(∸(S(P<sub>3</sub><sup>2</sup>(DifAbs(1, 3), 1, 3)), 3), ∸(3, S(1)))
    * +(∸(S(1), 3), ∸(3, S(1)))
    * +(∸(2, 3), ∸(3, S(1)))
    * +(∸(2, 3), ∸(3, 2))
    * +(1, ∸(3, 2))
    * +(1, 0)
    * 1
* **Igualdade**:
  * Igual(0, x) = !sn(x)
  * Igual(n+1, x) = !sn(DifAbs(S(P<sub>3</sub><sup>2</sup>(Igual(n, x), n, x)), x))
  * Se a diferença absoluta for 0 então é verdade que é igual (retorna 1 para verdadeiro, 0 para falso)
  * Exemplo:
    * Igual(2, 3)
    * !sn(DifAbs(S(P<sub>3</sub><sup>2</sup>(Igual(1, 3), 1, 3)), 3))
    * !sn(DifAbs(S(1), 3))
    * !sn(DifAbs(2, 3))
    * !sn(1)
    * 0
  * Exemplo 2:
    * Igual(3, 3)
    * !sn(DifAbs(S(P<sub>3</sub><sup>2</sup>(Igual(2, 3), 2, 3)), 3))
    * !sn(DifAbs(S(2), 3))
    * !sn(DifAbs(3, 3))
    * !sn(0)
    * 1
* **Estritamente Menor**
  * Menor(0,x) = 0
  * Menor(n+1,x) = !sn(+(Maior(S(n),x),Igual(S(n),P<sub>3</sub><sup>3</sup>(Menor(n,x),n,x))))
  * x < n + 1
  * Faz a soma do resultado da verificação de maior e da verificação de igualdade. Se a soma der maior que 0 é porque um deles é verdadeiro (x é maior ou igual a n+1), logo precisamos tornar o resultado 0 (false).
  * Se os dois forem falso (x é menor que n+1), logo precisamos tornar o resultado 1 (true).
  * Exemplo:
    * Menor(3,3)
    * !sn(+(Maior(S(2),3),Igual(S(2),P<sub>3</sub><sup>3</sup>(Menor(2,3),2,3))))
    * !sn(+(Maior(S(2),3),Igual(S(2),3)))
    * !sn(+(Maior(S(2),3),Igual(3,3)))
    * !sn(+(Maior(3,3),Igual(3,3)))
    * !sn(+(0,Igual(3,3)))
    * !sn(+(0,1))
    * !sn(1)
    * 0
* **Impar**:
  * impar(0) = 0
  * impar(n+1) = !sn(P<sub>3</sub><sup>1</sup>(impar(n), n))
  * Exemplo:
    * impar(3)
    * !sn(P<sub>2</sub><sup>1</sup>(impar(2), 2))
    * !sn(impar(2))
    * !sn(!sn(P<sub>2</sub><sup>1</sup>(impar(1), 1)))
    * !sn(!sn(impar(1)))
    * !sn(!sn(!sn(P<sub>2</sub><sup>1</sup>(impar(0)), 0)))
    * !sn(!sn(!sn(impar(0))))
    * !sn(!sn(!sn(0)))
    * !sn(!sn(1))
    * !sn(0)
    * 1
  * Exemplo 2:
    * impar(4)
    * !sn(P<sub>2</sub><sup>1</sup>(impar(3), 3))
    * !sn(impar(3))
    * !sn(!sn(P<sub>2</sub><sup>1</sup>(impar(2), 2)))
    * !sn(!sn(impar(2)))
    * !sn(!sn(!sn(P<sub>2</sub><sup>1</sup>(impar(1), 1))))
    * !sn(!sn(!sn(impar(1))))
    * !sn(!sn(!sn(!sn(P<sub>2</sub><sup>1</sup>(impar(0), 0)))))
    * !sn(!sn(!sn(!sn(impar(0)))))
    * !sn(!sn(!sn(!sn(0))))
    * !sn(!sn(!sn(1)))
    * !sn(!sn(0))
    * !sn(1)
    * 0
* **Metade**:
  * ÷(0) = 0
  * ÷(n+1) =  +(P<sub>2</sub><sup>1</sup>(÷(n), n), impar(n))
  * A idéia é fazer uma divisão que só retorna inteiro
    * Se n for par vai retornar n/2
    * Se n for impar vai retornar (n-1)/2
  * A divisão por 2 é feita basicamente somando 1 para todos os números impares até o número desejado.
  * Exemplo:  
    * ÷(4)
    * +(P<sub>2</sub><sup>1</sup>(÷(3), 3), impar(3))
    * +(÷(3), impar(3))
    * +(÷(3), 1)
    * +(+(P<sub>2</sub><sup>1</sup>(÷(2), 2), impar(2)), 1)
    * +(+(÷(2), impar(2)), 1)
    * +(+(÷(2), 0), 1)
    * +(+(+(P<sub>2</sub><sup>1</sup>(÷(1), 1), impar(1)), 0), 1)
    * +(+(+(÷(1), impar(1)), 0), 1)
    * +(+(+(÷(1), 1), 0), 1)
    * +(+(+(+(÷(0), impar(0)), 1), 0), 1)
    * +(+(+(+(÷(0), 0), 1), 0), 1)
    * +(+(+(+(0, 0), 1), 0), 1)
    * +(+(+(0, 1), 0), 1)
    * +(+(1, 0), 1)
    * +(1, 1)
    * 2
  * Exemplo 2:
    * ÷(3)
    * +(P<sub>2</sub><sup>1</sup>(÷(2), 2), impar(2))
    * +(÷(2), impar(2))
    * +(÷(2), 0)
    * +(+(P<sub>2</sub><sup>1</sup>(÷(1), 1), impar(1)), 0)
    * +(+(÷(1), impar(1)), 0)
    * +(+(÷(1), 1), 0)
    * +(+(+(P<sub>2</sub><sup>1</sup>(÷(0), 0), impar(0)), 1), 0)
    * +(+(+(÷(0), impar(0)), 1), 0)
    * +(+(+(÷(0), 0), 1), 0)
    * +(+(+(0, 0), 1), 0)
    * +(+(0, 1), 0)
    * +(1, 0)
    * 1
* **Somatório**:
  * ∑(0) = 0
  * ∑(n+1) = +(∑(n),S(n))
  * Simplesmente, ∑(n+1) = (n+1) + ∑n
  * Exemplo:
    * ∑(3)
    * +(∑(2),S(2))
    * +(∑(2),3)
    * +(+(∑(1),S(1)),3)
    * +(+(∑(1),2),3)
    * +(+(+(∑(0),S(0)),2),3)
    * +(+(+(∑(0),1),2),3)
    * +(+(+(0,1),2),3)
    * +(+(1,2),3)
    * +(3,3)
    * 6
* **Máximo**:
  * Max(0, x) = x
  * Max(n+1, x) = +(∸(S(n), P<sub>3</sub><sup>3</sup>(Max(n, x), n, x)), S(n))
  * Pegar o maior dos dois valores
  * O calculo é x ∸ (n+1) + n+1
  * Parece sem sentido se fosse subtração normal, mas com a limitada a gente consegue obter o mairo disso.
    * x > (n+1) então o calculo da x
    * x < (n+1) então o calculo da n+1
    * x = (n+1) então o calculo da n+1 que vai ser o mesmo valor que x
  * Exemplo:
    * Max(3, 2)
    * +(∸(S(2), P<sub>3</sub><sup>3</sup>(Max(2, 2), 2, 2)), S(2))
    * +(∸(S(2), 2), S(2))
    * +(∸(3, 2), S(2))
    * +(∸(3, 2), 3)
    * +(0, 3)
    * 3
  * Exemplo 2:
    * Max(2, 3)
    * +(∸(S(1), P<sub>3</sub><sup>3</sup>(Max(1, 3), 1, 3)), S(1))
    * +(∸(S(1), 3), S(1))
    * +(∸(2, 3), S(1))
    * +(∸(2, 3), 2)
    * +(1, 2)
    * 3
* **Máximo entre 3**:
  * Max3(0, y, z) = Max(y, z)
  * Max3(n+1, y, z) = Max(S(P<sub>4</sub><sup>2</sup>(Max(n, y, z), n, y, z)), Max(y, z))
  * Exemplo:
    * Max3(3, 2, 1)
    * Max(S(P<sub>4</sub><sup>2</sup>(Max(2, 2, 1), 2, 2, 1)), Max(2, 1))
    * Max(S(2), Max(2, 1))
    * Max(3, Max(2, 1)) `já sabemos calcular máximo entre 2 números`
    * Max(3, 2)
    * 3
* **Divisão**:  
  * /(0, x) = 0
  * /(n+1, x) = +(1,/(∸(x, S(P<sub>3</sub><sup>2</sup>(/(n,x),n,x))), x))
  * 1 + ( (n+1 ∸ x) / x )  
  * Essa divisão arredonda para cima.
  * n+1 é o numerador e x é o denominador.  
  * Exemplo:  
    * /(6,3)
    * +(1,/(∸(3, S(P<sub>3</sub><sup>2</sup>(/(5,3),5,3))), 3))
    * +(1,/(∸(3, S(5)), 3))
    * +(1,/(∸(3, 6), 3))
    * +(1,/(3, 3))
    * +(1,+(1,/(∸(3, S(P<sub>3</sub><sup>2</sup>(/(2,3),2,3))), 3)))
    * +(1,+(1,/(∸(3, S(2)), 3)))
    * +(1,+(1,/(∸(3, 3), 3)))
    * +(1,+(1,/(0, 3)))
    * +(1,+(1,0))
    * +(1,1)
    * 2
  * Exemplo 2:
    * /(4,3)  
    * +(1,/(∸(3, S(P<sub>3</sub><sup>2</sup>(/(3,x),3,3))), 3))  
    * +(1,/(∸(3, S(3)), 3))  
    * +(1,/(∸(3, 4), 3))  
    * +(1,/(1, 3))  
    * +(1,+(1,/(∸(3, S(P<sub>3</sub><sup>2</sup>(/(0,3),0,3))), 3)))  
    * +(1,+(1,/(∸(3, S(0)), 3)))  
    * +(1,+(1,/(∸(3, 1), 3)))  
    * +(1,+(1,/(0, 3)))  
    * +(1,+(1,0))  
    * +(1,1)  
    * 2
* **Resto**:
  * Res(0,x) = 0
  * Res(n+1,x) = ∸(∸(S(n),\*(/(S(n),x),x)), x)
  * x ∸ ( (n+1) / x) * x ) ∸ (n+1)
  * `Não mostrei a recursão 'Res(n,x), n, x' pois sempre acabava usando projeção para pegar apenas um deles, podemos pular essa etapa`
    * Mas caso queira saber como que fica mostrando a projeção  
    * Res(n+1,x) = ∸(∸(S(n),\*(/(S(n),x),x)), P<sub>3</sub><sup>3</sup>(Res(n,x),n, x))
    * Note que eu sempre escolho um local qualquer para botar a projeção, apenas para respeitar o formato que tinha sido mostrado no inicio.
      * f(n+1, ẍ) = g(f(n, ẍ), n, ẍ)
  * Exemplo:
    * Res(4,3)
    * ∸(∸(S(3),\*(/(S(3),3),3)), 3)
    * ∸(∸(4,\*(/(S(3),3),3)), 3)
    * ∸(∸(4,\*(/(4,3),3)), 3)
    * ∸(∸(4,\*(2,3)), 3)
    * ∸(∸(4,6), 3)
    * ∸(2, 3)
    * 1
  * Exemplo 2:
    * Res(5,3)
    * ∸(∸(S(4),\*(/(S(4),3),3)), 3) `resolvendo o sucessor de uma vez`
    * ∸(∸(5,\*(/(5,3),3)), 3)
    * ∸(∸(5,\*(2,3)), 3)
    * ∸(∸(5,6), 3)
    * ∸(1, 3)
    * 2
  * Exemplo 3:
    * Res(6,3)
    * ∸(S(5),\*(/(S(5),3),3))
    * ∸(6,\*(/(6,3),3))
    * ∸(6,\*(2,3))
    * ∸(6,6)
    * 0
* **if else**:
  * ifelse(0,x,y) = y
  * ifelse(n+1,x,y) = x
  * Escrevendo como código
    ```
    if(n+1) {
      x
    } else {
      y
    }
    ```
    * Lembrando que em C 0 é *false* e qualquer outro número é *true*.
  * Exemplo:
    * ifelse(10,5,10)
    * 5
  * Exemplo 2:
    * ifelse(0,5,10)
    * 10
  * Exemplo 3:
    * ifelse(/(6,3),+(1,1),+(1,2))
    * ifelse(2,+(1,1),+(1,2))
    * +(1,1)
    * 2
* **Square**:
  * √(0) = 0
  * √(n+1) = ifelse(Menor(Exp(2,S(√(n))),S(n)),√(n),S(√(n)))
  * Exemplo:
    * √(4)
    * ifelse(Menor(Exp(2,S(√(3))),S(3)),√(3),S(√(3)))
    * ifelse(Menor(Exp(2,S(√(3))),4),√(3),S(√(3)))
      * √(3)
      * ifelse(Menor(Exp(2,S(√(2))),S(2)),√(2),S(√(2)))
      * ifelse(Menor(Exp(2,S(√(2))),3),√(2),S(√(2)))
        * √(2)
        * ifelse(Menor(Exp(2,S(√(1))),S(1)),√(1),S(√(1)))
        * ifelse(Menor(Exp(2,S(√(1))),2),√(1),S(√(1)))
          * √(1)
          * ifelse(Menor(Exp(2,S(√(0))),S(0)),√(0),S(√(0)))
          * ifelse(Menor(Exp(2,S(√(0))),1),√(0),S(√(0)))
          * ifelse(Menor(Exp(2,S(0)),1),√(0),S(√(0)))
          * ifelse(Menor(Exp(2,S(0)),1),0,S(√(0)))
          * ifelse(Menor(Exp(2,S(0)),1),0,S(0))
          * ifelse(Menor(Exp(2,1),1),0,S(0))
          * ifelse(Menor(Exp(2,1),1),0,1)
          * ifelse(Menor(1,1),0,1)
          * ifelse(0,0,1)
          * 1
        * ifelse(Menor(Exp(2,S(1)),2),1,S(1)) `vou começar a fazer rápido`
        * ifelse(Menor(Exp(2,2),2),1,2)
        * ifelse(Menor(4,2),1,2)
        * ifelse(1,1,2)
        * 1
      * ifelse(Menor(Exp(2,S(1)),3),1,S(1))
      * ifelse(Menor(Exp(2,2),3),1,2)
      * ifelse(Menor(4,3),1,2)
      * ifelse(1,1,2)
      * 1
    * ifelse(Menor(Exp(2,S(1)),4),1,S(1))
    * ifelse(Menor(Exp(2,2),4),1,2)
    * ifelse(Menor(4,4),1,2)
    * ifelse(0,1,2)
    * 2
* **Primo**
  * prime(0) = 0
  * prime(n) = Igual(checkprime(n,S(n)),1)
  * É primo se o número de multiplicações que formam ele for 1
    * Estou verificando se vai retornar apenas 1
  * checkprime(0,x) = 0
  * checkprime(n+1,x) = ifelse(Igual(\*(S(n),/(S(n),x)),x),S(checkprime(n,x)),checkprime(n,x))
    * Como a divisão pode retornar um inteiro incorreto, preciso verificar se é realmente um divisor
      * Igual(\*(S(n),/(S(n),x)),x)
    * Se for, soma um ao nosso calculo e depois que testar para todos os outros
    * Se não, testa os outros
      * ifelse(...,S(checkprime(n,x)),checkprime(n,x))
  * Exemplo
    * prime(5)
    * Igual(checkprime(4,S(4)),1)
    * Igual(checkprime(4,5),1)
      * checkprime(4,5)
      * ifelse(Igual(\*(S(3),/(S(3),5)),5),S(checkprime(3,5)),checkprime(3,5))
      * ifelse(Igual(\*(4,/(4,5)),5),S(checkprime(3,5)),checkprime(3,5))
      * ifelse(Igual(\*(4,2),5),S(checkprime(3,5)),checkprime(3,5))
      * ifelse(Igual(8,5),S(checkprime(3,5)),checkprime(3,5))
      * ifelse(0,S(checkprime(3,5)),checkprime(3,5))
      * checkprime(3,5)
      * ifelse(Igual(\*(S(2),/(S(2),5)),5),S(checkprime(2,5)),checkprime(2,5))
      * ifelse(Igual(\*(3,/(3,5)),5),S(checkprime(2,5)),checkprime(2,5))
      * ifelse(Igual(\*(3,2),5),S(checkprime(2,5)),checkprime(2,5))
      * ifelse(Igual(6,5),S(checkprime(2,5)),checkprime(2,5))
      * ifelse(0,S(checkprime(2,5)),checkprime(2,5))
      * checkprime(2,5)
      * ifelse(Igual(\*(S(1),/(S(1),5)),5),S(checkprime(1,5)),checkprime(1,5))
      * ifelse(Igual(\*(2,/(2,5)),5),S(checkprime(1,5)),checkprime(1,5))
      * ifelse(Igual(\*(2,3),5),S(checkprime(1,5)),checkprime(1,5))
      * ifelse(Igual(6,5),S(checkprime(1,5)),checkprime(1,5))
      * ifelse(0,S(checkprime(1,5)),checkprime(1,5))
      * checkprime(1,5)
      * ifelse(Igual(\*(S(0),/(S(0),5)),5),S(checkprime(0,5)),checkprime(0,5))
      * ifelse(Igual(\*(1,/(1,5)),5),S(checkprime(0,5)),checkprime(0,5))
      * ifelse(Igual(\*(1,5),5),S(checkprime(0,5)),checkprime(0,5))
      * ifelse(Igual(5,5),S(checkprime(0,5)),checkprime(0,5))
      * S(checkprime(0,5))
      * S(0)
      * 1
    * Igual(1,1)
    * 1
  * Exemplo 2:
    * prime(4)
    * Igual(checkprime(3,S(3)),1)
    * Igual(checkprime(3,4),1)
      * checkprime(3,4)
      * ifelse(Igual(\*(S(2),/(S(2),4)),4),S(checkprime(2,4)),checkprime(2,4))
      * ifelse(Igual(\*(3,/(3,4)),4),S(checkprime(2,4)),checkprime(2,4))
      * ifelse(Igual(\*(3,2),4),S(checkprime(2,4)),checkprime(2,4))
      * ifelse(Igual(6,4),S(checkprime(2,4)),checkprime(2,4))
      * ifelse(0,S(checkprime(2,4)),checkprime(2,4))
      * checkprime(2,4)
      * ifelse(Igual(\*(S(1),/(S(1),4)),4),S(checkprime(1,4)),checkprime(1,4))
      * ifelse(Igual(\*(2,/(2,4)),4),S(checkprime(1,4)),checkprime(1,4))
      * ifelse(Igual(\*(2,2),4),S(checkprime(1,4)),checkprime(1,4))
      * ifelse(Igual(4,4),S(checkprime(1,4)),checkprime(1,4))
      * ifelse(1,S(checkprime(1,4)),checkprime(1,4))
      * S(checkprime(1,4))
        * checkprime(1,4)
        * ifelse(Igual(\*(S(0),/(S(0),4)),4),S(checkprime(0,4)),checkprime(0,4))
        * ifelse(Igual(\*(1,/(1,4)),4),S(checkprime(0,4)),checkprime(0,4))
        * ifelse(Igual(\*(1,4),4),S(checkprime(0,4)),checkprime(0,4))
        * ifelse(Igual(4,4),S(checkprime(0,4)),checkprime(0,4))
        * ifelse(1,S(checkprime(0,4)),checkprime(0,4))
        * S(checkprime(0,4))
        * S(0)
        * 1
      * S(1)
      * 2
    * Igual(2,1)
    * 0




Primitive Recursive Function: https://en.wikipedia.org/wiki/Primitive_recursive_function  
Primitive Recursive Functions Proof: https://proofwiki.org/wiki/Category:Primitive_Recursive_Functions  

## Indução

* **Função Fibonacci [1]**    
  * Esse tipo de função requer duas bases fib(1) e fib(2), além disso a função sempre vai precisar olhar duas funções anteriores, precisamos de uma maneira de passar os valores das duas funções anteriores. Utilizamos vetores como retorno:    
  * FIB(1) = (1, 0)  
  * FIB(2) = (1, 1)  
  * FIB(n+1) = (P<sub>2</sub><sup>1</sup>(FIB(n)) + P<sub>2</sub><sup>2</sup>(FIB(n)), P<sub>2</sub><sup>1</sup>(FIB(n)))  
  * Pega o primeiro e segundo valor do FIB anterior, soma eles e deixa como sendo o primeiro valor do vetor.  
  * Pega o primeiro valor do FIB anterior, deixa ele como segundo valor.
  * Exemplo:  
    * FIB(4)
    * (P<sub>2</sub><sup>1</sup>(FIB(3)) + P<sub>2</sub><sup>2</sup>(FIB(3)), P<sub>2</sub><sup>1</sup>(FIB(3)))  
      * FIB(3)
      * (P<sub>2</sub><sup>1</sup>(FIB(2)) + P<sub>2</sub><sup>2</sup>(FIB(2)), P<sub>2</sub><sup>1</sup>(FIB(2)))  
      * (P<sub>2</sub><sup>1</sup>(1,1) + P<sub>2</sub><sup>2</sup>(1,1), P<sub>2</sub><sup>1</sup>(1,1))  
      * (1 + 1, 1)  
      * (2, 1)  
    * (P<sub>2</sub><sup>1</sup>(2,1) + P<sub>2</sub><sup>2</sup>(2,1), P<sub>2</sub><sup>1</sup>(2,1))  
    * (2 + 1, 2)  
    * (3, 2)  
* **Função Fibonacci [2]**
  * Com a função descoberta anteriormente podemos escrever uma função fibonacci que retorna apenas o primerio valor, assim reproduzindo a função fibonacci original.  
  * fib(n) = P<sub>2</sub><sup>1</sup>(FIB(n))  
  * Exemplo:  
    * fib(1)
    * P<sub>2</sub><sup>1</sup>(FIB(1))
    * P<sub>2</sub><sup>1</sup>(1,0)
    * 1
  * Exemplo 2:
    * fib(3)
    * P<sub>2</sub><sup>1</sup>(FIB(3))
    * P<sub>2</sub><sup>1</sup>(3,2)
    * 3

Course Of Values: https://en.wikipedia.org/wiki/Course-of-values_recursion

05-1:08:10
