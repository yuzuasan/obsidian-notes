# 🧩 登場人物（役割）

| 役割         | 説明            |
| ---------- | ------------- |
| Originator | 状態を持つ本体       |
| Memento    | 状態のスナップショット   |
| Caretaker  | スナップショットを保管する |

---

# 📝 シンプルな例：「ゲームのセーブ機能」

* プレイヤーのHPを保存
* ダメージを受ける
* セーブ地点まで戻る（復元）

---

# ✅ 実装例（Java）

## ① Memento（状態のスナップショット）

```java
// Memento（スナップショット）
public class Memento {
    private final int hp;

    public Memento(int hp) {
        this.hp = hp;
    }

    // Originatorだけが使うための取得メソッド
    int getHp() {
        return hp;
    }
}
```

🔎 ポイント

* 外部から状態を変更できない（immutable）
* getterはpublicにしない（カプセル化を守る）

---

## ② Originator（状態を持つ本体）

```java
// Originator（状態を持つクラス）
public class GamePlayer {
    private int hp;

    public GamePlayer(int hp) {
        this.hp = hp;
    }

    public void damage(int amount) {
        hp -= amount;
        System.out.println("ダメージを受けた！HP: " + hp);
    }

    public void showStatus() {
        System.out.println("現在のHP: " + hp);
    }

    // 状態を保存
    public Memento save() {
        System.out.println("HPを保存します");
        return new Memento(hp);
    }

    // 状態を復元
    public void restore(Memento memento) {
        this.hp = memento.getHp();
        System.out.println("HPを復元しました！");
    }
}
```

🔎 ポイント

* save() → スナップショット作成
* restore() → 状態を復元
* 状態の詳細は外部に公開していない

---

## ③ Caretaker（保存係）

```java
// Caretaker（保存係）
public class GameCaretaker {
    private Memento memento;

    public void saveMemento(Memento m) {
        this.memento = m;
    }

    public Memento getMemento() {
        return memento;
    }
}
```

🔎 ポイント

* 状態の中身には触れない
* ただ保存しておくだけ

---

## ④ 実行クラス

```java
public class Main {
    public static void main(String[] args) {
        GamePlayer player = new GamePlayer(100);
        GameCaretaker caretaker = new GameCaretaker();

        player.showStatus();

        // セーブ
        caretaker.saveMemento(player.save());

        // ダメージ
        player.damage(30);
        player.showStatus();

        // 復元
        player.restore(caretaker.getMemento());
        player.showStatus();
    }
}
```

---

# 🖥 実行結果

```
現在のHP: 100
HPを保存します
ダメージを受けた！HP: 70
現在のHP: 70
HPを復元しました！
現在のHP: 100
```

---

# 🎓 この例で理解するポイント

### ✅ 1. カプセル化を守る

* CaretakerはHPの値を知らない
* Mementoの中身を直接触れない

---

### ✅ 2. 状態を壊さず退避

```java
Memento m = player.save();
```

→ オブジェクトのスナップショットを取得

---

### ✅ 3. 復元できる

```java
player.restore(m);
```

→ 過去の状態に戻せる
