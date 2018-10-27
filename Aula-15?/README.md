# λ-Calculus(não-tipado)

Sintaxe: Como são as expressões λ   
Semântica: O que quer dizer uma expressão λ  

Um λ-termo é:  
1) **Variável**: x, y, etc.  
2) **Aplicação**: e<sub>1</sub>, e<sub>2</sub>, ..., e<sub>n</sub>  
3) **Abstração**: λx.e  

λ-Calculus é associativo à esquerda, ou seja, se dois operadores tiverem o mesmo nível de preferência você resolve primeiro o operador a esquerda.  
`30 / 10 / 2  =>  (30 / 10) / 2  =>  3 / 2  =>  1,5`  

**Resolvendo λ-Calculus**:  
Imagine que você tem a seguinte expressão `λxλyλz.zyxz`  
É como se fosse uma função, você recebe valores e substitui as variáveis  
Se você tivesse recebendo **e<sub>1</sub>** como valor:  
(λxλyλz.zyxz)**e<sub>1</sub>**  
Você vai pegar o primeiro lambda, ver qual a variável e substituir a exitência dela por **e<sub>1</sub>**  
(λxλyλz.zyxz) **e<sub>1</sub>**  
(λyλz.zy **e<sub>1</sub>** z)   
Se você tivesse recebido vários valores? Continue executando em ordem os lambdas  
(λxλyλz.zyxz) **e<sub>1</sub>** **e<sub>2</sub>** **e<sub>3</sub>**  
(λyλz.zy **e<sub>1</sub>** z) **e<sub>2</sub>** **e<sub>3</sub>**  
(λz.z **e<sub>2</sub>** **e<sub>1</sub>** z) **e<sub>3</sub>**  
(**e<sub>3</sub>** **e<sub>2</sub>** **e<sub>1</sub>** **e<sub>3</sub>**)  
**e<sub>3</sub>** **e<sub>2</sub>** **e<sub>1</sub>** **e<sub>3</sub>**  
Solução: **e<sub>3</sub>** **e<sub>2</sub>** **e<sub>1</sub>** **e<sub>3</sub>**  



### Booleans
Vamos fazer que os tipos booleanos são funções de 2 parâmetros, onde se for true retorna o primeiro, se false retorna o segundo  

T = λxλy.x  
F = λxλy.y  

Exemplo:  
True  
(λxλy.x)b<sub>1</sub>b<sub>2</sub>  
(λy.b<sub>1</sub>)b<sub>2</sub>  
(b<sub>1</sub>)  
b<sub>1</sub>

False  
(λxλy.y)b<sub>1</sub>b<sub>2</sub>  
(λy.y)b<sub>2</sub>  
(b<sub>2</sub>)  
b<sub>2</sub>

### Not
A idéia é simples, você vai receber um T ou F e você tem que retorna o oposto.  
Como T retorna sempre o primeiro parâmetro, vamos deixar F como sendo o primeiro.  
Como F retorna sempre o segundo parâmetro, vamos deixar T como sendo o segundo.  

Not = λx.xFT  

Exemplo:  
Not True  
(λx.xFT)T  
(TFT) `Você pode expamdir T e F mas você já sabe o que eles fazem`   
(F)  
F

Not False  
(λx.xFT)F  
(FFT)  
(T)  
T

Exemplo expandindo:  
Not True  
(λx.xFT)T  
(TFT)   
((λxλy.x)FT)   
((λy.F)T)   
((F))   
(F)  
F  

### And
Você vai receber dois booleans e decidir se é true ou false.  

Uma maneira simples de pensar é: se o primeiro valor for true retorne o segundo valor, se não retorna false.  
Se você receber true e um outro boolean, você sabe que a resposta agora depende do segundo boolean então você pode já retornar ele.  
Caso você receber false e um outro boolean, você sabe que já pode retornar false e não precisa olhar o segundo.  


