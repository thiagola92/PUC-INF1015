# Programação Imperativa (PL)

### Sintaxe
Primeiro se declara a entrada do programa  
`INPUT X1,X2,X3...Xn`  
Segundo variáveis a retornar  
`OUTPUT Y1,Y2,Y3...Yn`  
Terceiro um conjunto de comandos, podendo ser qualquer um dos seguintes comandos  
`LOOP X DO <comandos> END`  
`INC(X)`  
`ZERO(X)`  
`COPY(X)`  
Por ultimo finaliza o programa com o comando end  
`END`  

`LOOP` é o único que recebe comandos, os outros 3 recebem variáveis.  

### Exemplo
```
INPUT X1,X2,X3
OUTPUT Y1

  ZERO(X1)
  INC(X2)
  COPY(Y1,X3)

  LOOP X2 DO
    INC(X1)
  END

END
```

Podemos facilitar a escrita utilizando setas para 3 das operações básicas.
```
INPUT X1,X2,X3
OUTPUT Y1

  X1 ← 0
  X2 ← X2 + 1
  Y1 ← X3

  LOOP X2 DO
    X1 ← X1 + 1
  END

END
```

## Primitiva Recursiva
Queremos provar que Programação Imperativa faz tudo que Primitiva Recursiva e vice-versa.  
Para isso vamos reproduzir as funções básicas em PL.  

**Zero**  
```
INPUT X
OUTPUT Y
  Y ← 0
END
```

**Sucessor**  
```
INPUT X
OUTPUT Y
  X ← X + 1
  Y ← X
END
```

**Projeção**  
```
INPUT X0,X1,X2,X3...Xn
OUTPUT Y
  Y ← Xk
END
```

## Operações Básicas

**Adição**
```
INPUT X1, X2
OUTPUT Y

  Y ← X1

  LOOP X2 DO
    Y ← Y + 1
  END
END
```

`ADD(X,Y)`  
Açúcar sintático: `X + Y`  

**Multiplicação**
```
INPUT X1, X2
OUTPUT Y

  Y ← 0

  LOOP X2 DO
    LOOP X1 DO
      Y ← Y + 1
    END
  END
END
```

`MULT(X,Y)`  
Açúcar sintático: `X * Y`  

**Exponenciação**
```
INPUT X1, X2
OUTPUT Y

  Y ← 1

  LOOP X2 DO
    Y ← MULT(Y,X1)
  END
END
```

`EXP(X,Y)`  
Açúcar sintático: `X ^ Y`  

**Predecessor**
```
INPUT X
OUTPUT Z

  Y ← 0
  Z ← 0

  LOOP X DO
    Z ← Y
    Y ← Y + 1
  END
END
```

`PRED(X)`  
Açúcar sintático: `X - 1`  

**Subtração limitada (Monus)**  
Lembrando que monus não deixa o valor ir abaixo de 0.  
```
INPUT X1, X2
OUTPUT Y

  Y ← X1

  LOOP X2 DO
    Y ← PRED(Y)
  END
END
```

`MONUS(X,Y)`  
Açúcar sintático: `X ∸ Y`  

**if else**   
```
INPUT X1, X2, X3
OUTPUT Y

  Z ← 0
  Z ← Z + 1

  LOOP X1 DO
    X1 ← 0
    Z ← 0
    Y ← X2
  END

  LOOP Z DO
    Y ← X3
  END
END
```

`IFELSE(X,Y,Z)`  


32:25
