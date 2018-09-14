# About

Esse exercício foi fazer uma máquina de turing que substituísse o primeiro acontecimento de uma string `w1` dentro da string `w3` pela string `w2`.  

Alfabeto de entrada é apenas {a, b, $}.  
O sinal de dolar ($) é usado para separar as strings.  
Considere brancos na esquerda e direita da entrada  
Exemplo: `aab$bba$aaabbaa`  

Em outras palavras  
`w1$w2$w3`  
`w1` string a ser procurada  
`w2` string que substituira a `w1`  
`w3` string onde vai ser procurado `w1` para trocar por `w2`  

### Exemplos  
Entrada => `ab$ba$aab`  
Saida => `ab$ba$aba`

Entrada => `ab$ba$abab`  
Saida => `ab$ba$baab`  

Entrada => `ab$b$abab`  
Saida => `ab$b$bab`  

Entrada => `a$bb$abab`  
Saida => `a$bb$bbbab`  
