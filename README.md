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
__________
| funcao2 |
| funcao1 |
|  main   |
|_________|
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

## Regra 9 (Evite Getters e Setters)

> Objetos devem proteger seu estado e expor comportamentos, não dados.

---

## Regra principal
* ❌ Não use getters para decisões de negócio fora da classe
* ❌ Não use setters genéricos
* ✅ Prefira métodos com intenção clara que contenham a regra de negócio

---

## Exemplo focado em **GETTER**

### 🧠 Contexto

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

## Exemplo focado em **SETTER**

### 🧠 Contexto

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

## Exemplo combinando **GETTER + SETTER** (boa prática)

### 🧠 Contexto

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
