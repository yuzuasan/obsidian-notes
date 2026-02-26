# 🎯 目的

### 本質

👉 **処理を連鎖させる**

### 今回のシナリオ

ユーザー登録時のバリデーション

* 必須チェック
* 文字数チェック
* メール形式チェック

を **if を並べる代わりにクラスを並べて処理** します。

---

# 🧠 クラス構成（パターン対応）

| 役割              | クラス                    | パターン上の意味 |
| --------------- | ---------------------- | -------- |
| Handler         | `Validator`            | 抽象ハンドラ   |
| ConcreteHandler | `RequiredValidator` など | 具体的な処理   |
| Client          | `Main`                 | 連鎖を組み立てる |

---

# 🧩 実装例

## ① Handler（抽象クラス）

```java
// Handler
abstract class Validator {

    private Validator next;

    // 次の処理をセット
    public Validator setNext(Validator next) {
        this.next = next;
        return next;
    }

    // バリデーション実行
    public void validate(String input) {
        check(input);

        if (next != null) {
            next.validate(input);
        }
    }

    // 各クラスで実装する処理
    protected abstract void check(String input);
}
```

---

## ② ConcreteHandler（具体的な処理）

### 必須チェック

```java
class RequiredValidator extends Validator {

    @Override
    protected void check(String input) {
        if (input == null || input.isEmpty()) {
            throw new IllegalArgumentException("必須項目です");
        }
    }
}
```

---

### 文字数チェック

```java
class LengthValidator extends Validator {

    @Override
    protected void check(String input) {
        if (input.length() < 5) {
            throw new IllegalArgumentException("5文字以上で入力してください");
        }
    }
}
```

---

### メール形式チェック

```java
class EmailFormatValidator extends Validator {

    @Override
    protected void check(String input) {
        if (!input.contains("@")) {
            throw new IllegalArgumentException("メール形式が正しくありません");
        }
    }
}
```

---

## ③ Client（連鎖の組み立て）

```java
public class Main {

    public static void main(String[] args) {

        // チェーンを構築
        Validator validator1 = new RequiredValidator();
        Validator validator2 = new LengthValidator();
        Validator validator3 = new EmailFormatValidator();

        validator1.setNext(validator2)
                  .setNext(validator3);

        // 実行
        try {
            validator1.validate("test@example.com");
            System.out.println("バリデーション成功！");
        } catch (Exception e) {
            System.out.println("エラー: " + e.getMessage());
        }
    }
}
```

---

# 🔄 処理の流れ

```
RequiredValidator
        ↓
LengthValidator
        ↓
EmailFormatValidator
```

`validator1.validate()` を呼ぶだけで、
処理が次々に流れていきます。

---

# 🔥 これが「if を並べる代わりにクラスを並べる」ということ

### ❌ if地獄パターン

```java
if (input == null) ...
if (input.length() < 5) ...
if (!input.contains("@")) ...
```

条件が増えるほど肥大化。

---

### ✅ Chain of Responsibility

* クラスを追加するだけ
* 既存コードを変更しない
* 条件が増えても整理された構造

---

# 🎓 学習ポイントまとめ

✔ 処理を「連鎖」させる
✔ クラスをつなげることで条件分岐を分割
✔ 新しい処理はクラス追加のみ
✔ 既存コードを変更しない（OCPに強い）
