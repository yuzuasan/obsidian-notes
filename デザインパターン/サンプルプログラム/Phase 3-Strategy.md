# 💳 サンプル例：決済処理

## 1️⃣ Strategyインターフェース（戦略）

```java
// Strategy
public interface PaymentStrategy {
    void pay(int amount);
}
```

👉 「支払う」というアルゴリズムの抽象化

---

## 2️⃣ 具体的なStrategy（戦略の実装）

```java
// ConcreteStrategy① クレジットカード
public class CreditCardPayment implements PaymentStrategy {

    @Override
    public void pay(int amount) {
        System.out.println("クレジットカードで " + amount + " 円支払いました");
    }
}
```

```java
// ConcreteStrategy② PayPay
public class PayPayPayment implements PaymentStrategy {

    @Override
    public void pay(int amount) {
        System.out.println("PayPayで " + amount + " 円支払いました");
    }
}
```

👉 アルゴリズム（支払い方法）だけが違う

---

## 3️⃣ Context（戦略を使う側）

```java
// Context
public class PaymentContext {

    private PaymentStrategy strategy;

    // Strategyを差し替え可能
    public void setStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void executePayment(int amount) {
        strategy.pay(amount);
    }
}
```

👉 Contextは「どう支払うか」を知らない
👉 「支払う」という操作をStrategyに委譲している

---

## 4️⃣ 実行クラス

```java
public class Main {

    public static void main(String[] args) {

        PaymentContext context = new PaymentContext();

        // クレジットカードで支払う
        context.setStrategy(new CreditCardPayment());
        context.executePayment(1000);

        // PayPayで支払う（差し替え）
        context.setStrategy(new PayPayPayment());
        context.executePayment(2000);
    }
}
```

---

# 🔥 実行結果

```
クレジットカードで 1000 円支払いました
PayPayで 2000 円支払いました
```

---

# 🧠 パターンとコードの対応関係

| パターン要素           | この例                               |
| ---------------- | --------------------------------- |
| Strategy         | PaymentStrategy                   |
| ConcreteStrategy | CreditCardPayment / PayPayPayment |
| Context          | PaymentContext                    |
| アルゴリズム           | 支払い処理                             |

---

# 🌟 なぜこれがStrategyなのか？

### ✔ アルゴリズムを差し替えている

```java
context.setStrategy(new PayPayPayment());
```

ここで「支払いロジック」を切り替えている。

---

### ✔ if/switchが存在しない

悪い例：

```java
if (type == CREDIT) { ... }
else if (type == PAYPAY) { ... }
```

Strategyなら：

```java
strategy.pay();
```

---

# 🎯 メリットの実感ポイント

✅ if/switch削減
✅ 新しい決済追加時はクラスを増やすだけ
✅ テスト時にモックを差し替え可能
✅ Contextは変更不要（OCP：開放閉鎖原則）

---

# 📌 さらにシンプルにした版（Map利用）

ご提示いただいた形に近い実装：

```java
import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {

        Map<String, PaymentStrategy> strategies = new HashMap<>();
        strategies.put("credit", new CreditCardPayment());
        strategies.put("paypay", new PayPayPayment());

        strategies.get("credit").pay(3000);
    }
}
```

---

# 🏁 まとめ

Strategyパターンの本質は：

> **「振る舞い」をオブジェクトとして切り出し、差し替え可能にすること**
