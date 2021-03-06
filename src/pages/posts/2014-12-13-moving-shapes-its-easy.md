---
templateKey: blog-post
title: 図形の移動が、こんなに簡単に実装できる時代になりました
date: 2014-12-13T00:00:00.000+09:00
tags:
  - foss4g
  - ReactiveX
  - Xamarin
---
　これは [FOSS4G Advent Calendar 2014 12日目](http://qiita.com/advent-calendar/2014/foss4goss4g) の記事です。

　FOSS4G と言えば GIS、GIS と言えば図形編集ですね。図形を追加したり移動したり回転したりできる機能です。面倒なんですよ、これプログラミングするの。

　なにが面倒かというと、色んな状態（マウスの状態＜左/右ボタンが押されている/押されてない、マウスダウン時の座標、現在の座標＞、図形の状態＜選択されている/いない＞）などなどがコードの中に入り乱れて、スパゲッティコードになりがちというか「なります」。
<!--more-->

　例えば「図形の移動」のフローは、

1. 図形をマウスダウン（＝選択）
2. そのままマウスムーブ（＝移動）
3. マウスボタンを離して終了

と、極めて単純なんですね。これが普通にコーディングするとフラグや状態管理の嵐になってしまう。

　と言ってた時代は終わりました。
　例えば、下の画面。

![](/img/posts/simply_shape_dragging_using_rx_01.gif)


　これは、白い四角形をドラッグで移動できるというスマホアプリの例ですが、これの実装の主要部分はたったの **６行** です。

```csharp
rectangle.DownEvent() // 1.図形をマウスダウン
    .SelectMany(rectangle.MoveEvent())  // 2.そのままマウスムーブ
    .Subscribe(e => {
        rectangle.SetX(e.RawX); // 移動の度に図形を移動
        rectangle.SetY(e.RawY);
    });
```

　このコードをよく見ると、上に書いたフローと似ているのが分かります。人が考えたままコードに落とし込める。しかもフラグとか状態管理とかのゴミが一切ない。素晴らしい！(3. に該当するコードが必要な気がするけどまあいいや）

　これを実現しているのは[リアクティブプログラミング](http://ninjinkun.hatenablog.com/entry/introrxja)という概念。なんでもかんでもストリーム(時系列にデータが降ってくる何か)で捉えよう、イベントでさえも。イベントはストリームであるので、あとはストリームの加工や他のストリームとの合成でどうにかできてしまいます。

　リアクティブ＋図形うんぬんの他の例は、

* [RxJS + Canvas](http://act.neue.cc/rxjs/canvas.htm)

などがあります。これは HTML なのですぐ試せますしコード（Javascript）も見られます。

　リアクティブプログラミング用の著名なライブラリはほとんどオープンソース、リアクティブプログラミング＋FOSS4G で **RxGIS** （なんかカッコいいから言ってみたかっただけ）

　いつかまたGIS作るみたいな仕事があったら、絶対 Rx 使ってつくるぞ！と思ってますのでよろしくお願いします。

（上のコード例の全コードは [gist](https://gist.github.com/amay077/1d22ba8ffa8ad95e9393) にあります。）

