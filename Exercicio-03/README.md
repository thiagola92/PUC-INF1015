# 2
F seria uma função que altera o programa para retornar o oposto  
Se retorna TRUE, agora retorna FALSE  
Se retorna FALSE, agora retorna TRUE  
```lua
function F(input)
  return not input()
end
```

Programa i retorna sempre TRUE  
ϕ <sub>i</sub>(n) = TRUE  
```lua
function i(n)
  return true
end
```

F(i) = FALSE  
F(F(i)) = TRUE = ϕ <sub>i</sub>(n)  

# 4
Não  

ϕ <sub>i</sub>(i) = 1  
Se o programa i receber ele mesmo como entrada e retorna 1, então 1  
Se o programa i receber ele mesmo como entrada e não retornar 1, então 0  

Para isso ocorrer, i tem que ser um programa capaz de se reconhecer.  
