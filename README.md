# GearScript
*APS - Lógica da Computação*  

## Introdução  
O **GearScript** é uma linguagem de domínio específico (DSL) criada para simular e automatizar o funcionamento de um carro em uma máquina virtual.  
Com ela, é possível definir veículos, executar operações de direção, usar sensores (combustível, velocidade, temperatura, posição), aplicar estruturas condicionais e repetir ações.  

A proposta é fornecer uma linguagem de alto nível que será traduzida para um Assembly específico de uma **VM Automotiva**, que conterá registradores (como `velocidade`, `combustivel`), memória de comandos e sensores internos.  

---

## Objetivos da Linguagem  
- Permitir a **definição de veículos**.  
- Executar **operações automotivas** (`acelerar`, `frear`, `abastecer`, `virar`).  
- Suportar **estruturas de decisão** (`SE ... ENTAO ... SENAO`).  
- Suportar **estruturas de repetição** (`REPETIR ... VEZES`, `ENQUANTO`).  
- Integrar **sensores de estado** (`velocidade`, `combustivel`, `temperatura`).  
- Produzir código intermediário traduzido em Assembly para a VM.  

---

## Gramática em EBNF  

```ebnf
PROGRAMA        = { COMANDO } ;

COMANDO         = ( DEFINIR_CARRO | OPERACAO | BLOCO_SE | BLOCO_REPETIR | MOSTRAR | COMENTARIO ) ;

/* --- Definições --- */
DEFINIR_CARRO   = "CARRO", IDENTIFICADOR, "{",
                    "modelo" "=", STRING, ";",
                    "combustivel" "=", NUMBER, ";",
                    "velocidade" "=", NUMBER, ";",
                    "temperatura" "=", NUMBER, ";",
                  "}" ;

/* --- Operações Automotivas --- */
OPERACAO        = ( ACELERAR | FREAR | ABASTECER | VIRAR ) ;

ACELERAR        = "ACELERAR", NUMBER, "EM", IDENTIFICADOR, ";" ;
FREAR           = "FREAR", NUMBER, "EM", IDENTIFICADOR, ";" ;
ABASTECER       = "ABASTECER", NUMBER, "EM", IDENTIFICADOR, ";" ;
VIRAR           = "VIRAR", DIRECAO, "EM", IDENTIFICADOR, ";" ;

DIRECAO         = "ESQUERDA" | "DIREITA" ;

/* --- Estruturas de Controle --- */
BLOCO_SE        = "SE", CONDICAO, "ENTAO", "{", { COMANDO }, "}", 
                   [ "SENAO", "{", { COMANDO }, "}" ] ;

BLOCO_REPETIR   = "REPETIR", NUMBER, "VEZES", "{", { COMANDO }, "}" 
                | "ENQUANTO", CONDICAO, "{", { COMANDO }, "}" ;

/* --- Exibição de Informação --- */
MOSTRAR         = "MOSTRAR", ( STRING | ATRIBUTO_CARRO ), ";" ;

/* --- Condições e Valores --- */
CONDICAO        = VALOR, OPERADOR, VALOR ;
VALOR           = ( NUMBER | ATRIBUTO_CARRO ) ;
ATRIBUTO_CARRO  = IDENTIFICADOR, ".", ( "combustivel" | "velocidade" | "temperatura" ) ;
OPERADOR        = "==" | ">" | "<" | ">=" | "<=" ;

/* --- Literais e Tipos Básicos --- */
NUMBER          = DIGIT, { DIGIT } ;
STRING          = '"', { LETTER | DIGIT | " " }, '"' ;
IDENTIFICADOR   = LETTER, { LETTER | DIGIT | "_" } ;
COMENTARIO      = "//", { LETTER | DIGIT | " " }, "\n" ;

/* --- Letras e Dígitos Explicitados --- */
LETTER          = "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" | "K" | "L" | "M" 
                | "N" | "O" | "P" | "Q" | "R" | "S" | "T" | "U" | "V" | "W" | "X" | "Y" | "Z" 
                | "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" 
                | "n" | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x" | "y" | "z" ;

DIGIT           = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
```

---