And = λxλy.xyF  

Exemplo:  
And T F  
(λxλy.xyF)TF  
(λy.TyF)F  
(TFF)  
(F)  
F  

And F T  
(λxλy.xyF)FT  
(λy.FyF)T  
(FTF)  
(F)  
F  

And T T  
(λxλy.xyF)TT  
(λy.TyF)T  
(TTF)  
(T)  
T  

### Or
Você vai receber dois booleans e decidir se é true ou false.  

Se o primeiro for false, olhe o segundo, se não true.  

Or = λxλy.xTy  

Exemplo:  
Or F T  
(λxλy.xTy)FT  
(λy.FTy)T  
(FTT)  
(T)  
T  

Or T T  
(λxλy.xTy)TT  
(λy.TTy)T  
(TTT)  
(T)  
T  

Or F F  
(λxλy.xTy)FF  
(λy.FTy)F  
(FTF)  
(F)  
F  

### Numerais de Church
Numerais podem ser representados por n aplicações de f.  
n = λf. f <sup>n</sup>  
0 seria nenhuma ocorrência de f, 1 seria uma ocorrência de f...  

n é um número qualquer  

0 = λfλn.n `zero é uma função sobre um número que é justamente o número`  
1 = λfλn.fn  
2 = λfλn.f(fn)  
3 = λfλn.f(f(fn))  
**. . .**  

### Sucessor
Recebe um número e retorna o número seguinte, ou seja, adiciona um f.

Suc = λxλfλn.f((xf)n)

Exemplo:  
Suc 0  
(λxλfλn.f((xf)n))0  
λfλn.f((0f)n) `expandindo 0 para a definição vista a cima`  
λfλn.f(((λfλn.n)f)n)  
λfλn.f((λn.n)n)  
λfλn.f(n)  
λfλn.fn `lembrando que isso é a definição de 1`  

Suc 1  
(λxλfλn.f((xf)n))1  
λfλn.f((1f)n)  
λfλn.f(((λfλn.fn)f)n)  
λfλn.f((λn.fn)n)  
λfλn.f(fn)  `lembrando que isso é a definição de 2`  

### Add
Recebe dois números e retorna a soma deles.  
Como aplicar x vai trazer todos os f's dele e

Add = λxy.x Suc y  
`λxy == λxλy`  

Exemplo:  
Add 1 2  
(λxy.x Suc y)1 2  
1 Suc 2  `agora você vai ver o poder dos númerais`  
(λfλn.fn)Suc 2  
Suc 2   
3   

Se o número fosse 2 ou 3 ou 4... Iria copiar a função Suc para todos os f que tem o númeral.

Add 2 2  
(λxy.x Suc y)2 2  
2 Suc 2   
(λfλn.f(fn))Suc 2  
(Suc(Suc 2))   
Suc(Suc 2)   
Suc(3)   
4   

### Mul
Uma multiplicação começa com 0 e vai somando x y-vezes.  

Mul = λxy.x (Add y) 0  

Exemplo:  
Mul 2 2  
(λxy.x (Add y) 0) 2 2  
2 (Add 2) 0   
(λfλn.f(fn)) (Add 2) 0   
(Add 2)((Add 2)0)   
(Add 2)(Add 2 0)   
(Add 2)2   
Add 2 2   
4   

Mul 2 0  
(λxy.x (Add y) 0) 2 0  
2 (Add 0) 0  
(λfλn.f(fn)) (Add 0) 0  `note o pq botamos 0 no final da função`
(Add 0)((Add 0)0)    
(Add 0)(Add 0 0)    
(Add 0) 0   
Add 0 0   
0   

Mul 0 2  
(λxy.x (Add y) 0) 0 2  
0 (Add 2) 0  
(λfλn.n) (Add 2) 0  
0  

### Exp
Uma exponencial começa em 1 e vai multiplicando por x y-vezes.  

Exp = λxy.x (Mul y) 1  

