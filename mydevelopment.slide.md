### 最近のPHPWebアプリ開発環境

についての(個人的な)まとめ

[Kohki Makimoto](https://github.com/kohkimakimoto)

---

### 実務でやってること

---

### VirtualBox

* ローカル開発環境。
* XAMPつかっていいのは小学生まで。

---

### Chef

* サーバ設定を自動化。あるべき状態に構築してくれる。

* 自動化も利点だけど、ローカル開発環境と本番の設定を一元管理できるのが大きい。

* サーバ環境をポータブルにできる。

* 実は、敷居はすごく低い。
  * インストールはコマンド一発
  * RPM

---

### Composer

* モダンなPHPモジュール管理。
* インストール簡単。
```
# これだけ。
$ curl -sS https://getcomposer.org/installer | php
$ mv composer.phar /usr/local/bin/composer
```
* アプリケーションレイヤでモジュール管理。
* システムワイドを汚さないので安心。
* この手のモジュール管理は最近のLLではスタンダード。
  * PerlではCarton
  * RubyではBundler
  * Pythonはしらない。。。

---

### Packagist

* Composerのメインリポジトリ。
* https://packagist.org/
* 流行りのPHPモジュールはここで探そう。
* 玉石混淆でなんでもある。
* Githubと連携させて自分で作ったモジュールを登録しておくとさらに便利。

---

### PHPUnit

* テストフレームワーク。
* PHPテストのデファクト。
* テストしたらカバレッジレポート出すべし。どれだけシステムが「保護」されているか確認できる。
* テストのないコードはレガシーコードですよ。

---

### SeleniumIDE

* FireFoxのアドオン
* ブラウザ自動操作ツール。
* ブラウザ操作を記録してSeleniumのテストケースを作成できる。
* テスト実行ボタンを押すとFireFoxが自動でもりもり動いてテストしてくれる。
* ただし、テスト自動化を進めていくとサーバ側での初期化処理などが必要になるので、実際のテスト実行はSelenium Serverから行う。

---

### Selenium Server

* ブラウザ自動操作をサーバで行う。
* GUIがないサーバで動作させるためXvfb(仮想フレームバッファ)を併用する。
* PHPUnitと連係させてコマンド一発でテスト開始。
* カバレッジレポートをとる。

---

### DBマイグレーション

* MySQLのスキーマ定義、状態を管理する。
* ツールを自作。
  * http://kohkimakimoto.github.io/lib-migration/
* スキーマ変更を手動、生SQLでやっていいのは小学生まで。
```
# => こういう操作やんない
mysql> alter table xxx ...
```

---

### デプロイツール

* ツールを自作。
  * http://kohkimakimoto.github.io/altax/
* 並列SSHを実行。
* RubyのCapistrano的なやつ。
* リモートサーバへの定型作業をタスクにして管理。
* アプリのデプロイやマイグレーションをコマンド一発でできるようにする。

---

### 最近いじってみたものとか

実務とはあんまし関係なしに。

---

### Travis CI

* CI(継続的インテグレーション)サービス。
* https://travis-ci.org/
* GithubリポジトリにPushするとそれをフックしてテストを自動実行してくれる。
* CIはここで初体験。
* 便利やわ～。
* テスト書くモチベーションUP。

---

### COVERALLS

* Travisでテストした結果のカバレッジを表示してくれるサービス。
* https://coveralls.io/
* 便利やわ～。
* テスト書くモチベーションUP。

---

### 新しめのフレームワーク

* Silex
  * RubyのSinatraみたいなマイクロフレームワーク。
* Symfony2
  * Packagistもこれでできてる。
* 1世代前のフレームワーク(Symfony, CakePHP, ZendFramework, Codeigniter)と比較して、構造化、標準化が進んだ感じがする。

---

### 新しめのフレームワーク

* 名前空間を使ったモジュールの構造化。
* Composerによる標準的なパッケージ管理。
* 昔はこの辺りを各フレームワークが、独自の命名規約、ライブラリなどで管理していた。
* 他言語由来の新しめの機能も追従して組み込まれてきている。
* Assetic
  * Railsのアセットパイプライン的なもの。
  * lessやCoffeeScriptを使えるようになる。


---

### Ansible

* すこーし触ってみただけ。
* http://www.ansibleworks.com/
* 軽量chef的なもの。
* chefのcookbookにあたるplaybookはymlで記述する。
* だからpython製だけどpythonほとんど意識しない。
* CentOSならepelからyumでインストールできる。
* デプロイツールとして使おうか検討中。

---

### Webデザインまわり
* Bootstrap3
  * http://getbootstrap.com/
  * モバイルに強くなった。レスポンシブデザイン。
* Font Awesome
  * http://fortawesome.github.io/Font-Awesome/
  * アイコンをフォントで表現。
  * 画像いじらなくても、CSSでアイコンのサイズ、色が変えられる。

---

### おしまい。