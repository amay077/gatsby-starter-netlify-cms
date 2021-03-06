---
templateKey: blog-post
title: "DroidKaigi2019 でクロスプラットフォーム開発ツールについて話しました"
date: 2019-02-11T00:00:00.000+09:00
tags:
  - Kotlin
  - Android
  - DroidKaigi
---
2019.2.7〜2.8 に行われた [DroidKaigi2019](https://droidkaigi.jp/2019/) に登壇させてもらいました。
参加者としての感想は [別に書きました](https://qiita.com/amay077/items/ed43ef822c34677d2254)。
<!--more-->

![](/img/posts/2019_02_10_droidkaigi2019.png)

## 登壇

「[クロスプラットフォームモバイルアプリ開発ツール総ざらい2019 〜Titanium MobileからKotlin/Nativeまで〜](https://droidkaigi.jp/2019/timetable/70891)」というタイトルで登壇してきました。

RoomC に来ていただいた方々、ありがとうございます。
観ていない方は、資料や動画もすでに公開(早い！)していただいているので、よければ観てみてください。

* 資料 - [クロスプラットフォームモバイルアプリ開発ツール総ざらい2019 〜Titanium Mobile から Kotlin/Native まで〜 #droidkaigi - Speaker Deck](https://speakerdeck.com/amay077/native-made-number-droidkaigi)
* セッション動画 - [YouTube](https://youtu.be/51SW52cf2UY)

コルーチンや LiveData+MVx まわりの事は他の人の方がガッツリやっていてライバルが多いだろうという事と、自分が近年注力していることで DroidKaigi に CfP を出せるのはやはりクロスプラットフォーム関連しかないなという事で、今回のネタになりました。

セッションの内容は、

* [Xamarin と React Native と Flutter の違いを正しく理解しよう - Qiita](https://qiita.com/amay077/items/dff88e7ce6868615a9bb)

の内容を30分で話すために、簡潔に整理して私の最新の視点を加えたものです。

改めて、「まとめ」だけ引用して振り返りましょうか。

* モバイルクロスプラットフォーム開発ツールは必要悪
* どのツールもオワコンではない
* Kotlin／Native には言語の壁を超えられる魅力がある
* プラットフォームとその言語へのリスペクトを忘れずに
* Webアプリとも仲良くやっていこう

クロスプラットフォーム開発ツールは、十分な開発リソース・期間・保守コストが確保できれば使う必要はないわけです。しかし、現実には大企業でも、イケイケなサービス企業でも、プロジェクト単位・チーム単位ではリソースは制限されていて、クロスプラットフォーム開発ツールが利用検討対象に挙がることはよくあるのだと思います。
正直、「どんなツールを選択すべきか？」はどうでもいいです。現実的には提供企業の規模とあなたのチームのスキルセットでだいたい選択肢は絞られるので、「あなたはその答えをもう持っているのだから…」とか返答しましょう。

クロスプラットフォーム流行の歴史では、私の観測範囲内でこれまでに登場してきたツールについて触れました。Xamarin 利用歴が一番長いので、視点がそれよりになってしまったかもですが、極力特定のツールに依存しない話にしたつもりです。
"Titanium" を知らない、読み方がわからないという方が一定数いらっしゃる事を知ったときには、 **「モバイルクロスプラットフォーム開発ツール老人会」** の発足が頭をよぎりましたね。

各ツールの説明にはややdisりが含まれていたかも知れません(そう感じた方にはすみません)が、どのツールもdisconにはなっておらず(disconになったツールはそもそも紹介してない)、世界的に見れば利用されている方は多いと思います。
"とある開発ツール" を利用する(あるいは利用しない)のには、それなりの理由があるのですから、その理由を理解しようとしないまま「オワコンだ」とか「成功しない」とかは言わない方がよいと思います。それよりは、利用した／しなかった 理由についての知識を溜め、自分のケースに当てはめて判断したらよいと考えています。

Kotlin/Native に関しては、他言語向けに親和性の高いライブラリをビルド&出力できる開発ツールは、モバイル関連では他に実用レベルに至っているものを知りません(.NET/C# における同類技術である [.NET Embedding コードネーム:Embeddinator-4000](https://github.com/mono/Embeddinator-4000) は、開発が停滞しているというウワサも聞きます)。
Android/Kotlin の Google / JetBrains / OSS 周辺の開発パワーはとても高いので、急速に環境が整備されていくのだろうなと感じています。

となると、Android/iOS アプリの多くの領域を Kotlin で書けるようになるため、「Kotlin/Native強硬派」が現れると思うのですが、それについてこれまで Swift で iOS アプリを開発していた人たちがどう思うかは十分に話し合って導入して欲しいと思います。敵対関係になってしまってはまったく意味がないです。(逆の立場だったらどうでしょう？)

「ガワネイティブ」は、脊髄反射で「NO」と言わない方がよい技術であることもお話しました。
SPA, PWA に代表される Web 技術は、確実にネイティブアプリの領域と重なって来ています。
クロスプラットフォームアプリ開発技術者としては、 **「PWA などのWeb技術の海」と、「ネイティブアプリ技術の陸地」の波打ち際** に注目していて、2019年2月の現時点だと、「クロスプラットフォーム開発ツールで作るガワネイティブアプリ」は、有力な「おとしどころ」だと思っています。

話さなかった(知識不足で話せなかった)ことに関して言えば、WebAssembly があります。
例えば、「ガワネイティブアプリの中にある HTML ページの div タグ内でネイティブのUIパーツが利用される」などという世界線があるのかも知れないし、ぜんぜん無いのかも知れないです。

なんやかんやでクロスプラットフォームアプリ開発ツールに関連する領域は、モバイルだけを見てもまだまだネタに尽きないですし、モバイルに拘らなければ無限にありますので、ウォッチしていて飽きないですね。

とりあえず来年の DroidKaigi には **Kotlin/Native with Multi Platform Project に関するセッションが10個以上はある** と思っています。今、CfP を考えてみても、

* 実践！Kotlin/Native with MPP アプリ開発
* Kotlin MPP に対応済のライブラリたち
* Kotlin/Native ＋ xxx(←任意のクロスプラットフォーム開発ツール)
* Kotlin MPP を踏まえたアプリケーション設計手法
* Kotlin/Native for XXX を作って(!)みた

などなど、挙げたらキリがないですね。
来年 CfP を出すとしても、セッションを聞くとしてもとても楽しみです。

## コミュニケーション

わざわざ声をかけていただいて「Qiita の投稿、勉強になってます！」などと言って頂いたのは死ぬほど嬉しかったです。
前々回も、同じように若いITエンジニアさんに声かけていただいて、承認要求充足おじさんでした。
ただそれが目的にならないように、たくさんの人からいいね!されるよりは、誰か一人が「超助かった」と言ってもらえるようなアウトプットを心がけたい思っています。

パーティでの「登壇者風船プレイ」も良かったですね(風船を付けたのは数年前の de:code 以来でした)。
こちらからグイグイいくタイプでないので、風船のおかげで何人かの人に声をかけてもらえました。
お話ししていただいた皆さん、ありがとうございました。

## おわりに

スタッフの皆さま、今回も最高のイベントでした。
スムースな Registration に会場移動、セッション終了時刻を意図的にズラしての流量調整など、イベントのプロでも実施できるチームは少ないのではないでしょうか、素晴らしい運営だったと思います。

遠方からのスピーカーに対するサポート強化もありがたかったです。
できましたら、(パーティ始まりに?)スタッフの皆様の紹介をしていただけたら、個別にごあいさつできたのですが。。。
(メール対応していただいた方の名前と Twitter アカウントと顔が一致しないとか)

DroidKaigi には毎年参加していて、今回含め2度登壇させてもらってますが、やはり登壇した方が楽しいですね。
また、次回があると信じていますが、その時はなんらかのネタで登壇を狙いたいと思います。

ありがとうございました！
