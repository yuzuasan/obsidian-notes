# 🎨 サンプル：UIテーマ生成

## ① 部品インターフェース

```java
// Buttonインターフェース
public interface Button {
    void render();
}

// Checkboxインターフェース
public interface Checkbox {
    void render();
}
```

---

## ② ライトテーマ実装

```java
public class LightButton implements Button {
    @Override
    public void render() {
        System.out.println("Light Button");
    }
}

public class LightCheckbox implements Checkbox {
    @Override
    public void render() {
        System.out.println("Light Checkbox");
    }
}
```

---

## ③ ダークテーマ実装

```java
public class DarkButton implements Button {
    @Override
    public void render() {
        System.out.println("Dark Button");
    }
}

public class DarkCheckbox implements Checkbox {
    @Override
    public void render() {
        System.out.println("Dark Checkbox");
    }
}
```

---

## ④ Abstract Factory（ここが本体）

```java
public interface UIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```

---

## ⑤ 各テーマのFactory

```java
public class LightUIFactory implements UIFactory {

    @Override
    public Button createButton() {
        return new LightButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new LightCheckbox();
    }
}
```

```java
public class DarkUIFactory implements UIFactory {

    @Override
    public Button createButton() {
        return new DarkButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new DarkCheckbox();
    }
}
```

---

## ⑥ クライアント側

```java
public class Application {

    private final Button button;
    private final Checkbox checkbox;

    public Application(UIFactory factory) {
        this.button = factory.createButton();
        this.checkbox = factory.createCheckbox();
    }

    public void renderUI() {
        button.render();
        checkbox.render();
    }

    public static void main(String[] args) {

        // テーマを切り替えるだけでセットが変わる
        UIFactory factory = new LightUIFactory();
        // UIFactory factory = new DarkUIFactory();

        Application app = new Application(factory);
        app.renderUI();
    }
}
```

---

# 🔎 これがAbstract Factoryの本質

## ✔ 生成のセットを固定する

LightUIFactory を渡せば：

* LightButton
* LightCheckbox

が必ず生成される。

DarkUIFactory を渡せば：

* DarkButton
* DarkCheckbox

が必ず生成される。

👉 **テーマ混在を防げる**
👉 クライアントは具体クラスを知らない

---

# 🎯 パターンのイメージ

```
            UIFactory
                ↑
   -------------------------
   ↑                       ↑
LightUIFactory        DarkUIFactory
   |                       |
LightButton          DarkButton
LightCheckbox        DarkCheckbox
```

---

# 🧠 まとめ

| ポイント   | 内容                   |
| ------ | -------------------- |
| 目的     | 関連する生成群をまとめる         |
| 何が嬉しい？ | セットの整合性が保証される        |
| 本質     | 生成の「族」を固定する          |
| 使い所    | UIテーマ、DB種別、OS依存処理 など |
