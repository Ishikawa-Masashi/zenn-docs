---
title: "弾幕記述用ライブラリ Bullet MLの紹介"
emoji: "👻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Typescript,ゲーム制作]
published: true 
---

この記事はまだ未完成です。
何回かにわけて記事を書いていきます。

# はじめに

長 健太(ABA Games)氏が制作したシューティングゲーム「Torus Trooper」をHTML5(Typescript)に移植しました。

[Torus Trooper](https://musical-basbousa-3a06f4.netlify.app/)

その際にTorus Trooperで使用されていたBullet MLもTypescriptに移植したので紹介します。

# 弾幕記述用ライブラリ Bullet ML

デモを用意したのでご覧ください。

[Bullet ML](https://dreamy-unicorn-c6955e.netlify.app/)

Bullet MLを使えばシューティングゲームにおける弾幕をTypescriptで定義することが出来ます。

```typescript
export const danmaku = new Root({
  top: action(
    repeat(
      999,
      repeat(
        30,
        fire(direction(13, 'sequence'), speed(5), bullet(actionRef('b'))),
        repeat(
          9 - 1,
          fire(direction(360 / 9, 'sequence'), speed(5), bullet(actionRef('b')))
        ),
        wait(2)
      ),
      wait(30),
      repeat(
        30,
        fire(
          direction(-12, 'sequence'),
          speed(5),
          bullet(actionRef('b'), { color: 'hsl(220, 60%, 80%)' })
        ),
        repeat(
          9 - 1,
          fire(
            direction(360 / 9, 'sequence'),
            speed(5),
            bullet(actionRef('b'), { color: 'hsl(220, 60%, 80%)' })
          )
        ),
        wait(2)
      ),
      wait(30)
    )
  ),
  b: action(
    changeSpeed(speed(1), 30),
    wait(30),
    changeDirection(direction(0, 'aim'), 60),
    changeSpeed(speed(3), 30),
    wait(50),
    vanish(),
    fire(speed(2), bullet({ color: 'hsl(50, 60%, 80%)' }))
  ),
});
```