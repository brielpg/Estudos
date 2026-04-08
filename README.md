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
        throw new IllegalStateException("O desconto não pode ser menor que o valor do produto"); // regra de negócio
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
