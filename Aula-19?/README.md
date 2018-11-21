# Machtey e Young

## A General Theory of Algorithms

Família Abstrata de Algoritmos  
( ϕ <sub>i</sub> ) <sub>i ∈ N</sub>  
ϕ <sub>i</sub> são funções parciais  
ϕ <sub>i</sub> : ℕ → ℕ  

* 1)
  * {f / f é parcial recursiva} ⊆ 𝕌 <sub>i ∈ N</sub> {ϕ <sub>i</sub>}
* 2)
  * ∃<sub>M</sub> ∈ ℕ
    * ϕ <sub>U</sub> é parcial recursiva
    * ϕ <sub>U</sub>(<i,x>) = ϕ <sub>i</sub>(x)
      * Basicamente essa função recebe o programa i e o dado x
      * Depois roda o como se fosse o programa i no dado de x
      * Em outras palavras, uma máquina que simula outra
        * Isso é uma função universal
* 3)
  * ∃<sub>C</sub> : ℕxℕ → ℕ e recursiva
    * V<sub>i, j</sub>
    * ϕ<sub>C (i,j)</sub> = ϕ<sub>j</sub> ∘ ϕ<sub>i</sub>
      * A composição de duas funções, pegar os dados finais de uma função e botar em outra função  
      * Outra maneira de ver é
        * ϕ <sub>C (f,g)</sub>(x)
          * f vai pegar x e gerar um resultado
          * g vai pegar o resultado e gerar outro resultado
          * Se tivesse mais funções, iria continuar reutilizando o resultado da anterior
          * g(f(x))
        * (ϕ <sub>g</sub> ∘ ϕ<sub>f</sub>)(x)
          * ϕ<sub>g</sub>(ϕ<sub>f</sub>(x))
          * Você cola o resultado da f(x) na entrada da g(x)

Universal function: https://en.wikipedia.org/wiki/Universal_function

---

**Fato**: Máquina de Turing ( ϕ <sub>M</sub> ) é uma Família Abstrata de Algoritmos (FAA)  

**Prop**:  
Existe s : ℕxℕ → ℕ  
s é recursiva tal que ϕ <sub>s (i,x)</sub>(y) = ϕ <sub>i</sub>(<x,y>)  

* Considere um programa i que recebe dois valores  
  * ϕ <sub>i</sub>(<x,y>)  
* Você pode construir outro programa que deixa o primeiro valor do programa já instanciado, ou seja, o valor x já instanciado  
* Esse programa i com x já instanciado só recebe um valor (y)   
  * ϕ <sub>s (i,x)</sub>(y)  

Exemplo:  
ϕ <sub>i</sub>(<x,y>)  
```
INPUT X Y
OUTPUT Z

  <COMANDOS>

END
```
ϕ <sub>s (i,n)</sub>(y)  
```
INPUT Y
OUTPUT Z
  X ← n
  <COMANDOS>

END
```
Esse código funciona igual ao ϕ <sub>i</sub>(<x,y>) quando x = n  
ϕ <sub>i</sub>(<n,y>) = ϕ <sub>s (i,n)</sub>(y)  

**Prova**:  
Sendo P uma função de parificação  
P(Y) = <0, y>   
Uma função que recebe um par e devolve um outro par com x incrementado  
Q(<x,y>) = <x+1,y>  
Dessa maneira você consegue representar qualquer par de números.  

ϕ <sub>i</sub>(<x,y>) = ϕ <sub>u</sub>(i, <x,y>)    
ϕ <sub>i</sub>(<x,y>) = ϕ <sub>s (i,x)</sub>(y)  

*Obs: ϕ <sub>u</sub> é a função universal*   

P e Q são funções recursivas então  
∃p,q tal que ϕ <sub>p</sub> = P e ϕ <sub>q</sub>  = Q  

Isso é verdade pois qualquer função que faça recursiva tem implementada em família abstrata de algoritmos.  

R(0) = q  
R(n+1) = c(R(n),p)  `composição de R(n) com p`  

