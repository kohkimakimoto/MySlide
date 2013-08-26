<h3>PHPWebアプリケーション<br/>開発環境</h3>

についての(個人的な)まとめ

[Kohki Makimoto](https://github.com/kohkimakimoto)

---

### 開発環境、ツール、サービス

---

### VirtualBox

* 仮想環境。
* ローカルマシンにLinuxサーバを立てて開発環境に。
* XAMPつかっていいのは小学生まで。

---

### Chef

* サーバ構築を自動化。

* サーバをあるべき状態に設定してくれる。

* 自動化も利点だけど、ローカル開発環境と本番の設定を一元管理できるのが大きい。

* サーバ環境をポータブルにできる。

* 実は導入の敷居はすごく低い。
  * インストールはコマンド一発
  * 組み込みRubyまで入っているRPMがある。

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
* 昨今のLLではスタンダードな構成管理の仕組み。
* 他言語で同様のもの。
  * Carton　(Perl)
  * Bundler (Ruby)

---

### Packagist

* Composerのメインリポジトリ。
* https://packagist.org/
* 必要なPHPモジュールはここで探す。
* 玉石混淆でなんでもある。
* Githubと連携させて自分で作ったモジュールを登録しておくと、いろんな場面で再利用が捗る。

---

### PHPUnit

* テストフレームワーク。
* PHPテストのデファクトスタンダード。
* テストしたらカバレッジレポートを出す。どれだけシステムが「保護」されているか確認できる。
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
* もちろんカバレッジレポートをとる。

---

### DBマイグレーション

* MySQLのスキーマ定義、状態を管理する。
* ツールを自作。
  * http://kohkimakimoto.github.io/lib-migration/
* スキーマ変更を手動、生SQLでやっていいのは小学生まで。
```
# => こういう操作を本番でやらない
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
* でも最近、[Ansible](http://www.ansibleworks.com/)のほうがいいんじゃないかと思い始めた。

---

### 最近いじってみたもの

実務とはあんまし関係なしに。

---

### Travis CI

* CI(継続的インテグレーション)サービス。
* https://travis-ci.org/
* GithubリポジトリにPushするとそれをフックしてテストを自動実行してくれる。
* CIは使ってみるとやはり便利。
* テスト書くモチベーションUP。

---

### COVERALLS

* Travisでテストした結果のカバレッジを表示してくれるサービス。
* https://coveralls.io/
* テスト書くモチベーションUP。

---

### 新しめのPHPフレームワーク

* Silex
* http://silex.sensiolabs.org/
* RubyのSinatraみたいなマイクロフレームワーク。
* やりたいことが増えてくるとSymfonyとかのほうがいい気がする。

---

### 新しめのPHPフレームワーク

* Symfony2
* Packagistもこれでできてる。
* バンドルで構造化された作りが、初見は複雑に感じるので、とっつきにくい気がする。
* DoctrineのアーキテクチャがActiveRecordからDataMapperに変更。
* 個人的にはActiveRecordのほうが好みなので、テンション下がった。

---

### 新しめのPHPフレームワーク

* ZnedFramework2
* 試してない。

---

### 新しめのPHPフレームワーク

* 1世代前のフレームワーク(Symfony, CakePHP, ZendFramework, Codeigniter)と比較して、構造化、標準化が進んだ感じがする。
* 名前空間を使ったモジュールの構造化。
* Composerによる標準的なパッケージ管理。
* 昔はこの辺りを各フレームワークが、独自の命名規約、ライブラリなどで管理していた。

---

### 新しめのPHPフレームワーク

* 他言語由来のモダンな機能を追従している。
* Composer
  * RubyのBunlderと同等。
* Assetic
  * Railsのアセットパイプライン。
  * lessやCoffeeScriptを使えるようになる。

---

### Ansible

* Pythonで書かれたサーバプロビジョニングツール。
* http://www.ansibleworks.com/
* 軽量なchef的なもの。
* chefのcookbookにあたるplaybookはymlで記述する。
* CentOSならepelからyumで一発インストールできる。
* デプロイツールとして使おうか検討中。

---

### Webデザインまわり

* Bootstrap3
* http://getbootstrap.com/
* モバイルへの表現に強くなった。
* レスポンシブデザイン。
* グリッドレイアウトの仕組みが2系と変わったので覚えなおさないといけない。

---

### Webデザインまわり

* Font Awesome
* http://fortawesome.github.io/Font-Awesome/
* アイコンをフォントで表現。
* 画像いじらなくても、CSSでアイコンのサイズ、色が変えられる。
* 最近のフラットデザインと親和性よし。

---

### おしまい。

