mecab-ext-dics
====
mecabの辞書を拡張するための辞書データ置き場

## Requirements

    mecab


## Install Dependencies

    brew install mecab


## mecabの辞書を拡張する

[https://mecab.googlecode.com/svn/trunk/mecab/doc/dic.html]()を参考にしてる

### WikipediaとはてなキーワードのデータをMecabフォーマットにする

文字コードはEUC-JPで統一した。IPA辞書がEUC-JPなので


### MacOS10の場合(homebrew環境)
    % git clone https://github.com/ytanaka-/mecab-ext-dics.git
    % cd mecab-ext-dics
    % curl -O https://mecab.googlecode.com/files/mecab-ipadic-2.7.0-20070801.tar.gz
    % tar zxfv mecab-ipadic-2.7.0-20070801.tar.gz
    % cd mecab-ipadic-2.7.0-20070801
    % cp ../hatena_keyword.csv ../wikipedia_title.csv .
    % ./configure
    % /usr/local/Cellar/mecab/0.996/libexec/mecab/mecab-dict-index -f euc-jp -t utf8
    % make install

ユーザー辞書への追加の方が簡単みたいだが、システム辞書へ追加した方がパフォーマンスでるらしいので上記のような面倒な手順になってる

ようはmecab-ipa辞書をmakeするときに一緒に追加分を含めてしまうということらしい。

mecab-dict-indexのところは環境によってpathが異なると思うので注意。-tオプションはバイナリ辞書の文字コード指定で、ここをutf8にしないと形態素解析された結果取得時に文字化けする。


ちなみに[http://qiita.com/ysk_1031/items/7f0cfb7e9e4c4b9129c9]()のようなやり方もある。

brewでmecab-ipaをインストールすると、Makefileが消失？してしまうので、ソースを取得してる。


### (番外)costの算出
[http://mecab.googlecode.com/svn/trunk/mecab/doc/dic-detail.html](MeCab の辞書構造と汎用テキスト変換ツールとしての利用)に公式のユーザースタディがあるが、[http://tmp.blogdns.org/archives/2009/12/mecabwikipediah.html]()こちらのコスト算出式の方が良いらしいのでこちらを採用した