* Se você escolher R(0)  
  * R(0) = q  
  * ϕ <sub>q</sub> = Q
    * ϕ <sub>q</sub>(x) = Q(x)
* Se você escolher R(1)  
  * R(1) = c(R(0),p) = c(q,p)  
  * ϕ <sub>c(q,p)</sub> = ϕ <sub>p</sub> ∘ ϕ <sub>q</sub>    
    * ϕ <sub>p</sub> ∘ ϕ <sub>q</sub>(x) = P(Q(x))    

ϕ <sub>R(x)</sub>(y) = <x,y>   

ϕ <sub>R(0)</sub>(y) = ϕ <sub>q</sub>(y) = Q(y) = <0,y>   
ϕ <sub>R(n+1)</sub>(y) = ϕ <sub>c(R(n),p)</sub>(y) = ϕ <sub>p</sub> ∘ ϕ <sub>R(n)</sub>(y) = ϕ <sub>p</sub>( ϕ <sub>R(n)</sub>(y) ) = <n+1,y>  

Com isso mostramos que é recursiva  
ϕ <sub>i</sub>(<x,y>)  
ϕ <sub>i</sub>( ϕ <sub>R(x)</sub>(y) )  
ϕ <sub>c(R(x),i)</sub>(y)  
c(R(x), i) = s(i, x)  
Logo s é recursiva  

## Teorema da Traução
Tudo que é computável é turing computável  

**Prop**:  
Sejam ϕ <sub>i</sub> e Ψ <sub>i</sub> duas Famílias Abstratas de Algoritmos, i ∈ ℕ  
Então existe t : ℕ → ℕ recursiva, tal que ∀i  
ϕ <sub>i</sub> = Ψ <sub>t(i)</sub>  

Existe um programa i em ϕ e  
Existe um programa em Ψ que faz a mesma coisa,  
Você pode descobrir esse programa pela função t.  

Em outras palavras, existe uma função t que liga o programa i em ϕ com um programa de Ψ  

**Prova**:  
(Evidência forte para tese church-turing)  

ϕ <sub>i</sub>(x) = ϕ <sub>u</sub>(<i,x>)  
Como ϕ <sub>u</sub> é parcial recursiva (item 2 sobre FAA)  
Então existe u' ∈ ℕ, tal que  
ϕ <sub>u</sub>(x) = Ψ <sub>u'</sub> (item 2 sobre FAA)  
ϕ <sub>i</sub>(x) = ϕ <sub>u</sub>(<i,x>) = Ψ <sub>u'</sub>(<i,x>) = Ψ <sub>s(u',i)/t(i)</sub>(x)  

