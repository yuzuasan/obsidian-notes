# 🎯 例：注文処理システム

## ❌ Facadeなし（複雑な状態）

Controller が Domain の複数クラスに直接アクセスしている状態：

```
Controller
   ↓
PaymentService
InventoryService
ShippingService
```

呼び出し側は

* 在庫確認
* 支払い処理
* 配送手配

の順番を **全部知っていないといけない**

→ 心理的ハードルが高い 😇

---

# ✅ Facadeあり（窓口を用意）

```
Controller
   ↓
OrderFacade  ← ★窓口
   ↓
PaymentService
InventoryService
ShippingService
```

Controller は

```java
orderFacade.placeOrder(...)
```

だけ呼べばよい。

---

# 🧩 サンプルコード（シンプル版）

## ① Domain層（複雑なサブシステム）

### 在庫サービス

```java
public class InventoryService {
    public boolean checkStock(String itemId) {
        System.out.println("在庫確認中...");
        return true;
    }
}
```

### 支払いサービス

```java
public class PaymentService {
    public void processPayment(String itemId) {
        System.out.println("支払い処理中...");
    }
}
```

### 配送サービス

```java
public class ShippingService {
    public void shipItem(String itemId) {
        System.out.println("配送手配中...");
    }
}
```

---

## ② Facade（窓口クラス）

ここがパターンの主役です。

```java
public class OrderFacade {

    private InventoryService inventoryService;
    private PaymentService paymentService;
    private ShippingService shippingService;

    public OrderFacade() {
        this.inventoryService = new InventoryService();
        this.paymentService = new PaymentService();
        this.shippingService = new ShippingService();
    }

    // ★ シンプルな窓口
    public void placeOrder(String itemId) {

        if (!inventoryService.checkStock(itemId)) {
            System.out.println("在庫がありません");
            return;
        }

        paymentService.processPayment(itemId);
        shippingService.shipItem(itemId);

        System.out.println("注文完了！");
    }
}
```

---

## ③ Controller（呼び出し側）

```java
public class OrderController {

    public static void main(String[] args) {

        OrderFacade orderFacade = new OrderFacade();

        // Controllerはこれだけ知っていればいい
        orderFacade.placeOrder("ITEM-001");
    }
}
```

---

# 🔎 パターンとの対応関係

| パターン要素    | この例                                                 |
| --------- | --------------------------------------------------- |
| 複雑なサブシステム | InventoryService / PaymentService / ShippingService |
| Facade    | OrderFacade                                         |
| 呼び出し側     | Controller                                          |
| 目的        | 複数のDomain操作を1つのメソッドにまとめる                            |
| 効果        | ControllerがDomainの詳細を知らなくてよい                        |

---

# 💡 重要ポイント（試験・実務で問われるところ）

### Facadeは「機能追加」ではない

Facadeは

❌ 新しいビジネスロジックを作る
⭕ 既存処理をまとめて簡単にする

---

### 依存の隠蔽が本質

Controllerは

```java
InventoryService
PaymentService
ShippingService
```

の存在を知らない。

知っているのは：

```java
OrderFacade
```

だけ。

👉 **依存を減らす**
👉 **心理的ハードルを下げる**

---

# 🧠 覚え方

> 「呼び出し側を楽にするための窓口」

Facade = 建物の「正面玄関」

裏で何が動いているかは知らなくていい。
