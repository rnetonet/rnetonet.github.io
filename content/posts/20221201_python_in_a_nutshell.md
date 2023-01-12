+++
title = "Notas sobre o livro Python Distilled"
date = "2022-12-01"
draft = false
+++


# Conceitos Básicos

## Executando

Python é uma linguagem interpretada. 

O download do interpretador pode ser feito em [www.python.org](https://www.python.org).

Ao executar o interpretador sem parâmetros, é apresentado um shell que permite a execução instantânea de código:

```python
$  python
Python 3.8.10 (default, Jun 22 2022, 20:18:18) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello World")
Hello World
>>> 
```

Servindo, inclusive, como calculadora:

```python
>>> 2 + 2
4
>>> 
```

**Apenas** neste modo interativo, o **_** (*underscore*) armazena automaticamente o último valor computado:

```python
>>> 2 + 2
4
>>> _
4
>>> _ * 3
12
>>> _
12
>>> 
```

Para sair, digite `quit()` ou use os atalhos `CTRL + D` (Linux e MacOS) / `CTRL + Z` (Windows).

```python
>>> quit()
```

## Programas Python

Programas em Python devem ser escritos em arquvos textos simples com codificação **UTF-8** e com extensão **.py** (recomendação).

```python
# exemplo.py
print("Hello World") # Comentário
```

No exemplo, `#` denota um comentário (texto informativo ignorado pelo interpretador) que se estende até o final da linha.

Alguns editores recomendados:

* [VS Code](https://code.visualstudio.com/)
* [PyCharm](https://www.jetbrains.com/pycharm/)

## Primitivos, variáveis e expressões

Python apresenta uma coleção de tipos primitivos: `bool` (*booleanos*), `int` (*inteiros*), `float` (*ponto flutuante*) e `str` (*string* |fc *texto*).

```python
>>> True # bool
True
>>> False # bool
False
>>> 10 # int
10
>>> 2.5 # float
2.5
>>> "Olá Mundo" # str
'Olá Mundo'
>>> 
```

Variáveis são nomes dados a objetos. Valores primitivos são objetos também:

```python
>>> x = 10
>>> print(x) # imprime na tela
10
>>> type(x) # retorna o tipo 
int
>>> 
```

Pode-se adicionar tipos à declaração de variáveis, mas estes tipos são apenas informativos e usados por ferramentas externas de verificação de código ([MyPy](http://mypy-lang.org/), [pytype](https://google.github.io/pytype/), [Pyre](https://pyre-check.org/)):

```python
>>> x : int = 10
>>> print(x)
10
>>> type(x)
int
>>> 
```

O interpretador ignora tipos informados:

```python
>>> x : str = 10
>>> print(x)
10
>>> type(x)
int
>>> 
```

**Expressões** são combinações de primitivos, variáveis e **operadores** que produzem novos valores:

```python
>>> x = 10
>>> x * 2 - 1
19
>>> 
```

Os resultados das expressões podem ser armazenados em variáveis:

```python
>>> x = 10
>>> y = 10 - 5
>>> y
5
>>> type(y)
int
>>> 
```

Exemplo de cálculo de juros composto usando primitivos, variáveis e expressões:

```python
>>> montante = 100
>>> taxa = 0.09 # 9%
>>> num_anos = 5
>>> ano_atual = 1
>>> while ano_atual <= num_anos:
...     montante = montante * (1 + taxa)
...     print(ano_atual, montante)
...     ano_atual += 1
... 
1 109.00000000000001
2 118.81000000000003
3 129.50290000000004
4 141.15816100000006
5 153.86239549000007
>>> 
```

O `while` testa e executa o **bloco de execução** enquanto a condição for verdadeira. 
Testa, executa. Testa novamente, executa novamente, enquanto a condição for verdadeira.

O **bloco de execução** está disposto imediatamente após a declaração e é indentado com espaços.
Recomenda-se a utilização de **4 espaços** para indentação.

Podemos aprimorar a apresentação do resultado no exemplo acima usando *f-strings*:

```python
>>> montante = 100
... taxa = 0.09 # 9%
... ano_final = 30
... ano_atual = 22
... while ano_atual <= ano_final:
...     montante = montante * (1 + taxa)
...     # >4d - decimal com quatro dígitos alinhado à direita
...     # 0.2f - ponto flutuante com precisão de dois dígitos
...     print(f"{ano_atual:>4d}, {montante:0.2f}")
...     ano_atual += 1
... 
  22, 109.00
  23, 118.81
  24, 129.50
  25, 141.16
  26, 153.86
  27, 167.71
  28, 182.80
  29, 199.26
  30, 217.19
```

## Operadores aritméticos

Python possui uma série de operadores aritméticos. Vejamos:

```python
>>> 10 + 2
12
>>> 10 - 2
8
>>> 10 * 2
20
>>> 10 / 2 # retorna ponto flutuante
5.0
>>> 10 // 2 # trunca, retorna inteiro
5
>>> 10 ** 2 # exponenciação
100
>>> 10 % 3 # "resto da divisão"
1
>>> 
```

Algumas funções matemáticas básicas também estão disponíveis:

```python
>>> abs( -10 )
10
>>> divmod( 10, 3 ) # 10 // 3, 10 % 3
(3, 1)
>>> pow(10, 2) # 10 ** 2
100
>>> pow(10, 2, 3) # 10 ** 2
1
>>> round(3.14, 1) # arredonda 3.14 para 1 casa de cimal
3.1
>>> round(3.149, 2) # arredonda 3.14 para 2 casas decimais
3.15
>>> 
```

> Obs: `round()` sempre arredonda valores de meio (`0.5, 1.5`) para o valor **par** mais próximo: `0.5`, vira `0.0`, `1.5` vira `2.0`.


Inteiros também permitem operações para manipulação de bits:

```python
>>> # & - bitwise AND
>>> x = 9   # 0b1001
... y = 10  # 0b1010
... 
... print(x & y)
... print(bin(x & y))
8
0b1000

>>> # | - bitwise OR
>>> x = 9   # 0b1001
... y = 10  # 0b1010
... 
... print(x | y)
... print(bin(x | y))
11
0b1011

>>> # ^ - Bitwise XOR
>>> x = 9   # 0b1001
... y = 10  # 0b1010
... 
... print(x ^ y)
... print(bin(x ^ y))
3
0b11

>>> # ~ - bitwise NOT
>>> x = 9  # 0b1001
... print(~x)
... print(bin(~x))
-10
-0b1010

>>> # <<, >> - bitwise shifts

>>> x = 9  # 0b1001
... print(x << 1)
... print(bin(x << 1))
18
0b10010

>>> x = 9  # 0b1001
... print(x >> 1)
... print(bin(x >> 1))
4
0b100
```

Os seguintes operadores permitem comparar valores:

```python
>>> 10 == 10
True
>>> 10 != 11
True
>>> 10 < 11
True
>>> 10 > 11
False
>>> 10 <= 11
True
>>> 10 >= 11
False
>>> 
```

O resultado das comparações é um booleano, `True` ou `False`.

Comparações compostas podem ser feitas conjugando os operadores `and` (**e** lógico), `or` (**ou** lógico) e `not` (negação lógica):

```python
>>> 10 < 11 and 9 < 10
True
>>> 10 < 11 and 9 < 8 # segunda condição é falsa
False
>>> 
>>> 
>>> 10 < 11 or 9 < 10
True
>>> 10 < 11 or 9 < 8
True
>>> 
>>> not 10 < 11
False
>>> not True
False
>>> not False
True
>>> 
```

Python considera como `False`:

| Tipo             | Valor |
|------------------|-------|
| Booleano         | `False` |
| Nulo             | `None`  |
| Inteiro          | `0`     |
| Ponto Flutuante  | `0.0`   |
| String Vazia     | `""`    |
| List Vazia       | `[]`    |
| Dicionário Vazio | `{}`    |

## Condicionais e fluxo de controle

A execução do programa pode ser condicionada usando declarações `if`, `elif` e `else`:

```python
extensao = input("Digite a extensão com três dígitos (ex: jpg, gif): ")

if extensao == "jpg": 
    print("imagem")
elif extensao == "gif":
    print("imagem")
elif extensao == "png":
    print("imagem")
else:
    print("Outo formato")
```

Exemplos dos possíveis fluxos de execução:

* `if`

```python
>>> extensao = input("Digite a extensão com três dígitos (ex: jpg, gif): ")
... 
... if extensao == "jpg":
...     print("imagem")
... elif extensao == "gif":
...     print("imagem")
... elif extensao == "png":
...     print("imagem")
... else:
...     print("Outo formato")
... 
Digite a extensão com três dígitos (ex: jpg, gif): jpg
imagem
>>> 
```

* `elif`

```python
>>> extensao = input("Digite a extensão com três dígitos (ex: jpg, gif): ")
... 
... if extensao == "jpg":
...     print("imagem")
... elif extensao == "gif":
...     print("imagem")
... elif extensao == "png":
...     print("imagem")
... else:
...     print("Outo formato")
... 
Digite a extensão com três dígitos (ex: jpg, gif): gif
imagem
>>> 
```

* `else`

```python
>>> extensao = input("Digite a extensão com três dígitos (ex: jpg, gif): ")
... 
... if extensao == "jpg":
...     print("imagem")
... elif extensao == "gif":
...     print("imagem")
... elif extensao == "png":
...     print("imagem")
... else:
...     print("Outo formato")
... 
Digite a extensão com três dígitos (ex: jpg, gif): mp4
Outo formato
>>> 
```

Você pode usar expressões condicionais ao atribuir valores a variáveis:

```python
>>> a = 10
>>> b = 12
>>> 
>>> maior_valor = a if a > b else b
>>> print(maior_valor)
12
>>> 
```

Em Python, atribuições não retornam valor. **Não** é possível fazer algo como:

```python
>>> contador = 0
>>> while (contador = contador + 1) < 10:
...     print(contador)
  Cell In[9], line 1
    while (contador = contador + 1) < 10:
                    ^
SyntaxError: invalid syntax
>>> 
```

Para tanto, foi criado o operador **walrus**, que realiza a atribuição e retorna o valor:

```python
>>> contador = 0
>>> while (contador := contador + 1) < 10: # parêntese sempre necessário!
...     print(contador)
... 
1
2
3
4
5
6
7
8
9
>>> 
```

> Obs: O operador **walrus** deve ser usado sempre entre parênteses.

Em repetições (**loops**) como o `while`, pode-se pular para a próximo ciclo de execução antecipadamente com a declaração `continue` ou interromper o ciclo com a declaração `break`:

```python
>>> contador = 0
>>> while (contador := contador + 1) < 10: # parêntese sempre necessário!
...     if contador == 5:
...         continue # pula para o próximo ciclo de execução do loop
...     elif contador == 7:
...         break # interrompe o ciclo antecipadamente
... 
...     print(contador)
... 
1
2
3
4
6
>>> 
```

## Strings

