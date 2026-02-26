# ■ サンプル例：データ読み込み処理

### 🎯 想定シナリオ

* データ読み込み処理の流れは共通
* 読み込み方法だけファイル版とDB版で違う

---

# ■ クラス構成

```
AbstractDataProcessor（抽象クラス）
 ├─ FileDataProcessor
 └─ DatabaseDataProcessor
```

---

# ■ ① 抽象クラス（Templateを持つ）

```java
// 抽象クラス（Template Method を定義）
abstract class AbstractDataProcessor {

    // Template Method（処理の順序を固定）
    public final void process() {
        open();
        readData();   // ← 差し替えポイント
        close();
    }

    private void open() {
        System.out.println("リソースをオープンします");
    }

    protected abstract void readData(); // 子クラスに強制

    private void close() {
        System.out.println("リソースをクローズします");
    }
}
```

---

# ■ ② 具体クラス（ファイル版）

```java
class FileDataProcessor extends AbstractDataProcessor {

    @Override
    protected void readData() {
        System.out.println("ファイルからデータを読み込みます");
    }
}
```

---

# ■ ③ 具体クラス（DB版）

```java
class DatabaseDataProcessor extends AbstractDataProcessor {

    @Override
    protected void readData() {
        System.out.println("データベースからデータを読み込みます");
    }
}
```

---

# ■ ④ 実行クラス

```java
public class Main {
    public static void main(String[] args) {

        AbstractDataProcessor fileProcessor = new FileDataProcessor();
        fileProcessor.process();

        System.out.println("-----");

        AbstractDataProcessor dbProcessor = new DatabaseDataProcessor();
        dbProcessor.process();
    }
}
```

---

# ■ 実行結果

```
リソースをオープンします
ファイルからデータを読み込みます
リソースをクローズします
-----
リソースをオープンします
データベースからデータを読み込みます
リソースをクローズします
```

---

# ■ パターンとの対応関係

| パターン概念          | このコードでの対応    |
| --------------- | ------------ |
| Template Method | `process()`  |
| 処理順固定           | `final` 修飾子  |
| 差し替えポイント        | `readData()` |
| 実装強制            | `abstract`   |

---

# ■ なぜ Template Method なのか？

### ✔ 処理順は親が握る

```java
public final void process()
```

→ 子クラスは流れを変更できない

### ✔ 実装を強制できる

```java
protected abstract void readData();
```

→ 必ず実装させられる

### ✔ フローの破壊を防ぐ

`final` によりオーバーライド不可

---

# ■ このパターンが使われる場面

* バッチ処理
* データ取込フロー
* 共通手順を必ず守らせたい処理
* フレームワーク内部処理

---

# ■ 学習ポイントまとめ

Template Method は：

> 「アルゴリズムの骨組みを親クラスで定義し、
> 具体的な処理だけを子クラスに任せる」

というパターンです。
