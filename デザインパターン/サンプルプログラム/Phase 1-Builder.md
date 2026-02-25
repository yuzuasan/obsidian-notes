# 🎯 例：ユーザー登録情報（User）

## ❌ Builderを使わない場合の問題

```java
User user = new User(
    "taro",
    "taro@example.com",
    "password123",
    20,
    true
);
```

* 引数が多い
* 順番を間違える
* nullが混じる
* 不正状態のまま生成される可能性

---

# ✅ Builderを使った実装例

## ① 完成品クラス（不変）

```java
public class User {

    private final String username;
    private final String email;
    private final String password;
    private final int age;
    private final boolean active;

    private User(Builder builder) {
        this.username = builder.username;
        this.email = builder.email;
        this.password = builder.password;
        this.age = builder.age;
        this.active = builder.active;
    }

    public String getUsername() { return username; }
    public String getEmail() { return email; }
    public int getAge() { return age; }
    public boolean isActive() { return active; }

    // --- Builder ---
    public static class Builder {

        private final String username;   // 必須
        private final String email;      // 必須

        private String password = "default";
        private int age = 0;
        private boolean active = true;

        // 必須項目はコンストラクタで受ける
        public Builder(String username, String email) {
            this.username = username;
            this.email = email;
        }

        public Builder password(String password) {
            this.password = password;
            return this;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public Builder active(boolean active) {
            this.active = active;
            return this;
        }

        public User build() {

            // 🔐 バリデーションを閉じ込める
            if (username == null || username.isEmpty()) {
                throw new IllegalStateException("usernameは必須です");
            }

            if (!email.contains("@")) {
                throw new IllegalStateException("email形式が不正です");
            }

            if (age < 0) {
                throw new IllegalStateException("ageは0以上です");
            }

            return new User(this);
        }
    }
}
```

---

## ② 使用例

```java
User user = new User.Builder("taro", "taro@example.com")
        .password("secret")
        .age(20)
        .active(true)
        .build();
```

---

# 🔎 この例で理解すべきポイント

## ① 引数が多くても可読性が高い

```java
.age(20)
.password("secret")
```

→ 何を設定しているか明確

---

## ② 完成済みオブジェクトしか作れない

* コンストラクタは `private`
* `build()` 以外から生成不可
* 途中状態は外に出ない

---

## ③ 不変条件を守れる

* `username` は必須
* `email` 形式チェック
* `age >= 0`

👉 **未完成状態のUserは存在できない**

---

# 🧠 本質の理解

### Builderが解決する問題

* 引数が多い
* 順番ミス
* 可読性低下
* 中途半端な状態の発生

---

# 💡 業務設計とのつながり

あなたの整理がとても重要です：

## ❌ データ中心設計

* DTOだけ作る
* ロジックはServiceに集中
* Service肥大化

## ✅ 状態遷移中心設計

* ドメインが振る舞いを持つ
* 不変条件はドメイン内部に閉じ込める

Builderはその補助技術。

---

# 🎯 一言で言うと

> 「正しい状態のオブジェクトしか作れない仕組み」