Exemplo:  
Exp 2 1  `note que é 1²`  
(λxy.x (Mul y) 1) 2 1  
2 (Mul 1) 1  
(Mul 1) (Mul 1) 1  
(Mul 1) Mul 1 1  
(Mul 1) 1  
Mul 1 1  
1  

Exp 1 2  `note que é 2¹`  
(λxy.x (Mul y) 1) 1 2  
1 (Mul 2) 1   
Mul 2 1   
2   

## Substituição  
Free Variables (FV)  
<sub>[ Variáveis Livres ]</sub>  

1) FV(x) = {x}  
2) FV(e<sub>1</sub> e<sub>2</sub>) = FV(e<sub>1</sub>) ∪ FV(e<sub>2</sub>)  
3) FV(λx.e) = FV(e) - {x}  

Termo fechado: sem variáveis livres (FV(t) = ∅)  
**λxλy.x(yx(y y)x)y**  

Combinador é uma λ-abstração com FV(t) = ∅  
Notação **e<sub>1</sub>[x -> e<sub>2</sub>]**  

**x[x -> e] = e**  
ou  
**y[x -> e] = y**  

**(e<sub>1</sub> e<sub>2</sub>)[x -> e] = (e<sub>1</sub> [x -> e])(e<sub>2</sub> [x -> e])**  
Provando:  
((λx.x)(λx.yx))[x -> e] = (λx.e)(λx.ye)  
(λx.x)[x -> e] (λx.yx)[x -> e] = (λx.e)(λx.ye)

**(λx.e<sub>1</sub>)[x -> e] = λx.e<sub>1</sub>**  

**(λy.e<sub>1</sub>)[x -> e<sub>2</sub>] = λy.(e<sub>1</sub>[x -> e<sub>2</sub>])**    
Obs: y ∉ FV(e<sub>2</sub>)  

Provando:  
(λy.xy)[x -> e] = λy.ey  
(λy.(xy[x -> e])) = λy.ey    


**(λy.e<sub>1</sub>)[x -> e<sub>2</sub>] = λz.(e<sub>1</sub>[y -> z])[x -> e<sub>1</sub>]**  
Onde z ∉ (FV(e<sub>2</sub>) ∪ FV(e<sub>1</sub>) ∪ {x})  

## Semântica

α - [alpha] - propaga substituição em λ-abstração  
β - [beta] - aplicação + substituição  
η - [eta] - extensionalidade  

#### α-redução  
(λx.e) ▻<sub>α</sub> λy(e[x -> y])  
x ≠ y  

Basicamente você está substituindo uma variável x por outra variável y.  
Agora sua função é em cima de y.  

#### β-redução
(λx.e<sub>1</sub>)e<sub>2</sub> ▻<sub>β</sub> e<sub>1</sub>[x -> e<sub>2</sub>]  

Basicamente você está substituindo uma variável x dentro de e<sub>1</sub> por e<sub>2</sub>.  

#### η-redução
Pares < 10 = {2, 4, 6, 8} `extencional`   
{x ∈ N | ∃k, 2k = x ^ x < 10} `intencional`  

(λx.e<sub>1</sub>x) ▻<sub>η</sub> e<sub>1</sub>  

Basicamente você retira a variável x.  

Notação:  
▻: 1 passso de redução  
▻<sup>\*</sup>: * passos de redução  

Redex:  
(λx.e<sub>1</sub>)e<sub>2</sub>  
Por que é redex? Pois essa função pode ser **red**uzida, você troca e<sub>1</sub> por e<sub>2</sub> e retira lambda.  

### Teorema Church-Rosser (Diamante)
Se e ▻<sup>\*</sup> e' && e ▻<sup>\*</sup> e'',  
então ∃e<sub>1</sub> tal que e' ▻<sup>\*</sup> e<sub>n</sub> && e'' ▻<sup>\*</sup> en
