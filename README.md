# 📑 Sumário

## 🧱 Fundamentos da Computação
- [Bits & Bytes](#bits--bytes)

    - [Bit](#-bit-binary-digit--b)
    - [Byte](#-byte--b)
- [Sistema Binário](#-sistema-binário-base-2)


## ⚙️ Memória
- [Stack vs Heap](#stack-vs-heap)

  - [Stack](#-stack-pilha)
  - [Heap](#-heap)


## 🏗️ Modelagem
- [JPA — Relacionamentos](#-guia-rápido-jpa--relacionamentos)

    - [OneToMany (1:N)](#-onetomany-1n)
    - [ManyToOne (N:1)](#-manytoone-n1)
    - [OneToOne (1:1)](#-onetoone-11)
    - [ManyToMany (N:N)](#-manytomany-nn)
    - [mappedBy](#-mappedby)
    - [JoinColumn](#-joincolumn)
    - [JoinTable](#-jointable)


## ️Banco de Dados
- [ACID](#acid)

    - [Atomicity](#a--atomicity)
    - [Consistency](#c--consistency)
    - [Isolation](#i--isolation)
    - [Durability](#d--durability)
- [Transaction](#transaction)


## 🧠 Paradigmas de Programação
- [Imperativo](#-paradigma-imperativo)
- [Declarativo](#-paradigma-declarativo)
- [Procedural](#-paradigma-procedural)
- [Orientado a Objetos](#-programação-orientada-a-objetos-oop)
- [Funcional](#-programação-funcional)


## 🧩 Boas Práticas e Design de Código
- [SOLID](#solid)

    - [Single Responsibility Principle](#s--single-responsibility-principle)
    - [Open/Closed Principle](#o--openclosed-principle)
    - [Liskov Substitution Principle](#l--liskov-substitution-principle)
    - [Interface Segregation Principle](#i--interface-segregation-principle)
    - [Dependency Inversion Principle](#d--dependency-inversion-principle)
- [Object Calisthenics](#object-calisthenics)

    - [Regra 1 (identação)](#regra-1-um-nível-de-indentação-por-método)
    - [Regra 2 (else)](#regra-2-não-use-a-palavra-chave-else)
    - [Regra 3 (encapsulamento de tipos primitivos/String)](#regra-3-encapsule-todos-os-primitivos-e-strings)
    - [Regra 9 (getters e setters)](#regra-9-evite-getters-e-setters)

---

# Bits & Bytes

## 🧠 Conceito fundamental

> Um bit só pode assumir **duas possibilidades**: `0` ou `1`.

Por isso, utilizamos um sistema de numeração baseado em **potências de 2**:

```
base^n → 2^n
```

---

## 📊 Quantidade de possibilidades

| Bits    | Cálculo          | O que representa?          |
| ------- | ---------------- | -------------------------- |
| 1 bit   | 2¹ = 2           | Sim/Não • Verdadeiro/Falso |
| 4 bits  | 2⁴ = 16          | 1 dígito hexadecimal (0–F) |
| 8 bits  | 2⁸ = 256         | 1 Byte • Tabela ASCII      |
| 24 bits | 2²⁴ = 16.777.216 | Cores RGB (True Color)     |

---

## ⚠️ Observação sobre `2⁰`

> `2⁰ = 1`, ou seja, apenas **uma possibilidade**

### ❌ Para armazenamento

* Não representa um "bit completo" isoladamente
* Um bit precisa representar **2 estados (0 e 1)**

### ✅ Para cálculos

* É **essencial**
* Sem `2⁰`, não existiria o valor `1`

Exemplo:

```
3 (decimal) = 2 + 1
3 (binário) = 011
```

Sem o `2⁰`, não seria possível representar esse valor.

---

## 🧠 A lógica das potências

Todo sistema numérico posicional funciona com potências da sua base.

### 🔢 Sistema Decimal (Base 10)

```
10⁰ = 1
10¹ = 10
10² = 100
10³ = 1000
```

👉 Cada posição vale **10x mais** que a anterior

---

### 💻 Sistema Binário (Base 2)

```
2⁰ = 1
2¹ = 2
2² = 4
2³ = 8
2⁴ = 16
...
```

👉 Cada posição vale **2x mais** que a anterior

---

## 🔹 Bit (BInary DigiT) — "b"

* Unidade básica de informação
* Representa um **pulso elétrico**
* Só pode assumir:

  * `0` → desligado
  * `1` → ligado

---

## 🔸 Byte — "B"

> Um Byte é um conjunto de **8 bits**

```
00000000 → 11111111  
Exemplos: 10100010 • 11100011
```

### 📊 Características

* Total de possibilidades: **256 (0 → 255)**
* 8 bits → 2⁸ = 256 combinações possíveis
* Foi padronizado com 8 bits porque:

  * Permite representar letras (maiúsculas e minúsculas)
  * Números
  * Símbolos
  * Caracteres especiais (ASCII)

---

## 🧮 Exemplo prático

### Convertendo binário para decimal

```
00001001 
```

### 📐 Cálculo

```
Bit x Peso
 0  x 128 = 0
 0  x 64  = 0
 0  x 32  = 0
 0  x 16  = 0
 1  x 8   = 8
 0  x 4   = 0
 0  x 2   = 0
 1  x 1   = 1
```

```
Resultado: 8 + 1 = 9
```

---

## 📌 Ordem dos bits

> Os bits seguem da direita para a esquerda:

```
[128][64][32][16][8][4][2][1]
  ↑                       ↑
Mais significativo   Menos significativo
```

* Direita → menor peso (`2⁰`)
* Esquerda → maior peso (`2⁷` em 1 byte)

---

## ✅ Resumo

* Bit = menor unidade (0 ou 1)
* Byte = 8 bits (0 → 255)
* Sistema binário usa base 2
* Tudo é construído com **potências de 2**
* `2⁰` não serve para armazenamento, mas é essencial para cálculo

---

# Stack vs Heap

## 🧠 Conceito fundamental

> A memória de um programa é dividida em regiões com responsabilidades diferentes.

As duas principais são:

* **Stack (Pilha)** → execução de métodos
* **Heap (Monte)** → armazenamento de objetos

---

## ⚖️ Diferença principal

> Stack gerencia **execução**, Heap gerencia **dados**

* Stack → controla o fluxo do programa
* Heap → guarda os dados que vivem por mais tempo

---

## 📦 Stack (Pilha)

> Estrutura de dados do tipo **LIFO (Last In, First Out)**

👉 O último que entra é o primeiro que sai

---

### 📊 Características

* ⚡ Mais rápida
* 📏 Tamanho limitado (definido pelo SO)
* 🧹 Limpeza automática (movimento do Stack Pointer)
* 📚 Armazena:

  * chamadas de função/método
  * parâmetros
  * variáveis locais
  * tipos primitivos (dependendo da linguagem)

---

### 🧱 Stack Frame

> Cada chamada de função cria um **Stack Frame**

```
__________
|         |
| funcao2 | ← último a entrar (sai primeiro)
| funcao1 |
|  main   |
|_________|
```

* Cada função tem seu próprio contexto
* Quando a função termina:

  * seu frame é removido
  * suas variáveis locais desaparecem

---

### ⚠️ Stack Overflow

> Ocorre quando a Stack ultrapassa seu limite

Exemplo comum:

```java
public void recursaoInfinita() {
    recursaoInfinita();
}
```

👉 Cada chamada adiciona um novo frame até estourar a memória

---

## 🗂️ Heap

> Região de memória usada para **alocação dinâmica**

---

### 📊 Características

* 🐢 Mais lenta que a Stack
* 📦 Armazena objetos e instâncias
* 📈 Cresce mais que a Stack (limitada pela RAM)
* 🔄 Dados não seguem uma ordem definida (não é pilha)
* 🧹 Gerenciamento/Limpeza dos objetos na memória
  
  * **Java, C#, Python** → Garbage Collector (automático)
  * **C, C++** → Gerenciamento Manual

---

## 🔗 Relação entre Stack e Heap

> A Stack não guarda objetos diretamente — ela guarda **referências para a Heap**

### 🧮 Exemplo

```java
public void exemplo() {
    int x = 10;                // Stack
    Produto p = new Produto(); // referência na Stack, objeto na Heap
}
```

---

### 📐 Representação

```
STACK                    HEAP
-----                    -----
x = 10                   (valor direto)

p -----------┐           Produto { ... }
             └---------> (objeto na memória)
```

---

## 🧠 Fluxo de execução

```java
public static void main(String[] args) {
    funcao1();
}

public static void funcao1() {
    funcao2();
}

public static void funcao2() {
}
```

### 📦 Stack durante execução:

```
┌─────────┐
│ funcao2 │
│ funcao1 │
│  main   │
└─────────┘
```

👉 Quando `funcao2` termina:

* ela sai da stack
* volta para `funcao1`

---

## ⚖️ Comparação direta

| Característica | Stack                     | Heap                 |
| -------------- | ------------------------- | -------------------- |
| Estrutura      | Pilha (LIFO)              | Livre                |
| Velocidade     | Mais rápida               | Mais lenta           |
| Gerenciamento  | Automático                | Automático ou manual |
| Armazena       | Funções, variáveis locais | Objetos              |
| Tempo de vida  | Curto                     | Mais longo           |
| Tamanho        | Limitado                  | Maior                |

---

# 📘 Guia rápido JPA — Relacionamentos

---

## 🧠 Como saber quem deve possuir a FK (dono da relação)?

### Regra mental mais importante:

> 👉 **“Quem precisa de quem para existir?”**

### Exemplo: Cliente vs Pedido

* ✅ Cliente pode existir sem pedido
* ❌ Pedido NÃO pode existir sem cliente

➡️ Logo: **Pedido possui a FK (`cliente_id`)**

---

## 🔁 Tipos de relacionamento

---

## 🔹 OneToMany (1:N)

### 🧩 Conceito

Um cliente pode ter vários pedidos

```
  One	        Many
	      ┌── Pedido1
Cliente ──┼── Pedido2
	      └── Pedido3
```

### 💻 Código

```java
public class Cliente {
  @OneToMany(mappedBy = "cliente")
  private List<Pedido> pedidos;

}
```

📌 **Importante:**

* `mappedBy` indica que **Cliente NÃO é dono da relação**

---

## 🔹 ManyToOne (N:1)

### 🧩 Conceito

Vários pedidos pertencem a um cliente

```
 Many	        One
Pedido1 ──┐
Pedido2 ──┼── Cliente
Pedido3 ──┘
```

### 💻 Código

```java
public class Pedido {
  @ManyToOne
  @JoinColumn(name = "cliente_id")
  private Cliente cliente;
}
```

📌 **Importante:**
* `@JoinColumn` indica que **aqui está o dono da relação!** *(quem possui a fk)*

---

## 🔹 OneToOne (1:1)

### 🧩 Conceito

Um registro para um registro

Exemplo:

* Usuário ↔ Subscription

### 💻 Exemplo

```java
public class Subscription {
  @OneToOne
  @JoinColumn(name = "user_id")
  private User user;
}

public class User {
  @OneToOne(mappedBy = "user")
  private Subscription subscription;
}
```

---

## 🔹 ManyToMany (N:N)

### 🧩 Conceito

Muitos para muitos → precisa de uma **tabela intermediária (join table)**

Exemplo:

* Pedido ↔ Produto

> Um pedido pode ter vários produtos
> Um produto pode estar em vários pedidos

---

### 🔗 Representação

```
Pedido1 ──┐
Pedido2 ──┼── Pedido_Produto ──┼── Produto1
Pedido3 ──┘                    └── Produto2
```

---

## 💻 Exemplo

```java
public class Pedido {
  @ManyToMany
  @JoinTable(
    name = "pedido_produto",
    joinColumns = @JoinColumn(name = "pedido_id"),
    inverseJoinColumns = @JoinColumn(name = "produto_id")
  )
  private List<Produto> produtos = new ArrayList<>();

}

public class Produto {
  @ManyToMany(mappedBy = "produtos")
  private List<Pedido> pedidos = new ArrayList<>();

}
```

---

## 📌 Importante

* `@JoinTable` → define a **tabela intermediária**
* `joinColumns` → FK da entidade atual (Pedido)
* `inverseJoinColumns` → FK da outra entidade (Produto)

---

## 🔧 mappedBy

### 🧩 O que é?

Indica **o lado inverso da relação** (quem NÃO tem a FK)

---

### 💡 Regra simples:

> 👉 `mappedBy` fica na entidade que **NÃO possui a FK**

---

### ⚠️ Atenção importante

O valor do `mappedBy`:

* ✔️ Deve ser o **nome do atributo Java**
* ❌ NÃO é o nome da coluna no banco

---

### 💻 Exemplo completo

```java
public class Pedido {
  @ManyToOne
  @JoinColumn(name = "cliente_id")
  private Cliente cliente;

}

public class Cliente {
  @OneToMany(mappedBy = "cliente")
  private List<Pedido> pedidos;

}
```

📌 `"cliente"` → nome do atributo na classe `Pedido`

---

### 🚨 Erro comum

```
mappedBy reference an unknown target entity property
```

➡️ Significa que o nome no `mappedBy` está errado

---

### 🤯 Dica importante

Você **NÃO é obrigado** a mapear os dois lados

```java
// ✔️ Isso funciona
public class Pedido {
  @ManyToOne
  @JoinColumn(name = "cliente_id")
  private Cliente cliente;

}

// ❌ Não precisa disso
public class Cliente {
  @OneToMany(mappedBy = "cliente")
  private List<Pedido> pedidos;
}
```

---

## 🔗 JoinColumn

### 🧩 O que faz?

Define **onde fica a FK**

---

### 💡 Regra de ouro:

> 👉 Quem tem `@JoinColumn` = **dono da relação**

---

### 💻 Exemplo

```java
@ManyToOne
@JoinColumn(name = "cliente_id")
private Cliente cliente;
```

---

### 🗄️ Isso gera no banco:

```sql
cliente_id BIGINT
FOREIGN KEY (cliente_id) REFERENCES cliente(id)
```

---

## 🔗 JoinTable

### 🧩 Quando usar?

Quando **não existe FK direta** → precisa de tabela intermediária

---

### 💻 Exemplo

```java
@ManyToMany
@JoinTable(
    name = "pedido_produto",
    joinColumns = @JoinColumn(name = "pedido_id"),
    inverseJoinColumns = @JoinColumn(name = "produto_id")
)
private List<Produto> produtos;
```

---

### 🗄️ Isso gera:

Tabela `pedido_produto`

```sql
pedido_id
produto_id
```

---

### 💡 Tradução mental

* `joinColumns` → FK da entidade atual
* `inverseJoinColumns` → FK da outra entidade

---

## 🧠 Resumo

* ✔️ Quem tem `@JoinColumn` → **dono da relação**
* ✔️ `mappedBy` → lado inverso *(sem fk)*
* ✔️ FK fica em quem **não pode existir sozinho**
* ✔️ `ManyToMany` → sempre tem tabela intermediária
* ✔️ `mappedBy` usa **nome do atributo Java**

---

# ACID

## 🧠 Conceito fundamental

> **ACID** é um conjunto de **4 garantias** que fazem com que operações no banco sejam **seguras, previsíveis e confiáveis**.

👉 **"Transações precisam funcionar corretamente mesmo com erros, concorrência e falhas."**
👉 **"Ou tudo acontece certo, ou nada acontece, e ninguém interfere no meio."**

---

## 📌 As 4 garantias

* **A**tomicity → Tudo ou nada dentro da transação
* **C**onsistency → Dados sempre válidos, `o banco sai de um estado válido para outro estado válido`
* **I**solation → Transações independentes, `dependendo do nível de isolamento`
* **D**urability → Dados persistentes após commit

---

### 📊 Visual simples:

```
BEGIN TRANSACTION
   ↓
Executa operações
   ↓
Tudo deu certo? → COMMIT ✅
Algo falhou?    → ROLLBACK ❌
```

---

## ❌ Exemplo incorreto

```sql
UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
-- ERRO acontece aqui
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;
```

🚨 Problema:

* O dinheiro saiu da conta 1
* Mas não entrou na conta 2

---

## ✅ Exemplo correto

```sql
BEGIN;

UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;

COMMIT;

-- 👉 Se algo falhar:
ROLLBACK;
```

---

## ✅ Resumo:

* Transações são seguras (Atomicity)
* Dados permanecem válidos (Consistency)
* Concorrência é controlada (Isolation)
* Dados persistem (Durability)

---

# A — Atomicity

> **Ou todas as suas operações são bem-sucedidas, ou nenhuma é aplicada.** Se alguma parte falhar, toda a transação é desfeita para manter o banco de dados consistente.

* **Commit:** Transação completa com sucesso
* **Rollback:** Desfaz qualquer alteração parcial em caso de falha

---

# C — Consistency

> **O banco de dados deve permanecer em um estado válido antes e depois de uma transação.**

* Regras e restrições *(PK, FK, UNIQUE, triggers)* são respeitadas
* É revertida caso, violar qualquer uma dessas regras.

---

# I — Isolation

> **Garante que transações concorrentes não causem inconsistências, controlando o nível de visibilidade entre elas.** As alterações feitas por uma transação não são visíveis para outras até que sejam confirmadas.

* Evita **dirty reads**, leitura de dados não comprometidos
* Evita **non-repeatable reads**, mudanças de dados entre duas leituras
* Evita **phantom reads**, novas linhas aparecem durante uma transação
* Nem sempre totalmente isoladas, depende do nível de isolamento *(READ COMMITTED, REPEATABLE READ, SERIALIZABLE)*
* Garante que o resultado final seja equivalente a uma execução sequencial

---

# D — Durability

> **Após o commit, as alterações serão salvas permanentemente, mesmo em caso de falhas.**

* Implementado via Write-Ahead Logging *(WAL)*, flush em disco ou replicação

---

# Transaction

## 🧠 Conceito fundamental

> Uma **transação** é um **conjunto de operações no banco que deve acontecer como uma única unidade**.

👉 Aplica as propriedades [**ACID**](#acid)  
👉 Deve ser finalizada com **COMMIT** ou **ROLLBACK**

* **COMMIT** → salva tudo
* **ROLLBACK** → desfaz tudo

---

## 🔄 Fluxo básico de uma transação

```sql
BEGIN;

UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;

COMMIT;
```

Ou, em caso de erro:

```sql
ROLLBACK;
```

---

## ❌ Exemplo incorreto

Transferência sem transação:

```sql
UPDATE contas SET saldo = saldo - 100 WHERE id = 1;

-- ERRO AQUI (ex: queda de sistema)

UPDATE contas SET saldo = saldo + 100 WHERE id = 2;
```

---

## 🚨 Problema

💥 O dinheiro some

* Conta 1 → perdeu 100
* Conta 2 → não recebeu
* Banco → inconsistente

👉 Isso quebra a **consistência do sistema**

---

## ✅ Exemplo correto

Usando transação:

```sql
BEGIN;

UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;

COMMIT;
```

Ou com erro:

```sql
BEGIN;

UPDATE contas SET saldo = saldo - 100 WHERE id = 1;

-- ERRO DETECTADO

ROLLBACK;
```

👉 Resultado: nada é aplicado → banco continua correto

---

## 💻 Exemplo fora do SQL

Exemplo conceitual em código:

```js
try {
  beginTransaction();

  debitar(conta1, 100);
  creditar(conta2, 100);

  commit();
} catch (e) {
  rollback();
}
```

---

## ✅ Resumo

* Transação = **grupo de operações indivisível**
* Sempre termina em:

  * ✅ COMMIT
  * ❌ ROLLBACK
* Base: **ACID**
* Evita:

  * Dados inconsistentes
  * Perda de informação
  * Problemas de concorrência

---

# Paradigmas da Programação

---

## 🧠 Conceito fundamental

> Paradigmas são **formas diferentes de pensar e estruturar código**.

👉 Eles definem **como você resolve problemas**, não apenas a sintaxe.
👉 **“Paradigma é o jeito de pensar antes de codar”**

---

## 📊 Resumo visual

```
Paradigmas
│
├── Imperativo (como fazer)
│   ├── Procedural
│   └── Orientado a Objetos (POO)
│
└── Declarativo (o que fazer)
    ├── Funcional
    └── Lógico
```

---

## Imperativo *(como fazer)*

> Você descreve **como o programa deve fazer algo**, passo a passo.

* **Procedural** → baseado em procedimentos/funções (ex: C)
* **Orientado a Objetos (POO)** → organiza em objetos (ex: Java, C++)

## Declarativo *(o que fazer)*

> Você descreve **o que quer obter**, sem especificar os passos detalhados.

* **Funcional** → baseado em funções puras (ex: Haskell)
* **Lógico** → baseado em regras (ex: Prolog)

---

# 🔹 Paradigma Imperativo

---

## 🧠 Conceito fundamental

> Você escreve **cada passo que o programa deve executar**

👉 “Controle total do passo a passo”

---

## 📊 Explicação estruturada

* Usa:

  * variáveis mutáveis
  * loops (`for`, `while`)
  * condicionais (`if`)

---

```java
int soma = 0;
for (int i = 1; i <= 3; i++) {
    soma += i;
}
```

---

## ✅ Resumo

* Imperativo funciona bem para controle fino
* Quanto mais cresce → mais complexo fica
* Controle total
* Muito usado
* Pode virar código bagunçado se mal estruturado

---

# 🔹 Paradigma Declarativo

---

## 🧠 Conceito fundamental

> Você diz **o que quer**, não como fazer

👉 “Descreva o resultado, não o processo”

---

## 📊 Explicação estruturada

* Muito usado em:

  * SQL
  * Streams
  * HTML

---

```sql
SELECT SUM(valor) FROM vendas;
```

```java
List<Integer> pares = lista.stream()
    .filter(i -> i % 2 == 0)
    .toList();
```

---

## 🔁 Comparação direta

| Imperativo  | Declarativo  |
| ----------- | ------------ |
| Como fazer  | O que fazer  |
| Mais código | Mais simples |

---

## ✅ Resumo

* Declarativo reduz complexidade
* Abstrai detalhes
* Aumenta produtividade
* Foco no resultado
* Menos código
* Mais legível

---

# 🔸 Paradigma Procedural

---

## 🧠 Conceito fundamental

> É o imperativo organizado em **funções (procedimentos)**

👉 “Quebre o problema em funções”

---

## 📊 Explicação estruturada

* Divide código em:

  * funções
  * métodos
* Evita repetição

---

```java
// ❌ Exemplo incorreto
int soma = 0;
for (int i = 1; i <= 10; i++) {
    soma += i;
}
System.out.println(soma);
soma = 0;
for (int i = 1; i <= 5; i++) {
    soma += i;
}
System.out.println(soma);

// 🚨 Problema
// * Código duplicado
// * Difícil manutenção


// ✅ Exemplo correto
public static int somar(int limite) {
    int soma = 0;
    for (int i = 1; i <= limite; i++) {
        soma += i;
    }
    return soma;
}
System.out.println(somar(10));
System.out.println(somar(5));
```

---

## 🔁 Comparação direta

| Antes           | Depois              |
| --------------- | ------------------- |
| Código repetido | Função reutilizável |

---

## ✅ Resumo

* Funções que reduzem duplicação
* Melhora na organização
* Facilidade em testes
* Base do código moderno
* Reutilização
* Mais organizado que imperativo puro

---

# 🔸 Programação Orientada a Objetos (OOP)

---

## 🧠 Conceito fundamental

> Modela o sistema como **objetos com estado e comportamento**

👉 “Quem tem o dado, faz a ação”

---

## 📊 Explicação estruturada

* Conceitos principais:

  * Classe
  * Objeto
  * Encapsulamento
  * Herança
  * Polimorfismo

---

```java
// ❌ Exemplo incorreto
class Pedido {
    public String status;
}

if (pedido.status.equals("PAGO")) {
    enviarEmail();
}

// 🚨 Problema
// * Regra fora do objeto
// * Quebra encapsulamento


// ✅ Exemplo correto
class Pedido {
    private String status;
  
    public boolean estaPago() {
        return status.equals("PAGO");
    }
}

if (pedido.estaPago()) {
    enviarEmail();
}
```

---

## 🔁 Comparação direta

| Errado           | Correto               |
| ---------------- | --------------------- |
| Dados expostos   | Comportamento interno |
| Lógica espalhada | Lógica encapsulada    |

---

## ✅ Resumo

* Centraliza regras
* Facilita manutenção
* Modela o mundo real
* Encapsula regras
* Muito usado em sistemas grandes

---

# 🔸 Programação Funcional

---

## 🧠 Conceito fundamental

> Baseado em **funções puras e dados imutáveis**

👉 “Não mude dados, crie novos”

---

## 📊 Explicação estruturada

* Funções puras:

  * mesmo input → mesmo output
* Sem efeitos colaterais
* Imutabilidade

---

```java
// ❌ Exemplo incorreto
int total = 0;
public void adicionar(int valor) {
    total += valor;
}

// 🚨 Problema
// * Estado global
// * Difícil prever comportamento
// * Bugs em concorrência


// ✅ Exemplo correto
public int somar(int a, int b) {
    return a + b;
}

// Ou com Stream:
int soma = List.of(1,2,3)
    .stream()
    .mapToInt(i -> i)
    .sum();
```

---

## 🔁 Comparação direta

| Mutável        | Imutável           |
| -------------- | ------------------ |
| altera estado  | retorna novo valor |
| difícil prever | previsível         |

---

## ✅ Resumo

* Imutabilidade = menos bugs
* Sem estado compartilhado = mais seguro
* Código previsível
* Ideal para concorrência
* Muito usado com Streams

---

# SOLID

## 🧠 Conceito fundamental

> **SOLID** é um conjunto de princípios que ajudam a criar códigos **mais organizados, flexíveis e fáceis de manter**

---

## 📌 Os 5 princípios

* **S** → Uma única responsabilidade.
* **O** → Extensível, mas não modificável.
* **L** → Substituição segura de classes filhas por pais.
* **I** → Interfaces específicas, não generalizadas.
* **D** → Dependa de abstrações, não de implementações.

---

# S — Single Responsibility Principle

## 🧠 Conceito

> **Uma classe deve ter apenas um motivo para mudar.** Ela não deve ser/fazer muitas coisas ao mesmo tempo, deve fazer apenas aquilo que ela se propõe a ser.

👉 Ou seja: deve ter **uma única responsabilidade**

---

## ❌ Exemplo incorreto
Uma classe Relatorio que gera os dados, formata para PDF e envia por email.

```java
class RelatorioFinanceiro {
    public void gerarRelatorio() {
        // Buscar dados
        // Gerar PDF
        // Enviar e-mail
    }
}
```

👉 Problema:

* Muitas responsabilidades em uma única classe

---

## ✅ Exemplo correto
Uma classe para gerar os dados, uma classe para gerar o PDF e uma classe para enviar email.

```java
class DadosRelatorio {
  // Entidade com as informações
}

// Gateways / Interfaces / Contratos
interface IExportadorPdf {
    byte[] exportar(DadosRelatorio dados);
}

interface IEmailService {
    void enviar(String destinatario, byte[] conteudo);
}

// Implementação Real das Interfaces
class ExportadorPDF implements IExportadorPdf {
    public byte[] exportar(DadosRelatorio dados) {
        // Gerando pdf...
    }
}

class ServicoEmail implements IEmailService {
    public void enviar(String destinatario, byte[] conteudo) {
        // Enviando email...
    }
}

// Relatório com a responsabilidade correta
class RelatorioFinanceiro {
    public void gerarRelatorio(IDadosProvider provider, IExportadorPdf exportador, IEmailService email) {
        DadosRelatorio dados = provider.coletarDados();
        byte[] pdf = exportador.exportar(dados);
        email.enviar("email", pdf);
    }
}
```

---

## ✅ Resumo

* Cada classe faz **uma coisa só**
* Facilita manutenção
* Facilita testes

---

# O — Open/Closed Principle

## 🧠 Conceito

> **Classes devem estar abertas para extensão, mas fechadas para modificação.** Devemos ser capazes de adicionar uma nova funcionalidade/comportamento ao código sem precisar mexer no código original que já funciona (através de interfaces e herança).

👉 Você adiciona comportamento sem alterar código existente

---

## ❌ Exemplo incorreto
Um sistema de hipotético de pagamentos que aceita pagamento por PIX e DÉBITO, funciona perfeitamente, e está da seguinte maneira:

```java
class ProcessadorPagamento {
    public void processar(String metodoPagamento) {
        if (metodoPagamento.equals("PIX")) {
            // processando PIX...
        } else if (metodoPagamento.equals("DEBITO")) {
            // processando DÉBITO...
        }
    }
}
```

👉 Problema:

* Toda nova regra exige modificar a classe (na prática, um novo if para cada novo caso adicionado)

---

## ✅ Exemplo correto
Um código correto deveria utilizar uma interface em comum com um método 'pagar()' que seria implementado por cada método de pagamento individualmente, sem a necessidade de alterar o código principal.

```java
interface MetodoPagamento {
    void pagar();
}

class PagamentoPix implements MetodoPagamento {
    public void pagar() {}
}

class PagamentoDebito implements MetodoPagamento {
    public void pagar() {}
}

// Novo método adicionado sem precisar alterar o código original
class PagamentoBoleto implements MetodoPagamento {
    public void pagar() {}
}

class ProcessadorPagamento {
    public void processar(MetodoPagamento metodo) {
        metodo.pagar();
    }
}
```

---

## 💡 Benefício

* Novo método de pagamento = nova classe
* Nenhuma alteração no código existente

---

## ✅ Resumo

* Evita `if/else` gigantes
* Usa polimorfismo
* Código mais extensível

---

# L — Liskov Substitution Principle

## 🧠 Conceito

> **Subclasses devem poder substituir suas classes base sem quebrar o comportamento.**

---

## ❌ Exemplo incorreto

```java
class Pagamento {
    public void processar(double valor) {
        // processa pagamento
    }
}

class CartaoCredito extends Pagamento {
    @Override
    public void processar(double valor) {
        System.out.println("Processando no cartão: " + valor);
    }
}

class Boleto extends Pagamento {
    @Override
    public void processar(double valor) {
        throw new UnsupportedOperationException("Boleto não é processado na hora");
    }
}
```

---

## 🚨 Problema

```java
public void finalizarCompra(Pagamento pagamento) {
    pagamento.processar(100);
}
```

👉 Funciona com CartaoCredito

👉 Quebra com Boleto ❌

---

## 💡 Insight

> O problema não é o código — é o **modelo errado de herança**

* Esse tipo de erro aparece MUITO quando você:
  
  * Junta coisas parecidas mas com comportamentos diferentes
  * Cria uma classe base genérica demais

---

## ✅ Exemplo correto

```java
interface Pagamento {
    void iniciar(double valor);
}

interface PagamentoInstantaneo extends Pagamento {
    void processar(double valor);
}

class CartaoCredito implements PagamentoInstantaneo {
    public void iniciar(double valor) {}
    public void processar(double valor) {
        System.out.println("Pago na hora");
    }
}

class Boleto implements Pagamento {
    public void iniciar(double valor) {
        System.out.println("Gerando boleto...");
    }
}
```

---

## ✅ Resumo

* Herança deve respeitar comportamento
* Subclasse não pode “quebrar expectativas”

---

# I — Interface Segregation Principle

## 🧠 Conceito

> **Nenhuma classe deve ser forçada a implementar métodos que não usa.** Faz mais sentido possuirmos interfaces específicas do que interfaces generalizadas.

---

## ❌ Exemplo incorreto

```java
interface ProcessadorPagamento {
    void validarDados();
    void processar();
    void gerarLinhaDigitavel(); // Só faz sentido para Boleto
    void validarParcelamento(); // Só faz sentido para Cartão
}
```

---

### 🚨 Problema

```java
class PagamentoBoleto implements ProcessadorPagamento {
    public void validarDados() {}
    public void processar() {}
    public void gerarLinhaDigitavel() {}
    public void validarParcelamento() {
        // Não faz sentido um boleto validar parcelamento
    }
}
```

---

## ✅ Exemplo correto

```java
interface MetodoPagamento {
    void processar();
}

interface PagamentoComCodigo {
    void gerarLinhaDigitavel();
}

interface PagamentoParcelavel {
    void validarParcelamento();
}

class PagamentoBoleto implements MetodoPagamento, PagamentoComCodigo {
    public void processar() {}
    public void gerarLinhaDigitavel() {}
}

class PagamentoCartaoCredito implements MetodoPagamento, PagamentoParcelavel {
    public void processar() {}
    public void validarParcelamento() {}
}
```

---

## ✅ Resumo

* Interfaces pequenas e específicas
* Evita métodos inúteis
* Código mais coeso

---

# D — Dependency Inversion Principle

## 🧠 Conceito

> **Dependa de abstrações, não de implementações concretas.** Módulos de alto nível *(regra negócio)* não devem depender de módulos de baixo nível *(implementação concreta)*.

---

## ❌ Exemplo incorreto

```java
class PasswordReminder {
    private PostgresConnection dbConnection;

    public PasswordReminder(PostgresConnection connection) {
        this.dbConnection = connection;
    }
}
```

---

## 🚨 Problema

* Forte acoplamento
* Difícil trocar o banco de dados

---

## ✅ Exemplo correto

```java
interface IDatabaseConnection {
    void connect();
}

class PostgresConnection implements IDatabaseConnection {
    public void connect() {}
}

class MySqlConnection implements IDatabaseConnection {
    public void connect() {}
}

class PasswordReminder {
    private IDatabaseConnection dbConnection;

    public PasswordReminder(IDatabaseConnection connection) {
        this.dbConnection = connection;
    }
}
```

---

## 💡 Uso

```java
IDatabaseConnection db = new PostgresConnection();
PasswordReminder reminder = new PasswordReminder(db);
```

---

## ✅ Resumo

* Baixo acoplamento
* Fácil troca de implementação
* Melhor para testes (mock)

---

# Object Calisthenics

## Regra 1 (Um nível de indentação por método)

> Cada método deve ter **apenas um nível de indentação**.

---

### 🧠 O que isso significa?

Você deve evitar código com muitos blocos aninhados (`if`, `for`, `while`, etc.).

👉 Se começou a “ir muito pra direita”, é um sinal claro de que:

* O método está fazendo **coisas demais**
* Precisa ser **quebrado em métodos menores**

---

### ❌ Exemplo incorreto

```java
public void processarPedido(Pedido pedido) {
    if (pedido != null) {
        if (pedido.estaPago()) {
            for (Item item : pedido.getItens()) {
                if (item.temEstoque()) {
                    enviarItem(item);
                }
            }
        }
    }
}
```

🚨 Problema:

* 3 níveis de indentação
* Difícil de ler
* Difícil de manter

---

### ✅ Exemplo correto

```java
public void processarPedido(Pedido pedido) {
    validarPedido(pedido);
    processarItens(pedido);
}

private void validarPedido(Pedido pedido) {
    if (pedido == null || !pedido.estaPago()) {
        throw new IllegalArgumentException();
    }
}

private void processarItens(Pedido pedido) {
    for (Item item : pedido.getItens()) {
        processarItem(item);
    }
}

private void processarItem(Item item) {
    if (item.temEstoque()) {
        enviarItem(item);
    }
}
```

---

### 💡 Benefícios

* Código mais **legível**
* Métodos menores e mais claros
* Facilita testes

---

### ✅ Resumo

* Evite “escadas” de `if/for`
* Extraia métodos
* Cada método deve fazer **uma coisa só**

---

## Regra 2 (Não use a palavra-chave `else`)

> Evite o uso de `else` para deixar o fluxo mais claro e direto.

---

### 🧠 O que isso significa?

Ao invés de usar `if/else`, você deve:

* Usar **retornos antecipados** (*early return, fail fast*)
* Separar responsabilidades
* Evitar bifurcações complexas

---

### ❌ Exemplo incorreto

```java
public void processarPagamento(Pagamento pagamento) {
    if (pagamento.estaValido()) {
        realizarPagamento(pagamento);
    } else {
        throw new IllegalArgumentException("Pagamento inválido");
    }
}
```

---

### ✅ Exemplo correto

```java
public void processarPagamento(Pagamento pagamento) {
    if (!pagamento.estaValido()) {
        throw new IllegalArgumentException("Pagamento inválido");
    }

    realizarPagamento(pagamento);
}
```

---

### 🔥 Exemplo mais interessante

```java
// ❌ Com else
if (usuario.isAdmin()) {
    liberarAcessoTotal();
} else {
    liberarAcessoLimitado();
}

// ✅ Sem else
if (usuario.isAdmin()) {
    liberarAcessoTotal();
    return;
}

liberarAcessoLimitado();
```

---

### 💡 Benefícios

* Fluxo mais **linear**
* Menos complexidade mental
* Evita código “aninhado”

---

### ✅ Resumo

* Prefira retornos antecipados
* Evite bifurcações desnecessárias
* Deixe o fluxo mais direto

---

## Regra 3 (Encapsule todos os primitivos e Strings)

> Tipos primitivos e Strings devem ser substituídos por **objetos que representem o domínio**.

---

### Regra principal

* ❌ Não use `String`, `int`, `double` diretamente para representar conceitos importantes
* ❌ Não deixe validações espalhadas pelo sistema
* ✅ Crie **Value Objects** com significado e regras de negócio
* ✅ Garanta que os dados já nasçam **válidos**

---

### Exemplo com **String**

#### 🧠 Contexto

Temos um `Usuario` com um email.

```java
// ❌ Forma incorreta: primitivo sem significado
class Usuario {
    private String email;
}
```

👉 Problema:

* Qualquer string pode ser atribuída
* Validação pode ficar espalhada pelo sistema (caso mais de um objeto no sistema utilize um email)

---

```java
// ✅ Forma correta: Value Object
class Email {
    private String email;

    public Email(String email) {
        if (!email.contains("@")) {
            throw new IllegalArgumentException("Email inválido");
        }
        this.email = email;
    }

    public String getValue() {
        return email;
    }
}

class Usuario {
    private Email email;
}

class Funcionario {
    private Email email;
}
```

👉 Benefício:

* Email **sempre válido**
* Regra centralizada

---

### Exemplo com **número**

#### 🧠 Contexto

Um produto tem um preço.

```java
// ❌ Forma incorreta
class Produto {
    private double preco;
}
```

---

```java
// ✅ Forma correta
class Preco {
    private double valor;

    public Preco(double valor) {
        if (valor < 0) {
            throw new IllegalArgumentException("Preço não pode ser negativo");
        }
        this.valor = valor;
    }

    public double getValor() {
        return valor;
    }
}

class Produto {
    private Preco preco;
}
```

---

### 💡 Insight

> Primitivos são "burros". Objetos carregam **comportamento + regra + significado**.

---

### ⚖️ Quando aplicar

👉 Use quando:

* Existe **regra de validação**
* O dado tem **significado no domínio**
* Você quer evitar erros comuns

👉 Evite quando:

* É algo trivial (ex: contador interno, loop, índice)

---

### ✅ Resumo

* Enriquece o modelo de domínio
* Centraliza validações
* Evita estados inválidos
* Deixa o código mais orientado a objetos

---

## Regra 9 (Evite Getters e Setters)

> Objetos devem proteger seu estado e expor comportamentos, não dados.

---

### Regra principal
* ❌ Não use getters para decisões de negócio fora da classe
* ❌ Não use setters genéricos
* ✅ Prefira métodos com intenção clara que contenham a regra de negócio

---

### Exemplo focado em **GETTER**

#### 🧠 Contexto

Imagine que temos um `Pedido` com um `status`.
Queremos enviar um e-mail quando o pedido estiver **ENVIADO**.

```java
// ❌ Forma incorreta: regra fora do objeto
if (pedido.getStatus().equals("ENVIADO")) { // regra fora do objeto
    enviarEmail();
}

// ✅ Forma correta: intenção clara
if (pedido.estaEnviado()) {
    enviarEmail();
}

// Dentro da classe Pedido
public boolean estaEnviado() {
    return status.equals("ENVIADO"); // encapsula regra
}
```

> ❗ Lembre-se: nunca use getters para decisões de negócio fora da classe.
> Prefira métodos que expressem **intenções** do objeto.

---

### Exemplo focado em **SETTER**

#### 🧠 Contexto

Imagine que temos um `Product` com um `price`.
Não devemos permitir que qualquer parte do sistema altere o preço diretamente.

```java
// ❌ Forma incorreta: setter genérico
product.setPrice(50); // altera estado sem regra de negócio

// ✅ Forma correta: método de domínio
product.applyDiscount(20);

// Dentro da classe Product
public void applyDiscount(double value) {
    if (this.price < value) {
        throw new IllegalStateException("O desconto não pode ser maior que o valor do produto"); // regra de negócio
    }
    this.price -= value;
}
```

> ❗ Setters genéricos quebram encapsulamento. Prefira métodos com **intenção clara**.

---

### Exemplo combinando **GETTER + SETTER** (boa prática)

#### 🧠 Contexto

Queremos criar um `Pedido` com um `status` inicial e depois aprová-lo.
O cliente do objeto não precisa manipular diretamente o status nem perguntar os detalhes internos.

```java
// ✅ Uso correto: comportamento explícito
pedido.aprovar();            // altera estado com regra interna
if (pedido.estaAprovado()) { // verifica estado de forma segura
    enviarEmail();
}

// Dentro da classe Pedido
public void aprovar() {
    if (this.status != PedidoStatus.PENDENTE) {
        throw new IllegalStateException("Pedido não pode ser aprovado"); // regra de negócio
    }
    this.status = PedidoStatus.APROVADO;
}

public boolean estaAprovado() {
    return this.status == PedidoStatus.APROVADO; // expõe intenção, não dado cru
}
```

> ✅ Combinando os dois:
>
> * O setter é substituído por um método com regra (`aprovar`)
> * O getter é substituído por um método de intenção (`estaAprovado`)
