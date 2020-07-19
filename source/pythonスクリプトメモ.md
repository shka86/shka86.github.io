<!--
{"id":"17391345971635326534","title":"pythonスクリプトメモ","categories":[],"draft":false}
-->
# pythonスクリプトメモ
## Shebang
- シバンは環境にあわせて
- マジックコメントは、文字エンコードを指定する。とりあえずutf-8に統一しておく。

``` python
#!/usr/bin/python
# -*- coding: utf-8 -*-

print("Hello World!")
```

## ファイル関連
``` python
# 存在確認
os.path.isfile(path)

# ファイル名を取得
os.path.basename(path)

# ファイルコピー
shutil.copyfile(src, dst, *, follow_symlinks=True)

# ファイル削除
os.remove(path)

# write file
f = open(filename, 'w') # 追記は'a'
f.write(text)
f.close()

# read file
f = open(filename, 'r')
text = f.read()
f.close()
print(text)
```


## ディレクトリ関連
``` python
# ディレクトリ作成
os.mkdir(path)

# 存在確認
os.path.isdir(path)

# パス名を取得
os.path.dirname(path)

# ディレクトリコピー（上書きはエラー）
shutil.copytree(src, dst)

# ディレクトリコピー
from distutils.dir_util import copy_tree
copy_tree(src, dst)

# ディレクトリ削除（ファイルがあるとエラー）
os.rmdir(path)

# ディレクトリ削除（ファイルがあってもOK）
shutil.rmtree(path)

# カレントディレクトリを取得
os.getcwd()
```


## リンク関連
``` python
# シンボリックリンク作成
os.symlink(src, dst)

# 存在確認
os.path.islink(path)
```

## その他
``` python
# パスの存在確認
os.path.exists(path)

```
