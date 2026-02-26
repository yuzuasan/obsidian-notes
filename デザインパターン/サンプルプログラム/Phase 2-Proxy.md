# ■ Proxyパターンの簡単な例（Java）

## 🎯 シナリオ

「高額決済の場合だけ承認チェックを挟む」

* `Payment` … インターフェース（共通の窓口）
* `RealPayment` … 本来の決済処理
* `PaymentProxy` … 承認チェックを挟む代理オブジェクト

---

# ■ クラス構成（役割対応）

| 役割          | クラス            | 説明               |
| ----------- | -------------- | ---------------- |
| Subject     | `Payment`      | 共通インターフェース       |
| RealSubject | `RealPayment`  | 本来の処理            |
| Proxy       | `PaymentProxy` | 横断的処理（承認チェック）を追加 |

---

# ■ サンプルコード

```java
// Subject
interface Payment {
    void pay(int amount);
}

// RealSubject
class RealPayment implements Payment {
    @Override
    public void pay(int amount) {
        System.out.println(amount + "円を決済しました。");
    }
}

// Proxy
class PaymentProxy implements Payment {

    private RealPayment realPayment;

    public PaymentProxy() {
        this.realPayment = new RealPayment();
    }

    @Override
    public void pay(int amount) {

        // ★ 横断的処理（承認チェック）
        if (amount > 100000) {
            System.out.println("高額決済のため承認が必要です。");
            if (!approve()) {
                System.out.println("承認されませんでした。");
                return;
            }
        }

        // 本来の処理を呼び出す
        realPayment.pay(amount);
    }

    private boolean approve() {
        System.out.println("管理者が承認しました。");
        return true;
    }
}

// 動作確認
public class Main {
    public static void main(String[] args) {
        Payment payment = new PaymentProxy();

        payment.pay(5000);     // 通常決済
        System.out.println("----");
        payment.pay(200000);   // 高額決済
    }
}
```

---

# ■ 実行結果

```
5000円を決済しました。
----
高額決済のため承認が必要です。
管理者が承認しました。
200000円を決済しました。
```

---

# ■ この例で理解するポイント

## ① 呼び出し側はProxyを意識しない

```java
Payment payment = new PaymentProxy();
payment.pay(5000);
```

呼び出し側は **Paymentインターフェースしか知らない**
→ これが「同じインターフェースで扱える」の意味

---

## ② RealPaymentは一切変更していない

```java
class RealPayment implements Payment
```

決済処理の本体には承認ロジックを書いていない
→ 横断的処理を外から挟んでいる

---

## ③ 「包む」イメージ

```
呼び出し
   ↓
Proxy（チェック）
   ↓
RealPayment（本処理）
```

これが覚え方の

> 元オブジェクトを包んで機能を挟む

という意味です。

---

# ■ この例は何Proxy？

これは **Protection Proxy（保護プロキシ）** に近い例です。

他の代表例：

* Virtual Proxy → Lazy Load
* Cache Proxy → 結果を保存
* Logging Proxy → ログ出力

---

# ■ Proxyパターンの本質まとめ

✔ インターフェースは同じ
✔ 本体を変更しない
✔ 代理が前後に処理を挟む
✔ 呼び出し側は気づかない
