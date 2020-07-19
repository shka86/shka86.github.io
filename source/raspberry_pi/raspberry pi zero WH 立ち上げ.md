# raspberry pi zero WH 立ち上げ

またしてもメモ

## OSインストール
- 公式サイトからOSをダウンロードする

普通は最新版を落とすところだけど、Pi3と同じバージョンがほしいので
[ここ](https://downloads.raspberrypi.org/)
からjessieのlite版を持ってきた。

- SDカードにOSを入れる
etcherを使う

echo "deb https://dl.bintray.com/resin-io/debian stable etcher" | sudo tee /etc/apt/sources.list.d/etcher.list

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 379CE192D401AB61

sudo apt install etcher-electron



sudo mkfs.vfat -v -c -F 32 /dev/sde