Como u' é a função universal de Ψ,  
Você pode fazer Ψ rodar o programa i com  
Ψ <sub>s(u',i)</sub> `s é a função composição se não me engano`  
Como <sub>s(u',i)</sub> é justamente a função que roda o programa i,  
Essa é a função t que procuravamos que rodaria o programa ϕ <sub>i</sub>  
Ψ <sub>s(u',i)</sub> = Ψ <sub>t(i)</sub>  

ϕ <sub>i</sub>(x) = ϕ <sub>u</sub>(<i,x>) = Ψ <sub>u'</sub>(<i,x>) = Ψ <sub>s(u',i)/t(i)</sub>(x) = Ψ <sub>t(i)</sub>(x)  
Ou seja  
ϕ <sub>i</sub>(x) = Ψ <sub>t(i)</sub>(x)   

## Teorema de Recursão  

Se ϕ <sub>i</sub> (i ∈ ℕ) uma FAA's e f uma função recursiva, então existe p ∈ ℕ, tal que  
ϕ <sub>p</sub> = ϕ <sub>f(p)</sub>  

Pensando em f como uma função que recebe um código e devolve um outro código, então existe um programa que é inalterado quando passado por essa função  

A função fatorial  
fat(0) = 1  
fat(n) = n * fat(n-1)  

f(fat) = fat  
ϕ <sub>f(fat)</sub> = ϕ <sub>fat</sub>   

---

Seja f parcial recursiva  
Quantas máquinas de turing diferente nós temos que implementam f?  
Infinitas, pois você pode sempre acrescentar código inutil  

Para máquina de turing, sabemos que ∃m tal que  
ϕ <sub>m</sub> = f  
|{ m / ϕ <sub>m</sub> = f }| = |ℕ|  

## Teorema da Tradução Injetiva
**Prop**:  
Sejam ϕ <sub>i</sub> e Ψ <sub>i</sub> duas Famílias Abstratas de Algoritmos, i ∈ ℕ  
Então existe t : ℕ → ℕ recursiva, tal que ∀i  
ϕ <sub>j</sub> = Ψ <sub>t(j)</sub> = Ψ <sub>s(i,j)</sub>   

|F<sub>i</sub>| = |{ j / ϕ <sub>i</sub> }| = |ℕ|  

**Prova?**:  
(Evidência forte para tese church-turing)  

Máquina de turing = Ψ <sub>i</sub> (i ∈ ℕ)  
Existe PAD recursiva, tal que ∀i,∀n  
Ψ <sub>PAD(i, n)</sub> = Ψ <sub>i</sub>  
e PAD(i, n) ≠ PAD(i, n'), se n = n'  

PAD é uma função que recebe uma função i e um número n de estados para acrescentar a função i, PAD devolve o mesmo resultado que a função i iria retornar normalmente.  
Basicamente PAD é uma função que acrescenta estados que não alteram o comportamento da função i.  
Imagine acrescentar na função i um estado que tudo que faz é apontar para si mesmo novamente ou coisa do tipo...  

Exemplo:  
g(x) = x, recebe x e retorna x  
g(f(x)) = f(x), recebe f(x) e retorna mesma coisa que f(x) retornaria  

PAD acrescenta n estados inuteis, ou seja, PAD(f,3)  
PAD(f,3) = g(g(g(f(x)))) = g(g(f(x))) = g(f(x)) = f(x)  

## Função injetiva
Seja ϕ <sub>h</sub> (h : ℕ → ℕ), h recursiva  
Então existe i ∈ ℕ tal que  
ϕ <sub>h(x)</sub> = ϕ <sub>s(i,x)</sub>  
E se s(i,x) = s(i,x') então x = x'  
Existe i tal que  

* ϕ <sub>s(j,y)</sub> = 0, se
  * ∃k < j [s(i,k) = s(i,j)]  
* ϕ <sub>s(j,y)</sub> = 1, se
  * ∀k < j [s(i,k) ≠ s(i,j)]
  * ∃k ≤ y [k > j ^ s(i,k) = s(i,j)]  
* ϕ <sub>s(j,y)</sub> = ϕ <sub>h(j)</sub>(y), caso contrário

Ou seja  

ϕ <sub>s(j,y)</sub> =
* 0
  * Procura de 0 até j-1 alguém que de o mesmo resultado que s(i,j)  
* 1
  * Se ninguém de 0 até j-1 da o mesmo resultado que s(i,j)
  * Procura entre j e y alguém que de o mesmo resultado que s(i,j)  
* ϕ <sub>h(j)</sub>(y)
  * Caso nenhum dos casos acima, roda h que é uma função recursiva que sempre para.  


A função h é uma recursiva qualquer que altera o programa.   
A função s é injetiva no segundo argumento, só existe uma combinação de i e x que levam a um valor.  

Página 112 do Livro no Site  

## Teorema do Isomorfismo de Rogers

42:29 aula-20

# Observação

**Função Recursiva Total**: Uma função que sempre termina  

**Função Recursiva Primitiva**: Uma função onde o unico tipo de loop que existe são aqueles que executam uma quantidade pré determinada.  
`for 1 to 10 do { ... }`  

Difference between total recursive and primitive recursive functions: https://math.stackexchange.com/questions/75296/what-is-the-difference-between-total-recursive-and-primitive-recursive-functions
