sphinx環境立ち上げ記録＠win10
===

環境をそろえる
---
1. install python3.8.1
[https://www.python.org](https://www.python.org/)

1. install sphinx
```
pip install sphinx
```

1. support markdown
```
pip install commonmark recommonmark sphinx-markdown-tables
```

1. get theme
```
pip install sphinx_rtd_theme
```

プロジェクトを立ち上げる
---

1. generate project
```
mkdir sphinx_work
cd sphinx_work
sphinx-quickstart -q -p "test_prj" -a author_name -v 1.0 -l ja prj_dir --sep
```

- githubにupすることを念頭に置いて
`--ext-githubpages`をつけておくと、.nojekyllファイルを作ってくれるという
 


[https://www.sphinx-doc.org/ja/master/man/sphinx-quickstart.html](https://www.sphinx-doc.org/ja/master/man/sphinx-quickstart.html)



見た目を整える
---

1. source/conf.pyの編集  
※conf.pyはsourceとbuildを分けなかった場合は、プロジェクトdirの直下に置かれる。


```py
# -- Path setup --------------------------------------------------------------
# enable to use markdown
from recommonmark.parser import CommonMarkParser

# enable reST extension on markdown source
from recommonmark.transform import AutoStructify

# enable rtd theme
import sphinx_rtd_theme

# -- Project information -----------------------------------------------------
project = 'test_prj'
copyright = '2020, author_name'
author = 'author_name'
version = '1.0'
release = '1.0'

# -- General configuration ---------------------------------------------------
extensions = [
    'sphinx_markdown_tables',
]

templates_path = ['_templates']

language = 'ja'

exclude_patterns = []

source_suffix = ['.rst', '.md']
source_parsers = {
    '.md': CommonMarkParser,
}

# -- Options for HTML output -------------------------------------------------
html_theme = "sphinx_rtd_theme"

html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]

html_style = "css/my_theme.css"

html_static_path = ['_static']

```

1. theme をちょっとカスタマイズ
`_static/css/my_theme.css`を作成。場所を間違えるとcss全部適用されない。

```css
@import url("theme.css");
 
.wy-nav-content {
    max-width: none;
}

h1,h2,h3,h4,h5,h6 {
    border-bottom: 1px solid #ccc;
}

.wy-table-responsive table td, .wy-table-responsive table th {
    white-space: normal;
}

colgroup {
    display: none;
}
```


ありがたいページ
---
[https://qiita.com/pashango2/items/d1b379b699af85b529ce](https://qiita.com/pashango2/items/d1b379b699af85b529ce)  
[http://kuttsun.blogspot.com/2016/11/sphinx-sphinxrtdtheme.html](http://kuttsun.blogspot.com/2016/11/sphinx-sphinxrtdtheme.html)


memo
---
調べていて気になったものを書き留めておく場所

- sphinxcontrib-blockdiag  
sphinxでブロック図、シーケンス図がかけるとのこと
