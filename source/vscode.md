vscode関係
===

sublime text 3 環境に近づけるために導入したextentions
---

- Monokai Extended

- Sublime Text Keymap and Settings

- Python-autopep8  
    別途autopep8のインストールが必要

- Python  
    lintingとかやってくれるそうなので



- insertNums


キーボードショートカット
---

- Insert Date String  
    キーボードショートカットに "Insert Date" を "ctrl + ;" に設定する。  
    zoom機能がdefaultで登録されているようですが、構わず削除
- Shift+Enter でダブルスペース改行  
    テキスト編集時のDefault は Find Previous になっている。これは削除。  
    さらに下記を追加する。

    ```json
    {
        "key": "shift+enter",
        "command": "type",
        "args": {
            "text": "  \n"
        },
        "when": "editorTextFocus"
    }
    ```

- crtl+shift+w: word wrap に変更



snippet 関連
---
- snippet を優先して表示  
settings.jsonに追加 
`"editor.snippetSuggestions": "top"`

- snippet のタブストップ中に入力補完できるようにする  
settings.jsonに追加 
`"editor.suggest.snippetsPreventQuickSuggestions": false`

- snippet が効かないとき  
Global は出てくるけど scope 限定したスニペットはキーワード打っただけでは出てこない仕様っぽい。
Ctrl+Space すると出てくる。


