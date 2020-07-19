# RaspberryPi3ModelBインストール
Raspberry Pi 3 Model B のインストールから初期設定までの作業メモです。

## SDカード準備
- SD Formatter 4.0でフォーマットする。（クイックで構わない）
- NOOBSを展開してSDに入れる
    - 「NOOBS_v_2_4_0」フォルダではなく、その中身をSD直下に置く。

## インストール
- SDカードを本体にセットして電源を接続する。
- 言語は日本語に(何でもいいけど)
- Raspbian with PIXELにチェック。
- 左上、インストールをクリックしてしばらく待つ。


## その他設定
正確にはインストールではないですが、流れでやっておきたいことなので、ここに書いておきます。

- Raspberry Piの設定
    - ロケール：多分そのままでいい
        - 言語：ja (japanese)
        - 国：JP (Japan)
        - 文字セット：UTF-8
    - タイムゾーン：お好みで
    - キーボード：
        - Country：日本
        - Variant：日本語
    - 無線LANの国設定
        - 国：JP Japan
- wifi設定
    - 右上にwifi設定アイコンをクリックして任意のアクセスポイントを選択・パスワードを入力する
- rootパスワード変更
```
sudo passwd root
//変えなくても良いみたい
//初期状態（sudo kate /etc/shadowで"*"となっている場合）はログイン不可
```
- piのパスワード変更
```
passwd pi
```
## 日本語環境 fcitx-mozcをインストール
- とりあえずアップデート
```
sudo apt-get update
```
- fcitxをインストール
```
sudo apt-get install fcitx-mozc -y
//yで後の[Y/n]確認を先にしておく
```
- 入力メソッドを設定
```
im-config -n fcitx
```
- 再起動
```
reboot
```

- 通りの操作が済んだら、右上に「キーボード」または「あ」のアイコンが追加されているはず。

## samba
- インストール
```
//インストールして、
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install samba
//確認！
smbd -V
Version 4.1.17-Debian
```

- 設定を追記します。
```
sudo vim /etc/samba/smb.conf
//末尾に追記
[pi]
comment = Raspberry Pi
path = /home/pi
guest ok = yes
read only = no
public = yes
browsable = yes
force user = pi
```

- sambaを再起動します。
```
$ sudo service smbd restart
$ sudo service nmbd restart
```

- Windowsからアクセスします。
エクスプローラのアドレスバーに
ラズパイのIPを入力すると見えます。
```
//こんな感じ
\\xxx.xxx.xxx.xxx
```

## windowsからssh接続する環境
- Windows側の準備
  - Tera Termのインストール
  [https://osdn.net/projects/ttssh2/:title]

  - X-mingのインストール
  X window forwardingで窓を飛ばすのに使用

  - ~~(Option)~~ atom + remote-FTP
  ~~ドキュメントをwindows側から編集できるけど、使い勝手がイマイチ悪い。。。atomだけで完結できないか模索中~~
  とりあえずremote-FTPの設定は下記のようにすればつながる。
  なぜかdefaultの.ftpconfigを編集して接続を試みてもうまくいかなかった。いらなさそうなものを削って繋がったのが下記。
```
{
    "protocol": "sftp",
    "host": "<IP Address>",
    "port": デフォルトは22(ダブルコーテーション不要),
    "user": "<User Name>",
    "pass": "<Password>",
    "remote": "/",
    "connTimeout": 10000,
    "pasvTimeout": 10000,
    "keepalive": 10000,
    "watch": [],
    "watchTimeout": 500
}
```


- ラズパイ側の準備
  - sshオプション設定
     - sudo raspi-config
```
> 5 Interfacing Options > P2 SSH > YES
```

  - 固定IPを設定する
  /etc/dhcpcd.conf を変更する
```
interface wlan0
static ip_address=192.168.N.M/L
static routers=192.168.N.1
static domain_name_servers=192.168.N.1
//なんでこうするかはよく知らない
```

  - X11-appsのインストール
  接続テストにxeyesを使いたいため
```
sudo apt-get install X11-apps
```

- 疎通確認
  - X-mingでXserverを起動しておく
  - Tera Termで新しい接続を開始
  →プロンプトが表示されたらssh接続は成功
  - xeyesで目玉が飛んできたらwindow forwardingまで成功

## Raspberry Piの起動を確認できるように小細工
- /boot/config.txt に追記
```
dtparam=act_led_trigger=heartbeat
```
- reboot すると、起動中は緑LEDが鼓動する

以上おわり。
