### 🏦 レガシーシステム（変更できない）

```java
public class LegacyPaymentSystem {

    // typeCode: "01"=クレジット, "02"=銀行振込
    public void executePayment(String typeCode, int amount) {
        System.out.println("Legacy決済実行: typeCode=" + typeCode + ", amount=" + amount);
    }
}
```

* typeCode は "01" や "02"
* 呼び出し側にこの仕様を漏らしたくない

---

# 🎯 新しい理想インターフェース

```java
public interface PaymentService {
    void pay(String paymentType, int amount);
}
```

* 呼び出し側は `"CREDIT"` や `"BANK"` を使いたい

---

# 🔁 Adapter 実装

```java
public class PaymentAdapter implements PaymentService {

    private final LegacyPaymentSystem legacyPaymentSystem;

    public PaymentAdapter(LegacyPaymentSystem legacyPaymentSystem) {
        this.legacyPaymentSystem = legacyPaymentSystem;
    }

    @Override
    public void pay(String paymentType, int amount) {

        // ここで翻訳（Adapterの役割）
        String typeCode;

        switch (paymentType) {
            case "CREDIT":
                typeCode = "01";
                break;
            case "BANK":
                typeCode = "02";
                break;
            default:
                throw new IllegalArgumentException("未対応の支払い種別");
        }

        legacyPaymentSystem.executePayment(typeCode, amount);
    }
}
```

---

# 🚀 利用側（クライアント）

```java
public class Main {
    public static void main(String[] args) {

        PaymentService paymentService =
                new PaymentAdapter(new LegacyPaymentSystem());

        paymentService.pay("CREDIT", 1000);
        paymentService.pay("BANK", 2000);
    }
}
```

---

# 🧠 クラス構造（対応関係）

| 役割          | クラス                   |
| ----------- | --------------------- |
| Target（新IF） | `PaymentService`      |
| Adapter     | `PaymentAdapter`      |
| Adaptee（既存） | `LegacyPaymentSystem` |
| Client      | `Main`                |

---

# 🔍 どこが Adapter なのか？

### ✅ インターフェースを合わせている

* `pay(String paymentType, int amount)`
* → `executePayment(String typeCode, int amount)`

### ✅ レガシー仕様を隠蔽

* "01" や "02" は Adapter の中だけに存在

### ✅ 変更が局所化

もし typeCode が変わっても、
**修正箇所は Adapter だけ**

---

# 🎓 覚え方

> 「既存コードを変更せずに接続する翻訳機」

* 既存APIに合わせるのではなく
* 呼び出し側が使いやすいIFを作り
* Adapterが間で変換する
