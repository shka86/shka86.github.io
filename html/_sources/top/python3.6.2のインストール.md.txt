## python3.6.2のインストール
どうやら最初に書いた方法では、pipが使えなくなるようだ。

---
おソースを取ってきてmakeしてインストールする。
'python'のシンボリックリンクを更新して完了。

``` python
# インストール
sudo wget  https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
xz -dc Python-3.6.2.tar.xz | tar xfv -
cd Python-3.6.2
./configure # defaultでは/usr/local/binに入る
make
sudo make install

# 後日pipが入っていなくて困った。
# 同じディレクトリで下のようにやる。
sudo apt-get install libssl-dev
sudo make install

※エラー 404 Not Foundで うまくいかなかったら
sudo apt-get updateしてね

# おまけ
python3 -m pip -V # pipが入っているか確認
python3 -m pip freeze # 入っているパッケージの確認

```
