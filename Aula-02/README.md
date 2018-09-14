# Máquina de Turing Universal
Máquina de Turing que consegue executar outra Máquina de Turing.  

Escrevendo de outra maneira, temos a máquina de turing universal `U`, uma máquina de turing `M` e os dados `d`.  
A máquina `U` ao receber `M` e `d` tem que conseguir executar a mesma tarefa que a máquina `M` quando recebe `d`.  
`U(M$d) = M(d)`  

Os parênteses são para mostrar o que a máquina está recebendo como entrada.  
`$` é apenas um separador, para saber quando a máquina acaba e os dados começam. É para mostrar que a máquina `U` está recebendo duas entradas.  

Como pode ver, ambos tem que dar o mesmo resultado já que `U(M$d)` é igual a `M(d)`.  
`U(M$d) = M(d)`   

Suponha que a máquina `M` tenha n estados {`q1, q2, q3, q4, ..., qn`}  
Lembre que o alfabeto que uma máquina possui é **finito** e a quantidade de estados de uma máquina pode ter é **infinito**.
Não tem como a máquina de turing universal possuir um símbolo para cada estado que uma máquina de turing pode ter (pois ela pode ter infinitos estados).  
Para que a máquina `U` possa trabalhar com os estados da máquina `M` é preciso converter o símbolo desses estados para um dentro do alfabeto da máquina.  

Suponha que a máquina `M` tem os estados {`q1, q2, q3, q4`} e o alfabeto {`1, 2, 3, 4, 5, 6`}.  
Podemos converter o símbolo dos estados para "Q concatenado com uma cadeia unária que representa o estado". Exemplo:  
```
q1 = Q1
q2 = Q11
q3 = Q111
q4 = Q1111
```
Podemos converter o alfabeto para "S concatenado com uma cadeira unária que representa o símbolo do alfabeto". Exemplo:  
```
1 = S1
2 = S11
3 = S111
4 = S1111
5 = S11111
6 = S111111
```

Com essa conversão podemos representar as transições feitas de estados.  
Uma transição de uma máquina `<q1, 1, q2, 2, D>` seria representada como  
`Q1S1Q11S11D`  

Como exemplo, suponha que temos a seguinte máquina de turing  
Estados {`q1, q2, q3`}, sendo `q3` o estado final    
Alfabeto {`1, 2`}  
Transições   
```
<q1, 1, q1, 1, D>
<q1, 2, q2, 1, D>
<q2, 1, q1, 2, D>
<q2, 2, q3, 2, D>
```

Após converter os estados e alfabetos  
Estados {`Q1, Q11, Q111`}  
Alfabeto {`S1, S11`}
Transições  
```
<Q1, S1, Q1, S1, D>
<Q1, S11, Q11, 1, D>
<Q11, S1, Q1, S11, D>
<Q11, S11, Q111, S11, D>
```

Agora a máquina de turing universal consegue receber essas transições como entrada.  
```
U(M$d)
U(Q1S1Q1S1DQ1S11Q111DQ11S1Q1S11DQ11S11Q111S11D$d)
```

Considere a entrada `112122`, podemos também converter a entrada.  
```
U(M$d)
U(Q1S1Q1S1DQ1S11Q111DQ11S1Q1S11DQ11S11Q111S11D$d)
U(Q1S1Q1S1DQ1S11Q111DQ11S1Q1S11DQ11S11Q111S11D$S1S1S11S1S11S11)
```


1:06:00
