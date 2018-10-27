### 1a
Como y é indiferente nessa função podemos ignora-lo.  
f(x,0) = 1  
f(x,n+1) =  Exp(f(x,n),x)  

Considerando que conseguimos fazer adição, multiplicação e exponencial como já resolvidos.  

* Exemplo:  
  * f(2,3)
  * Exp(f(2,2),2)
  * Exp(Exp(f(2,1),2),2)
  * Exp(Exp(Exp(f(2,0),2),2),2)
  * Exp(Exp(Exp(1,2),2),2)
  * Exp(Exp(2,2),2)
  * Exp(4,2)
  * 16
* Exemplo 2:
  * f(0,3)
  * Exp(f(0,2),0)
  * Exp(Exp(f(0,1),0),0)
  * Exp(Exp(Exp(f(0,0),0),0),0)
  * Exp(Exp(Exp(1,0),0),0)
  * Exp(Exp(1,0),0)
  * Exp(1,0)
  * 1

### 1c
Calcular o máximo entre dois números pode ser feito pelo seguinte calculo  
x ∸ (n+1) + n+1  

Max(0,x) = x  
Max(n+1,x) = +(∸(S(n), x), S(n))  

Isso considerando que já temos adição e monus.  

* Exemplo:
  * Max(2,3)  
  * +(∸(S(1), 3), S(1))  
  * +(∸(2, 3), S(1))  
  * +(∸(2, 3), 2)  
  * +(1, 2)  
  * 3  
* Exemplo 2:
  * Max(3,2)  
  * +(∸(S(2), 2), S(2))
  * +(∸(3, 2), S(2))
  * +(∸(3, 2), 3)
  * +(0, 3)
  * 3


Para calcular o maior entre dois basta repetir o mesmo processo.  

Max(0,y,z) = Max(y,z)  
Max(n+1,y,z) = Max(S(n), Max(y,z))  

* Exemplo:
  * Max(1,2,3)
  * Max(S(0), Max(2,3))
  * Max(1, Max(2,3))
  * Max(1, 3)
  * 3

### 1d
Estou considerando que conseguio fazer **if else**   

* ifelse(0,x,y) = y  
* ifelse(n+1,x,y) = x   

Que consigo verificar se é **menor** que x  

* Menor(0,x) = 0  
* Menor(n+1,x) = !sn(+(Maior(S(n),x),Igual(S(n),x)))  

Minha verificação de menor utiliza **maior** e **igual**   

* Maior(0, x) = 0  
* Maior(n+1, x) = !sn(MenorIgual(S(n), x))  


* Igual(0, x) = !sn(x)  
* Igual(n+1, x) = !sn(DifAbs(S(n), x))  

Minha verificação de maior utiliza **menor igual**, minha verificação de igual utiliza **diferença absoluta**  

* MenorIgual(0, x) = !sn(x)  
* MenorIgual(n+1, x) = !sn(∸(S(n), x))  


* DifAbs(0, x) = x
* DifAbs(n+1, x) = +(∸(S(n), x), ∸(x, S(n)))  

**Monus**, **adição** e **teste de zero** são considerados como resolvidos  

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

### 1b

* prime(0) = 0
* prime(n) = Igual(checkprime(n,S(n)),1)

* checkprime(0,x) = 0
* checkprime(n+1,x) = ifelse(Igual(\*(S(n),/(S(n),x)),x),S(checkprime(n,x)),checkprime(n,x))

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
