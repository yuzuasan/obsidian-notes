## 🧠 今回のシンプルな例：フォルダ構造

実務例にもある

> フォルダ → サブフォルダ → ファイル

を使います。

* **ファイル** → 単体（Leaf）
* **フォルダ** → 集合（Composite）
* どちらも「表示する（display）」という同じ操作を持つ

---

# 🏗 クラス構造（パターンとの対応）

| 役割        | クラス         | 説明         |
| --------- | ----------- | ---------- |
| Component | `Entry`     | 共通インターフェース |
| Leaf      | `File`      | 子を持たない     |
| Composite | `Directory` | 子を持つ       |
| Client    | `Main`      | 利用側        |

---

# 💻 サンプルコード（できるだけシンプル）

```java
// Component
abstract class Entry {
    public abstract void display(String indent);
}
```

```java
// Leaf
class File extends Entry {
    private String name;

    public File(String name) {
        this.name = name;
    }

    @Override
    public void display(String indent) {
        System.out.println(indent + "- File: " + name);
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

// Composite
class Directory extends Entry {
    private String name;
    private List<Entry> entries = new ArrayList<>();

    public Directory(String name) {
        this.name = name;
    }

    public void add(Entry entry) {
        entries.add(entry);
    }

    @Override
    public void display(String indent) {
        System.out.println(indent + "+ Directory: " + name);

        for (Entry entry : entries) {
            entry.display(indent + "  ");  // 再帰呼び出し
        }
    }
}
```

```java
// Client
public class Main {
    public static void main(String[] args) {

        Directory root = new Directory("root");
        File file1 = new File("file1.txt");
        File file2 = new File("file2.txt");

        Directory subDir = new Directory("sub");
        subDir.add(new File("subFile1.txt"));

        root.add(file1);
        root.add(file2);
        root.add(subDir);

        root.display("");
    }
}
```

---

# ▶ 実行結果

```
+ Directory: root
  - File: file1.txt
  - File: file2.txt
  + Directory: sub
    - File: subFile1.txt
```

---

# 🔎 パターン理解ポイント

## ① 単体と集合を同じ型で扱っている

```java
List<Entry> entries
```

* `File` も `Directory` も `Entry`
* 呼び出し側は区別しない

---

## ② 再帰的な木構造処理

```java
entry.display(indent + "  ");
```

Directoryの中にDirectoryが入れられるため
**再帰で木構造を処理できる**

---

## ③ Clientは違いを意識しない

```java
root.add(file1);
root.add(subDir);
```

どちらも `Entry` なので同じ操作で追加できる。

---

# 🎯 Compositeの効果とコードの対応

| 効果          | コードでの該当箇所        |
| ----------- | ---------------- |
| 木構造の再帰処理    | `display()` 内の再帰 |
| 単体と集合を同じ操作  | `Entry` を継承      |
| 呼び出し側が意識しない | `Entry` 型で統一     |

---

# 🧩 まとめ

Compositeは

> 「部分」と「全体」を同じインターフェースで扱う

パターンです。

今回の例では：

* File（個）
* Directory（集合）

を `Entry` で統一することで

✅ 再帰処理が簡単
✅ 呼び出し側がシンプル
✅ 木構造に強い設計

になります。
