Windows10上でUbuntuを使いたい
===

使うといっても、自作のプログラムの動作確認に使う目的で。
単体でubuntuマシンを立ち上げられるならそれが一番いいと思う。

ちなみにこの方法だとGUIは起動しません。

1. WSLを有効にする

        コンパネ > プログラム > Windowsの機能の有効化または無効化 > 「Windows Subsystem for Linux」 にチェック


1. Windowsを再起動

1. Microsoft Store から Ubuntu をインストール

        好きなバージョンを選べばよい

1. 起動 ～ 初期設定

        「起動」を押して少し待った後、 username と password を設定する

        最初ソフトウェアの更新を済ませる。
        sudo apt update && sudo apt upgrade
        途中で何度か返答を求められるので適宜入力する。

1. 日本語設定

        sudo apt install language-pack-ja && sudo apt install manpages-ja

1. rootになれるようにする

        ルートのパスワードを設定すればいい
        sudo passwd root

1. ついでにpython3までいれる

        python3.7以上を入れると多分 lib_release 関連で躓く
        その時は /usr/bin/lsb_release のシバンを 3.6 に指定してやると解消する。
        これでいいのかは知らん。


と、ここまでやってubuntuを動かしてみた結果、純粋なlinuxとは挙動が異なる部分が出てきたので、投げた。
つぎはVMwareかな。
