# このソフトウェアについて

GitHubアップローダにサイトのContributions自動バックアップ機能を追加した。(更新頻度1日1回のみに改良)

* [GitHub.Uploader.AddFunction.Contributions.201705141424](https://github.com/ytyaru/GitHub.Uploader.AddFunction.Contributions.201705141424)の変異版

# これまでの問題

[GitHub.Uploader.AddFunction.Contributions.201705141424](https://github.com/ytyaru/GitHub.Uploader.AddFunction.Contributions.201705141424)には以下の問題が合った。

* 起動後にアップローダでコミット等したContributionsにおいてはバックアップされない。それは次回の起動時にならないと取り込まれない。
* 起動時間が遅くなる。アカウント6件で7〜8秒間の遅延発生

[GitHub.Uploader.AddFunction.Contributions.SingleUser.201705141610](https://github.com/ytyaru/GitHub.Uploader.AddFunction.Contributions.SingleUser.201705141610)でContributions自動バックアップ対象を指定ユーザのみに限定した。起動時間の遅延を軽減したと思ったが、たいして変わっていない気がする。

[GitHub.Uploader.AddFunction.Contributions.Async.201705141627](https://github.com/ytyaru/GitHub.Uploader.AddFunction.Contributions.Async.201705141627)で非同期にした。一定の効果はあったが以下の問題が。

* `async`を使っているためPython3.5以降でないと実行できなくなってしまった
* 指定ユーザのみのときは7〜8秒でなく3秒くらいになったが、全ユーザの時は8〜9秒になった。

# 今回

1日1回のみ更新されるようになった。更新する必要がないときに更新処理をしなくなった。遅延する頻度が減った。今回はトレードオフのない改善と思うが、コードが汚くなった。`./database/src/contributions/Main.py`。

しかし1回目は遅延することに変わりない。

## 動作確認

* 全ユーザDB未存在
    * ファイルの新規作成を確認した(12秒間かかった)
* 全ユーザDB最新
    * 待機時間ほぼなし
* 1ユーザの最新数日分を削除してそのユーザだけ更新処理が走ったのを確認
    * `************************{username}`

# 開発環境

* Linux Mint 17.3 MATE 32bit
* [Python 3.4.3](https://www.python.org/downloads/release/python-343/)
* [SQLite](https://www.sqlite.org/) 3.8.2

## WebService

* [GitHub](https://github.com/)
    * [アカウント](https://github.com/join?source=header-home)
    * [AccessToken](https://github.com/settings/tokens)
    * [Two-Factor認証](https://github.com/settings/two_factor_authentication/intro)
    * [API v3](https://developer.github.com/v3/)

# ライセンス

このソフトウェアはCC0ライセンスである。

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)

Library|License|Copyright
-------|-------|---------
[requests](http://requests-docs-ja.readthedocs.io/en/latest/)|[Apache-2.0](https://opensource.org/licenses/Apache-2.0)|[Copyright 2012 Kenneth Reitz](http://requests-docs-ja.readthedocs.io/en/latest/user/intro/#requests)
[dataset](https://dataset.readthedocs.io/en/latest/)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2013, Open Knowledge Foundation, Friedrich Lindenberg, Gregor Aisch](https://github.com/pudo/dataset/blob/master/LICENSE.txt)
[bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)|[MIT](https://opensource.org/licenses/MIT)|[Copyright © 1996-2011 Leonard Richardson](https://pypi.python.org/pypi/beautifulsoup4),[参考](http://tdoc.info/beautifulsoup/)
[pytz](https://github.com/newvem/pytz)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2003-2005 Stuart Bishop <stuart@stuartbishop.net>](https://github.com/newvem/pytz/blob/master/LICENSE.txt)
[furl](https://github.com/gruns/furl)|[Unlicense](http://unlicense.org/)|[gruns/furl](https://github.com/gruns/furl/blob/master/LICENSE.md)
[PyYAML](https://github.com/yaml/pyyaml)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2006 Kirill Simonov](https://github.com/yaml/pyyaml/blob/master/LICENSE)

