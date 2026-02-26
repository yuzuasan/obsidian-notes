## 📌 テーマ

**温度センサー**

* 温度が変わる（イベント発行）
* 表示モニターやログ出力が自動で通知を受け取る

---

# 🏗 パターン構造

| 役割               | 説明          | 実装クラス             |
| ---------------- | ----------- | ----------------- |
| Subject          | 通知元         | TemperatureSensor |
| Observer         | 通知先インターフェース | Observer          |
| ConcreteObserver | 通知を受ける具体クラス | Display / Logger  |

---

# 💻 サンプルコード（Java）

```java
// Observer（通知を受け取る側のインターフェース）
interface Observer {
    void update(float temperature);
}

// Subject（通知を送る側のインターフェース）
interface Subject {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// ConcreteSubject（具体的な通知元）
class TemperatureSensor implements Subject {

    private java.util.List<Observer> observers = new java.util.ArrayList<>();
    private float temperature;

    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void setTemperature(float temperature) {
        this.temperature = temperature;
        notifyObservers();  // 🔔 変化が起きたら通知
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature);
        }
    }
}

// ConcreteObserver①（表示）
class Display implements Observer {
    @Override
    public void update(float temperature) {
        System.out.println("Display: 現在の温度は " + temperature + " 度です");
    }
}

// ConcreteObserver②（ログ記録）
class Logger implements Observer {
    @Override
    public void update(float temperature) {
        System.out.println("Logger: 温度が " + temperature + " に変更されました");
    }
}

// 動作確認用クラス
public class Main {
    public static void main(String[] args) {

        TemperatureSensor sensor = new TemperatureSensor();

        Observer display = new Display();
        Observer logger = new Logger();

        // 🔗 疎結合で登録
        sensor.addObserver(display);
        sensor.addObserver(logger);

        // 温度変更（イベント発行）
        sensor.setTemperature(25.0f);
        sensor.setTemperature(30.5f);
    }
}
```

---

# 🔍 パターンとコードの対応関係

## ① 通知元がイベントを発行

```java
sensor.setTemperature(25.0f);
```

⬇

```java
notifyObservers();
```

👉 **主導権はイベント発行側**

---

## ② 通知先は疎結合

```java
interface Observer
```

TemperatureSensor は
「Observerという型」しか知らない。

👉 Display や Logger の具体実装を知らない
👉 副作用を分離できる

---

## ③ 横方向に拡張できる

新しい機能を追加したい場合：

```java
class AlertSystem implements Observer {
    public void update(float temperature) {
        if (temperature > 35) {
            System.out.println("警告！高温です！");
        }
    }
}
```

既存コードは変更不要。

👉 OCP（Open Closed Principle）を守れる
👉 横に“広がる”構造

---

# 🌳 構造イメージ

```
           +------------------+
           | TemperatureSensor|
           +------------------+
                /    |    \
               /     |     \
          Display  Logger  Alert
```

縦ではなく、**横に拡張される**のがポイント。

---

# ✨ Observerパターンの本質

* 主導権は通知元
* イベント駆動
* 副作用の分離
* 横に広がる構造
