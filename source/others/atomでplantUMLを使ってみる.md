シーケンス図やフローチャートは、ビジュアル的に訴えられるので強いですよね。
visioみたいなお絵かきソフトは、きれいな図を描こうと思ったらある程度時間をとられます。
操作感もクセがあって、積極的に使いたいとは思えない。
なので、テキストベースでパパっと作ってしまうおうという作戦です。

## 材料
- atom
  - plantuml-viewer
- Graphviz
- Java（JREのほうでいい。portableでパスを通すのでもいけそう）
- 先達の知恵

## plantuml-viewerの導入
だいたい分かるな？
SettingsのCharsetは"utf-8"

## Graphviz（の中のdot.exe）
1. Graphviz Download

  [http://www.graphviz.org/Download_windows.php:title]

2. 環境に合ったzipを落としてきて解凍する
  これを書いたときは graphviz-2.38
  .../graphviz-2.38\release\bin\dot.exe

3. plantuml-viewerの
  GraphvizDot Executableに上記パスを入力する。

  以上で準備完了

## 動作確認
ここが役に立ちそう
[https://qiita.com/ogomr/items/0b5c4de7f38fd1482a48:title]

plantuml-viewer
ショートカット：Ctrl+Alt+p

※atomは一度落とさないとだめかも

---
なんとなく動作確認的なことをしてみたものの、、、微妙
```
digraph G {
size ="4,4";
subgraph cluster0{
  start [shape=box]; /* this is a comment */
  start -> step1;
  edge [color=red]; // so is this


  node [shape=box,style=filled,color=".7 .3 1.0"];
  step1 -> step2;
}

  node [shape=default,style=outline,color=black];
  step2 -> step3 [style=bold,label="comment"];

subgraph cluster1{
  step3 [shape=diamond];
  step3 -> step4 [style=dotted];
  step4 [shape=ellipse];
  step4 -> end [style=dotted];
  end -> end[label="hoge"];
}

step1 -> make_string;
make_string [label="branch"];

}

```
