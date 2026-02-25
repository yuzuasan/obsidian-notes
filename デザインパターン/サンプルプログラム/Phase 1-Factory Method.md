# 🧩 例：メッセージ作成アプリ

メッセージを作るアプリを考えます。

* `Message` … 抽象製品
* `EmailMessage` / `SmsMessage` … 具体製品
* `MessageCreator` … 抽象Creator（Factory Methodを持つ）
* `EmailCreator` / `SmsCreator` … 具体Creator

---

# 📌 クラス構成イメージ

```
MessageCreator
   └─ createMessage() ← Factory Method
        └─ EmailCreator
        └─ SmsCreator
```

---

# 💻 サンプルコード（Java）

```java
// ===== 製品インターフェース =====
interface Message {
    void send();
}

// ===== 具体製品 =====
class EmailMessage implements Message {
    @Override
    public void send() {
        System.out.println("Emailを送信します");
    }
}

class SmsMessage implements Message {
    @Override
    public void send() {
        System.out.println("SMSを送信します");
    }
}

// ===== Creator（Factory Methodを持つ抽象クラス）=====
abstract class MessageCreator {

    // ★ Factory Method
    protected abstract Message createMessage();

    // 生成されたオブジェクトを使う共通処理
    public void sendMessage() {
        Message message = createMessage(); // ← newしない！
        message.send();
    }
}

// ===== 具体Creator =====
class EmailCreator extends MessageCreator {
    @Override
    protected Message createMessage() {
        return new EmailMessage();
    }
}

class SmsCreator extends MessageCreator {
    @Override
    protected Message createMessage() {
        return new SmsMessage();
    }
}

// ===== 実行クラス =====
public class Main {
    public static void main(String[] args) {

        MessageCreator creator1 = new EmailCreator();
        creator1.sendMessage();

        MessageCreator creator2 = new SmsCreator();
        creator2.sendMessage();
    }
}
```

---

# 🔍 何がポイント？

### ❌ Factory Method を使わない場合

```java
Message message = new EmailMessage(); // 具体クラスに依存
```

→ 呼び出し側が具体クラスを知ってしまう

---

### ✅ Factory Method を使うと

```java
MessageCreator creator = new EmailCreator();
creator.sendMessage();
```

→ 呼び出し側は **MessageCreator だけ知っていればよい**

---

# 🎯 なぜ OCP 改善になる？

新しい種類を追加する場合：

```java
class PushMessage implements Message { ... }
class PushCreator extends MessageCreator { ... }
```

👉 既存コードを変更せず、クラス追加だけで拡張できる。

---

# 🧠 まとめ（イメージ）

Factory Method は

> 「new をサブクラスに追い出すパターン」

* 生成を分離する
* 具体依存を隠す
* 拡張に強くする
