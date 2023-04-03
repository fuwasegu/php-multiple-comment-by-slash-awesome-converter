# PHPer 必携！
https://awesome-converter.fuwasegu.com/

# こんなこと思ったことありませんか．．．？
Laravel のソースコードリーディングをしていて．．．
たとえば，[Illuminate\Database\Concerns\ManagesTransactions.php](https://github.com/laravel/framework/blob/10.x/src/Illuminate/Database/Concerns/ManagesTransactions.php) を見ているときに．．．

```php
public function transaction(Closure $callback, $attempts = 1)
{
    for ($currentAttempt = 1; $currentAttempt <= $attempts; $currentAttempt++) {
        $this->beginTransaction();

        // We'll simply execute the given callback within a try / catch block and if we
        // catch any exception we can rollback this transaction so that none of this
        // gets actually persisted to a database or stored in a permanent fashion.
        try {
            $callbackResult = $callback($this);
        }

        // If we catch an exception we'll rollback this transaction and try again if we
        // are not out of attempts. If we are out of attempts we will just throw the
        // exception back out, and let the developer handle an uncaught exception.
```

ワイ「なんか長いコメントがあるな！」

ワイ「英語読めへんから，DeepL 先生に聞いてみよか！」

ワイこのままコピペしてっと．．．

![readme-1](https://user-images.githubusercontent.com/52437973/229556886-f797d4bf-ead1-4b89-bc8a-a9d31646cbd5.png)

ワイ「うーん．スペースもあるし，先頭のスラッシュも 2 行目以降は残ってまう」

ワイ「スラッシュのせいで文が切れてしまって翻訳も微妙や」

ワイ「毎回消すの面倒くさいな．．．」

ワイ「そうや！」

ワイ「この，『PHP のスラッシュで書かれた複数行コメントをいい感じに整形して翻訳しやすくするやつ』を使えばええんや！」

![readme-2](https://user-images.githubusercontent.com/52437973/229557456-23771f21-98bc-409e-853e-6c08163270b7.png)

ワイ「わーい！一瞬で整形されたで！」

ワイ「あとはクリップボードにコピーして，DeepL に貼り付けるだけや〜！」
