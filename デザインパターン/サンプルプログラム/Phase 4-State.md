# 🎯 今回の例：信号機

信号は

* 青 → 「進め」
* 黄 → 「注意」
* 赤 → 「止まれ」

という **状態ごとに振る舞いが変わる** 典型例です。

---

# ❌ まずは悪い例（if文で分岐）

```java
class TrafficLight {
    private String state = "RED";

    public void action() {
        if (state.equals("RED")) {
            System.out.println("止まれ");
            state = "GREEN";
        } else if (state.equals("GREEN")) {
            System.out.println("進め");
            state = "YELLOW";
        } else if (state.equals("YELLOW")) {
            System.out.println("注意");
            state = "RED";
        }
    }
}
```

### 問題点

* 状態追加のたびにifが増える
* OCP違反
* 状態ロジックが1クラスに集中

---

# ✅ Stateパターン版

---

## ① Stateインターフェース

```java
interface State {
    void handle(TrafficLight context);
}
```

👉 状態と振る舞いを一体化

---

## ② 各ConcreteState

### 🟥 赤状態

```java
class RedState implements State {
    @Override
    public void handle(TrafficLight context) {
        System.out.println("止まれ");
        context.setState(new GreenState());
    }
}
```

### 🟢 青状態

```java
class GreenState implements State {
    @Override
    public void handle(TrafficLight context) {
        System.out.println("進め");
        context.setState(new YellowState());
    }
}
```

### 🟡 黄状態

```java
class YellowState implements State {
    @Override
    public void handle(TrafficLight context) {
        System.out.println("注意");
        context.setState(new RedState());
    }
}
```

---

## ③ Contextクラス

```java
class TrafficLight {

    private State state;

    public TrafficLight() {
        state = new RedState(); // 初期状態
    }

    public void setState(State state) {
        this.state = state;
    }

    public void change() {
        state.handle(this);
    }
}
```

👉 Contextは状態に処理を委譲するだけ
👉 分岐なし！

---

## ④ 実行クラス

```java
public class Main {
    public static void main(String[] args) {
        TrafficLight light = new TrafficLight();

        for (int i = 0; i < 5; i++) {
            light.change();
        }
    }
}
```

---

# 🧠 実行結果

```
止まれ
進め
注意
止まれ
進め
```

---

# 🔎 パターンとの対応関係

| パターン要素        | 今回の例                                    |
| ------------- | --------------------------------------- |
| State         | `State`インターフェース                         |
| ConcreteState | `RedState`, `GreenState`, `YellowState` |
| Context       | `TrafficLight`                          |
| 状態遷移          | 各State内で `context.setState()`           |

---

# 💡 なぜこれが良いのか？

## ✔ 状態と振る舞いを一体化

「赤のとき何をするか」は `RedState` に閉じ込められる

## ✔ 分岐が消える

Contextにifが存在しない

## ✔ OCPを守れる

例えば「点滅状態」を追加する場合：

* `BlinkingState` を追加するだけ
* `TrafficLight`は変更不要

## ✔ ドメイン知識が構造になる

「信号の状態遷移」がクラス構造として表現されている

---

# 🎓 Stateパターンの本質

Stateパターンは

> 「オブジェクトの状態をオブジェクトとして扱う」

という設計です。

---

# 📌 使いどころ

* ワークフロー
* 注文ステータス
* ゲームキャラクター状態
* 接続状態（接続中 / 切断 / 再接続）
