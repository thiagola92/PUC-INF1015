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
