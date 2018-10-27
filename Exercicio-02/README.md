1a)
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

1c)
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

2)
