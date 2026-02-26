# 🎯 例：ボタンとテキストボックスを調停するダイアログ

### 💡 仕様

* チェックボックスがONならボタンを有効化
* OFFならボタンを無効化
* ボタンやチェックボックスは**お互いを直接知らない**
* すべての調整は **Mediator（ダイアログ）** が行う

---

# 🧠 パターン構造と対応関係

| パターン要素            | 今回のクラス               |
| ----------------- | -------------------- |
| Mediator          | `Mediator` インターフェース  |
| ConcreteMediator  | `Dialog`             |
| Colleague         | `UIComponent`        |
| ConcreteColleague | `CheckBox`, `Button` |

---

# 🧩 実装コード（できるだけシンプル）

```java
// Mediator
interface Mediator {
    void notify(UIComponent sender, String event);
}

// ConcreteMediator
class Dialog implements Mediator {

    private CheckBox checkBox;
    private Button button;

    public void setCheckBox(CheckBox checkBox) {
        this.checkBox = checkBox;
    }

    public void setButton(Button button) {
        this.button = button;
    }

    @Override
    public void notify(UIComponent sender, String event) {
        if (sender == checkBox && event.equals("check")) {
            if (checkBox.isChecked()) {
                button.setEnabled(true);
            } else {
                button.setEnabled(false);
            }
        }
    }
}

// Colleague
abstract class UIComponent {
    protected Mediator mediator;

    public UIComponent(Mediator mediator) {
        this.mediator = mediator;
    }
}

// ConcreteColleague1
class CheckBox extends UIComponent {

    private boolean checked = false;

    public CheckBox(Mediator mediator) {
        super(mediator);
    }

    public void check() {
        checked = !checked;
        System.out.println("CheckBox: " + (checked ? "ON" : "OFF"));
        mediator.notify(this, "check");
    }

    public boolean isChecked() {
        return checked;
    }
}

// ConcreteColleague2
class Button extends UIComponent {

    private boolean enabled = false;

    public Button(Mediator mediator) {
        super(mediator);
    }

    public void setEnabled(boolean enabled) {
        this.enabled = enabled;
        System.out.println("Button: " + (enabled ? "有効" : "無効"));
    }
}

// 実行クラス
public class Main {
    public static void main(String[] args) {

        Dialog dialog = new Dialog();

        CheckBox checkBox = new CheckBox(dialog);
        Button button = new Button(dialog);

        dialog.setCheckBox(checkBox);
        dialog.setButton(button);

        // ユーザー操作
        checkBox.check();  // ON → ボタン有効
        checkBox.check();  // OFF → ボタン無効
    }
}
```

---

# 🔎 重要ポイントの解説

## ✅ 1. オブジェクト同士を直接結ばない

```java
// これがないのが重要
// checkBox.setButton(button); ← こうしない！
```

CheckBoxはButtonを知らない。
ButtonもCheckBoxを知らない。

---

## ✅ 2. 依存を中央に集約

依存はすべて `Dialog` に集中：

```
CheckBox → Dialog ← Button
```

網の目依存（A→B, B→C, C→A…）が
放射状依存に変わる。

---

## ✅ 3. 「相互調整」に強い

UIのように、

* Aが変わるとBが変わる
* Bが変わるとCが変わる
* 条件が複雑

こういうケースで威力を発揮します。

---

# ⚠ 注意点（実感できる部分）

`Dialog` の中を見てください：

```java
if (sender == checkBox && event.equals("check")) {
    ...
}
```

コンポーネントが増えると：

```java
if (...) { ... }
else if (...) { ... }
else if (...) { ... }
```

👉 **神クラス化**
👉 条件分岐の集中

ここがMediatorパターンの弱点です。

---

# 🆚 Mediatorを使わない場合

CheckBoxがButtonを直接保持：

```
CheckBox → Button
Button → TextField
TextField → Label
```

変更時に影響範囲が広がる。

Mediatorを使うと：

```
CheckBox → Dialog ← Button
                 ← TextField
                 ← Label
```

影響範囲が局所化される。

---

# 🎓 学習観点まとめ

### Mediatorの本質

* 「仲介」ではなく **「調停」**
* コミュニケーションのルールを中央に閉じ込める
* 横連携ではなく「相互調整」
