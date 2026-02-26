# 💡 例：PaymentService

### 🎬 シナリオ

* `PaymentService` に支払い機能がある
* 既存コードは変更したくない
* 後から「ログ機能」を追加したい

---

# 🧱 クラス構成（役割とパターン対応）

| 役割                | クラス                       | 説明         |
| ----------------- | ------------------------- | ---------- |
| Component         | `PaymentService`          | 共通インターフェース |
| ConcreteComponent | `BasicPaymentService`     | 元の実装       |
| Decorator         | `PaymentDecorator`        | 包む抽象クラス    |
| ConcreteDecorator | `LoggingPaymentDecorator` | ログ機能追加     |

---

# 🧩 サンプルコード（Java）

```java
// Component
interface PaymentService {
    void pay(int amount);
}

// ConcreteComponent（元の機能）
class BasicPaymentService implements PaymentService {
    @Override
    public void pay(int amount) {
        System.out.println(amount + "円を支払いました。");
    }
}

// Decorator（抽象デコレーター）
abstract class PaymentDecorator implements PaymentService {
    protected PaymentService paymentService;

    public PaymentDecorator(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}

// ConcreteDecorator（機能追加）
class LoggingPaymentDecorator extends PaymentDecorator {

    public LoggingPaymentDecorator(PaymentService paymentService) {
        super(paymentService);
    }

    @Override
    public void pay(int amount) {
        System.out.println("[LOG] 支払い開始: " + amount + "円");
        paymentService.pay(amount);  // 元の処理を呼び出す
        System.out.println("[LOG] 支払い終了");
    }
}

// 動作確認
public class Main {
    public static void main(String[] args) {

        // 元のサービス
        PaymentService service = new BasicPaymentService();

        // ログ機能を追加（包む）
        PaymentService loggingService = 
            new LoggingPaymentDecorator(service);

        loggingService.pay(1000);
    }
}
```

---

# ▶ 実行結果

```
[LOG] 支払い開始: 1000円
1000円を支払いました。
[LOG] 支払い終了
```

---

# 🔎 どこがDecoratorなのか？

### ✅ ① 同じインターフェースを実装

```java
abstract class PaymentDecorator implements PaymentService
```

### ✅ ② 元オブジェクトを保持

```java
protected PaymentService paymentService;
```

### ✅ ③ 元の処理を呼び出している

```java
paymentService.pay(amount);
```

---

# 🧠 なぜこれが「変更せずに機能追加」なのか？

* `BasicPaymentService` は一切変更していない
* ログ機能は外側から追加している
* 呼び出し側は `PaymentService` しか見ていない

つまり：

> オープン・クローズド原則（OCP）を満たしている

---

# 🎓 応用（重ねがけ可能）

Decoratorは**何重にも重ねられる**のが強みです。

```java
PaymentService service =
    new LoggingPaymentDecorator(
        new BasicPaymentService()
    );
```

さらに `AuthPaymentDecorator` を作れば：

```java
PaymentService service =
    new LoggingPaymentDecorator(
        new AuthPaymentDecorator(
            new BasicPaymentService()
        )
    );
```

これが「横断的処理を後付けできる」という意味です。

---

# 🚀 実務イメージ

* Spring のトランザクション
* AOP ログ出力
* Servlet Filter
* IO の `BufferedReader`
