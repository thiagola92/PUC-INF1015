# Aula 01

# Revisando
Primeiras aulas vão ser revisão, então você precisa se lembrar da matéria de LFA.  

## Máquina de Turing
Dada a entrada 1011  
`bbbb1011bbbb`  
b normalmente é usado para blank.  
1011 nesse caso é a nossa entrada  

Estados são representados como q0, q1... qn.  
O estado final é representado por qf.  
O estado inicial começa no primeiro valor da entrada.  

Esse estados tem transições para outros estados e são representados como  
`<q0, 1, q0, 1, D>`  
Dado que você está no estado __q0__ e você está lendo __1__  
Passe para o estado __q0__ e escreva __1__ no lugar da entrada lida  
Ande para a __direita__ com o ponteiro da entrada  

OUTRO EXEMPLO  
`<q0, 1, q1, 0, D>`  
Dado que você está no estado __q0__ e você está lendo __1__  
Passe para o estado __q1__ e escreva __0__ no lugar da entrada lida  
Ande para a __direita__ com o ponteiro da entrada  

OUTRO EXEMPLO  
Faça um programa que dada uma entrada em binária, transforma no número binário seguinte  
```
<q0, 1, q0, 1, D>
<q0, 1, q0, 0, D>
<q0, b, q1, b, E>
<q1, 0, qf, 1, D>
<q1, 1, q1, 0, E>
<q1, b, qf, 1, D>
```

Fonte: https://en.wikipedia.org/wiki/Turing_machine

## Função
`f: entrada --------> saida`  
Uma função é um objeto matemática que recebe uma entrada e retorna uma saida.  
Logo tem um domínio de entrada e domínio de saida.  

Como estamos tratando de computação podemos dizer que a entrada e saida são strings.  
Pois arrays, char, objetos... Todos podem ser representados como strings.  

Nós sabemos que isso de strings é só um conforto, podemos sempre converter strings para números naturais.  
`f: naturais ---------> naturais`  
Suponha que temos um alfabeto com 3 letras: {a, b, c}  
Podemos numerar todas as strings desse alfabeto.  
vazio -> 0
a -> 1
b -> 2
c -> 3
aa -> 4
ab -> 5
ac -> 6

O calculo para conseguir a númeração da string é bem fácil, igual a decimal.  
ca = 3x3¹ + 1x3<sup>0</sup> = 10  
Explicando por partes  
**3**x3¹ + **1**x3<sup>0</sup>  
O valor o caracter (c = 3 e a = 1)  
3x**3**¹ + 1x**3**<sup>0</sup>  
Tamanho do alfabeto {a,b,c} = 3 letras  
3x3**¹** + 1x3<b><sup>0</sup></b>  
A casa em que se encontra (começando a contagem da esquerda)  

# Tese de Church
(é uma tese justamente pois não tem como se provar)

> Uma função é computável se somente se é λ-definível  

É equivalente a

> Uma função é computável se somente se é computável por máquina de Turing

O que é um função computável?  
É uma função que consegue receber outra função como entrada e fazer o que aquela função faria.  

O que é uma máquina ser programável?  
Uma máquina programável é uma máquina que você pode usar para programar.  

Computable Function: https://en.wikipedia.org/wiki/Computable_function   
