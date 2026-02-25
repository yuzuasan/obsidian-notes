# ① ダメと言われがちな「素朴な Singleton」

「アプリ全体で1つしか存在しない設定クラス」という例です。

```java
public class AppConfig {

    // 唯一のインスタンス
    private static final AppConfig instance = new AppConfig();

    // コンストラクタをprivateにして外部からnewできないようにする
    private AppConfig() {
        System.out.println("AppConfig initialized");
    }

    // グローバルアクセスポイント
    public static AppConfig getInstance() {
        return instance;
    }

    // 何かの設定値
    private String appName = "MyApp";

    public String getAppName() {
        return appName;
    }
}
```

利用側：

```java
public class Main {
    public static void main(String[] args) {

        AppConfig config1 = AppConfig.getInstance();
        AppConfig config2 = AppConfig.getInstance();

        System.out.println(config1 == config2); // true
        System.out.println(config1.getAppName());
    }
}
```

### ✔ 何が起きているか

* `new` できない（コンストラクタがprivate）
* `getInstance()` で常に同じインスタンスを返す
* アプリ全体で1個

---

## ❗ 問題点（あなたが書いている通り）

* ほぼグローバル変数
* テスト時に差し替えできない
* どこからでも呼べてしまう（隠れ依存）
* 状態が共有される

例：

```java
AppConfig.getInstance().getAppName();
```

これがどこでも書ける → 依存が見えない

---

# ② 推奨される考え方（Singletonを自分で作らない）

現代的な設計では：

> Singletonは「言語で作る」のではなく
> DIコンテナで管理する

例えば（Springのイメージ）

```java
@Component
public class AppConfig {

    private String appName = "MyApp";

    public String getAppName() {
        return appName;
    }
}
```

利用側：

```java
@Component
public class UserService {

    private final AppConfig appConfig;

    // コンストラクタインジェクション
    public UserService(AppConfig appConfig) {
        this.appConfig = appConfig;
    }

    public void printAppName() {
        System.out.println(appConfig.getAppName());
    }
}
```

### ✔ 何が違うか

* 自分でSingletonを書かない
* newしない
* DIコンテナが1インスタンスだけ生成
* 依存がコンストラクタに明示される

---

# 🔎 イメージまとめ

## ❌ 古いSingleton

```java
SomeClass.doSomething();
Logger.getInstance().log("hello");
```

→ どこから依存してるか見えない

---

## ✅ DI管理

```java
public SomeClass(Logger logger) {
    this.logger = logger;
}
```

→ 依存が見える
→ テストでモックに差し替え可能

---

# 🎯 まとめ

### Singletonパターンとは？

* インスタンスを1つだけに制限するパターン
* グローバルアクセスポイントを提供する

### しかし現代では？

* 自分でSingletonを実装しない
* DIコンテナに任せる
* 依存はコンストラクタで受け取る
