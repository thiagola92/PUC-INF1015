# Machtey e Young

## A General Theory of Algorithms

Família abstrata de algoritmos  
( ϕ <sub>i</sub> ) <sub>i ∈ N</sub>  
ϕ <sub>i</sub> são funções parciais  
ϕ <sub>i</sub> : ℕ → ℕ  

* 1)
  * {f / f é parcial recursiva} ⊆ 𝕌 <sub>i ∈ N</sub> {ϕ <sub>i</sub>}
* 2)
  * ∃<sub>M</sub> ∈ ℕ
    * ϕ <sub>M</sub> é parcial recursiva
    * ϕ <sub>M</sub>(<i,x>) = ϕ <sub>i</sub>(x)
      * Basicamente essa função recebe o programa i e o dado x
      * Depois roda o como se fosse o programa i no dado de x
      * Em outras palavras, uma máquina que simula outra
        * Isso é uma função universal
* 3)
  * ∃<sub>C</sub> : Wxℕ → ℕ e recursiva
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

ϕ <sub>i</sub>(<x,y>) = ϕ <sub>0</sub>(i, <x,y>)  
ϕ <sub>i</sub>(<x,y>) = ϕ <sub>s (i,x)</sub>(y)  

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

### Evidência forte para tese church-turing  
**Prop**:  
Sejam
27:54 computabilidade-19
