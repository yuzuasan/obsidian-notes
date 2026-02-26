# 🎯 例：電気のON / OFF

## 🎭 登場人物（構造との対応）

| パターン     | 今回の例                                |
| -------- | ----------------------------------- |
| Command  | `LightOnCommand`, `LightOffCommand` |
| Receiver | `Light`                             |
| Invoker  | `RemoteController`                  |
| Client   | `Main`                              |

---

# ✅ サンプルコード（最小構成）

```java
// Command（やることの共通インターフェース）
interface Command {
    void execute();
}
```

---

```java
// Receiver（実際の処理を持つクラス）
class Light {
    public void on() {
        System.out.println("ライトをONにします");
    }

    public void off() {
        System.out.println("ライトをOFFにします");
    }
}
```

---

```java
// ConcreteCommand（ON処理）
class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.on();
    }
}
```

---

```java
// ConcreteCommand（OFF処理）
class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.off();
    }
}
```

---

```java
// Invoker（実行者）
class RemoteController {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}
```

---

```java
// Client（組み立て役）
public class Main {
    public static void main(String[] args) {

        // Receiver
        Light light = new Light();

        // Command
        Command lightOn = new LightOnCommand(light);
        Command lightOff = new LightOffCommand(light);

        // Invoker
        RemoteController remote = new RemoteController();

        remote.setCommand(lightOn);
        remote.pressButton();  // ON実行

        remote.setCommand(lightOff);
        remote.pressButton();  // OFF実行
    }
}
```

---

# 🧠 パターンと実装の対応理解

## ① 「やること」をオブジェクト化

```java
Command lightOn = new LightOnCommand(light);
```

👉 「ライトをONにする」という行為そのものをオブジェクトにしている

---

## ② Invokerは処理内容を知らない

```java
command.execute();
```

RemoteControllerは

* ライトを知らない
* ONなのかOFFなのかも知らない
* ただ execute() を呼ぶだけ

👉 **実行主体の分離**

---

## ③ 変動点

> * 実行される処理そのもの

ONやOFF以外にも：

```java
class LightDimCommand implements Command { ... }
class FanOnCommand implements Command { ... }
class TvOnCommand implements Command { ... }
```

Invokerは一切変更不要。

---

# 💪 Commandパターンの強みとの対応

| 強み      | この例でどう拡張できる？           |
| ------- | ---------------------- |
| 遅延実行    | List<Command> に溜めて後で実行 |
| キュー投入   | Queueに入れて順番にexecute    |
| 再実行     | 同じCommandを再度execute    |
| Undo    | undo() を追加すれば可能        |
| ログ保存    | 実行Commandを保存できる        |
| 実行主体の分離 | Invokerはexecuteしか知らない  |

---

# 🎓 なぜこれがCommandパターンなのか？

通常ならこう書いてしまいます：

```java
remote.turnOnLight();
```

でもそれだと：

* リモコンがLightを知っている
* 処理が固定される
* 拡張に弱い

Commandパターンでは：

> 「操作」そのものをオブジェクトにした

これが本質です。
