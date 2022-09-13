# 自作RDBMSやろうぜ!
## このサイトの目的
- RDBMS（いわゆるリレーショナルデータベース）というものはプログラミング言語の処理系や、OSなどと同様に、世の中で広く使われているソフトウェアであるにも関わらず、いざ自作してみようと思うと日本語で記述されたサイトで、必要な情報・情報源がまとまったサイトがないことに気づきました
- そこで、叩き台として、本サイト管理人および数名のコミッタで開発している自作RDBMSである [SamehadaDB](https://github.com/ryogrid/SamehadaDB) が軌道に乗るまでの経験をベースに、自作RDBMSに関する情報をある程度整理して書き記してみました
  - 各々の情報・情報源はあいかわらず多くが英語で記述されていますが、その点はご容赦下さい
- なお、本サイトは技術的な解説を提供するのではなく、適切と思われる情報・情報源をポイントするようなサイトとなることを想定しています
- GitHub Pagesで構築したWebページですので、Pull Requestなど送っていただければ可能な限り反映しますし、集合知的なやり方で良いものにしていければと考えています
  - 個人的なメモとして作成したコンテンツではないですし、管理人だけが情報発信する想定で作成したサイトでもないので、原型が残らないレベルでガンガン Pull Request 送ってもらってOKです
  - ただし、趣旨からズレるものはNGです

## ハードコース
- 英語スラスラ読めるし、とっかかりさえあれば自分でどうにかできるという方はこちら
- 以下のページに Database System について学ぶための情報源がリストされているので、適宜参照しながら進められると良いでしょう
  - [awesome-database-learning](https://github.com/pingcap/awesome-database-learning)
- 以下の書籍で丸っとDatabase Systemに関する基礎知識と実装まで押さえるというのもよいと思います
  - [ Edward Sciore 『Database Design and Implementation (Second Edition) 』](https://link.springer.com/book/10.1007/978-3-030-33836-7)
- [awesome-dbdev](https://github.com/huachaohuang/awesome-dbdev)に基礎的な内容と論文がずらずら並んでいる
  - DB自作するなら知っておきたい情報まとめ（ただし英語）
  - 基礎的な内容とおすすめ論文の列挙って感じでDBの研究の外観を知るには良いけど、普通のRDBMSを普通に作るための情報っていう観点だと微妙に思います
  - 論文pdfが全部リポジトリ内に入ってる

## 段階的に進んでいこうコース（= おおむね管理人が歩んだ道）
- いきなり英語とか辛いので日本語なサイトや書籍等で基本を押さえてから段階的に進んでいきます
- これがベストと言うつもりはないので、こういう世界線もあるよ、という方はよろしくサイト内リンクで飛べるような形でまとめて Pull Request を送っていただけるとありがたやです

### 自作RDBMSしてる方々のブログ記事などを読んで雰囲気を感じよう
Database Systemのアーキテクチャの概要などについて解説されている記事も含め、入門者にはありがたい情報がたくさんです
- [Kotlinで自作DBMS（keyem4251氏のZenn記事）](https://zenn.dev/keyem4251/articles/my-kotlin-dbms)
- [自作DBを始めたい人におすすめの本 - salachike:blog](https://tarovel4842.hatenablog.com/entry/2021/12/20/084413)
- [DBMSをGoで実装してみた - Sansan Builders Blog](https://buildersbox.corp-sansan.com/entry/2019/10/24/110000)
- [自作DBMS Advent Calendar 2020 - Adventar](https://adventar.org/calendars/5548)
- [Java8でRDBMS作ったよ（きしだなおき氏の スライド資料 at slideshare）](https://www.slideshare.net/nowokay/with-java8)
  - オンメモリでの実装（ディスクへの永続化を行わない）かつ、シングルスレッド、型無しといった形での割り切った実装
  - [ソースコード](https://github.com/kishida/sqlparser)
- [PostgreSQL 互換の DBMS を自作してみた - goropikariの備忘録](https://goropikari.hatenablog.com/entry/build_own_dbms)
  - こちらもオンメモリでの実装のようです
  - PostgreSQL client から接続できるようにした（そこの点で互換性を持たせた）そうで、フロント回りのお話は特に興味深いです

### 日本語の書籍で（Relational) Database System の基本について押さえよう
- [北川 博之著 『データベースシステム 改訂2版』](https://www.amazon.co.jp/%E3%83%87%E3%83%BC%E3%82%BF%E3%83%99%E3%83%BC%E3%82%B9%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0-%E6%94%B9%E8%A8%822%E7%89%88-%E5%8C%97%E5%B7%9D%E5%8D%9A%E4%B9%8B-ebook/dp/B08BNXFRL3/)
  - 大学の情報系の講義などで用いられる教科書といった感じの書籍です
  - 実装寄りかと言えばそうでもないですが、基本を押さえておけば英語の情報にあたった時もなんとかなります
  - なお、管理人は後述の日本語な情報源の存在を知ったタイミングの関係から、本書のうちの、実装段階でひとまず必要そうな所に一通り目を通したところで次のステップに進みました
- [Alex Petrov 著、小林隆浩 監訳、成田昇司 訳『詳説 データベース -- ストレージエンジンと分散データシステムの仕組み』](https://www.oreilly.co.jp/books/9784873119540/)
  - タイトルからも分かるように全体としては分散データベースや分散ストレージエンジンにフォーカスした書籍です
  - しかしながら、全体の約半分を占める第I部は "分散していないデータベース" でもおおむね共通の内容に見えるので、分散DBMSにトライしようという方でなくても読んでおいて損はないと思われます
  - オライリーのサイトから電子版（pdfフォーマット）が購入可能です
- [KOBA789著 『WEB+DB PRESS Vol. 122 "特集3 作って学ぶ RDBMS のしくみ"』](https://www.amazon.co.jp/WEB-DB-PRESS-Vol-122-PRESS%E7%B7%A8%E9%9B%86%E9%83%A8-ebook/dp/B092Q8SKDB)
  - 特集のタイトルの通り実装を追いながらRDBMSについて解説しています
  - rellyというシンプルなRDBMS実装について解説しており、コードはGitHubにあります
    - [KOBA789/relly](https://github.com/KOBA789/relly)
  - 日本語で書かれているという点で、大変貴重な記事なのですが、実装がRustなため、Rust経験者でない場合、コードの読解は少し苦労するかもしれません 
  - WEB+DB PRESSは上のリンクから vol.122 だけのKindle版が購入できます
- 管理人が自作RDBMSするにあたっていろいろとアドバイスをいただいている方の一人が [kumagi](https://github.com/kumagi)氏 ですが、以下のようなものを書いてたりするので、読んでおくと、後でああ、あの話かーという感じで役に立つかもしれません
  - [一人トランザクション技術 Advent Calendar 2016 - Qiita](https://qiita.com/advent-calendar/2016/transaction)
  - 次のセクションのオープンコースウェアな講義で良く分からなかったときに参照する、というのでもよい気はします
- [星野喬著 『データベースシステム自作入門』](https://github.com/starpos/develop-transaction-system/releases/)
  - RDBMSではなくDBMSに関してのものですが、実装寄りの貴重な日本語の書籍（GitHub上でpdfで公開されている）です
  - トランザクションというものの解説に重点を置いており、入門というタイトルではありますが深いところまで踏み込んでいる感じもあります（グラデーションはあります）
  - これまでに挙げた情報源からすると相対的には最初に読む情報源ではないかもしれません
  - こちらも、次のセクションのオープンコースウェアな講義で良く分からなかったときに参照する、一通り理解したあとで読んでみるというのでもよいかもしれません


### オープンコースウェア（※）を活用して本格的な RDBMS の実装について学ぼう
- ※：大学や大学院などの高等教育機関で正規に提供された講義とその関連情報を、インターネットを通じて無償で公開する活動 (Wikipediaより）
- ここについては以下のGitHubリポジトリにまとめておいたので、ひとまずそちらをご参照下さい
  - [ryogrid/CMU_lecture_DATABASE_SYSTEMS_materials](https://github.com/ryogrid/CMU_lecture_DATABASE_SYSTEMS_materials)
- 管理人および数名のコミッタは、前出ですが、自作RDBMSとして [SamehadaDB](https://github.com/ryogrid/SamehadaDB) というものをちまちまと開発していますが、これは現状、上記のCMUの講義で扱っている教育用RDBMS実装 BusTubを C++ から Go言語にポーティングすることが主な作業となっています
  - brunocalza氏が先だって [brunocalza/go-bustub](https://github.com/brunocalza/go-bustub) というプロジェクトを進めていたため、全てのポーティングを管理人らが行ったわけではありません
  - なお、brunocalza氏は、時間が取れなくなったそうで、go-bustub プロジェクトは管理人が fork するしばらく前から更新されておらず、今後更新できる見込みも無いとのこと
    - 現状、やっている作業がgo-bustubのやろうとしていたことに類似しているだけであって、プロジェクトを引き継いだわけではありません
  - 本家BusTubは講義の課題として実装の穴埋めをさせるように作られているため、歯抜けになっていますが、brunocalza氏及び管理人らはそれらの部分を埋める形でポーティングを行ったため、全てではないですが一応、一通り実装が行われています
  - 従って、手前味噌ですが、BusTub相当の機能までであれば、SamehadaDBのコードベースを参考にしていただくのも良いのではないかと思います
    - 更新しきれていない部分も多いですが、[なんちゃってクラスダイアグラム](https://user-images.githubusercontent.com/24614/145060831-1d3ec3a9-267d-4295-96e7-a2bbe824cf9c.png) も go-bustub読解の時点で作成したので、ご活用ください
  - (Go言語にポーティングしているのは写経的な意味と、個人的にC++のまま拡張していくの辛いな・・・と思ったためです)

### アドバンスドなところも実装していこう
- BusTubには残念ながら planner/optimizer に相当するところの実装やフロントエンドの実装がありません
  - サーバとして動作させたいのであれば、DBコネクタ（DBドライバ）や REST API 等の、NW越しにクエリを投げて結果取得できるインタフェースも必要ですが、フロントがないのでこれも当然ありません
- [awesome-database-learning](https://github.com/pingcap/awesome-database-learning) を参照して気合で実装するのも良いかもしれませんが、なかなか大変らしいです（管理人らもまだそこまで達していない）
- というわけで、ハードコースの方で既出、かつ英語ではありますが、以下の書籍を参考に実装するとよいらしいです
  - [ Edward Sciore 『Database Design and Implementation (Second Edition) 』](https://link.springer.com/book/10.1007/978-3-030-33836-7)
  - 通称、SimpleDB本とも呼ばれたりするらしく、SimpleDBというRDBMS実装（Java）をフロントエンドからストレージエンジンのところまで丸っと実装しています
  - SimpleDBのソースコードは著者のWebページから入手可能です
    - [The SimpleDB Database System](http://www.cs.bc.edu/~sciore/simpledb/)
  - 同書を読みながらSimpleDBをC++で実装したという方がいて、GitHubにコードがあったりもします
    - [yutaroyamanaka/SimpleDB](https://github.com/yutaroyamanaka/SimpleDB)  
    - なお、本家SimpleDBの全てをカバーしているわけではないようです
  - Rustで実装してみた方もいらっしゃるようです
    - [cutsea110/simpledb](https://github.com/cutsea110/simpledb)
    - [cliツールで操作しているデモ動画](https://t.co/Zib8V880Yn)
      - NW通信越しに動作している模様
      - プロトコルは [Cap’n Proto](https://capnproto.org/) を用いた[RPC](https://capnproto.org/cxxrpc.html) による独自のもののようです
        - 使用しているクレート: [capnp-rpc-rust](https://crates.io/crates/capnp-rpc/)
  - Golangでの実装もありました
    - [goropikari/simpledbgo](https://github.com/goropikari/simpledbgo)
    - PostgreSQLの通信プロトコルを実装していて、psqlコマンドで接続できるそう

### 戦いはさらに続く
- ここまでに挙げたものは基本的なところを、比較的一般的かつ、さほど難度の高くない手法で実装している認識ですが、RDBMSをより良いものにしようと思えば、やれることは際限なくあります
- 例えば、logging/recoveryにおける snapshot で ARIES などの fuzzy snapshot を実装してみるというのもよいでしょう
- 実用を意識した場合、アクセス認証なども必要でしょうが、どのような方式に対応するか、認証データの保持周りの設計はどうすべきか、など考えてみると奥が深そうです
- そのあたりは [awesome-database-learning](https://github.com/pingcap/awesome-database-learning) など参照して各自追求していきましょう（一緒に）
- あと、自作 (R)DBMSの世界で定番？なコンテンツとして通称redbook（赤本）と呼ばれる 『Readings in Database Systems』というものがありまして、その内容は押さえておくとよいのだろうと思います
  - [Peter Bailis, Joseph M. Hellerstein, Michael Stonebraker, editors『Readings in Database Systems, 5th Edition』](http://www.redbook.io/)

### 余談
- インデックスの実装にB+木が広く利用されているということで、ここまでに挙げた書籍でも採用されていることが多いですが、レコードの削除・更新および並行トランザクション実行における排他制御までサポートしようとすると途端に難易度が跳ね上がるそうです
  - それもあり、SamehadaDBでは 木構造ベースなインデックスの実装は後回しとする判断をしていたりします（2022/05/10 時点）
- 従って、B+木でインデックスを実装してみるというのは学習という観点では良いことだと考えていますが、実用に耐えうるとは言わないまでも、基本的なSQLが通り、かつ、あきらかな手抜き箇所がないものに仕上げようと思った際は地獄が待っているかもしれない、ということは念頭に置いておくとよいかもしれません
  - 排他制御に関してはテーブル単位で丸っとロックするといった対処も可能ですが、スループットは（少なくとも、同一テーブルのおおむね同一のレコード群に触る参照系と更新系の混ざった並列トランザクション実行では、）落ちます
- ちなみに、B木（とその亜種）ベースのインデックスないしその手のものの設計・実装には様々なバリエーションがあるそうで、それらの解説だけで専門書が1冊存在するくらいです
  - [Goetz Graefe『Modern B-Tree Techniques (Foundations and Trends(r) in Databases)』](https://www.amazon.co.jp/Modern-B-Tree-Techniques-Foundations-Databases/dp/1601984820)
  - うわぁ、いいお値段するし絶版本かぁと思ったあなた。元々、論文が書籍化されたものであり、元論文はpdfの形で公開されています
    - [元論文](https://w6113.github.io/files/papers/btreesurvey-graefe.pdf)
    - Graefe氏への respect を忘れないようにしつつ拝読しましょう

## その他の自作RDBMSに役立ちそうな情報源
- 何か載せたいものがあれば Pull Request お願いします
- 下の"MITのDATABASE SYSTEMS"のような感じで並べていければと思います
  - 必要であれば、<https://github.com/dbms-jisaku> の中にmdファイルなりhtmlファイルなり置いてもらって構いません
- [UC berkeleyの Introduction to Database Systems](https://cs186berkeley.net/)
  - 上述なCMUの講義 [DATABSE SYSTEMS](https://15445.courses.cs.cmu.edu/fall2021/) における[BusTub](https://github.com/cmu-db/bustub)と同じような感じで [rookiedb](https://cs186.gitbook.io/project/)というRDBMSの実装を穴埋め形式で課題として学生に課している講義です
    - コードはこちら: [berkeley-cs186/sp22-rookiedb](https://github.com/berkeley-cs186/sp22-rookiedb)
      - BusTubではコードや課題の内容についての解説は少なくともテキストの形では存在しませんが、rookiedbについてはそのあたりについてもいくらか解説があり良い感じです。また、BusTubでカバーしていない範囲についても rookiedb では扱っています
    - なお、rookiedbの実装はSimpleDBなどと同様、Javaです
      - RDBMS開発のようなシステムプログラミングの用途においてJavaが適した技術選定かと言えば違うのではないかと管理人的には思いますが、黒魔術的な要素が少なく、比較的クセの少ないOOP言語という点で教育用途には向いている、ということなのかと思っています
    - [講義動画](https://www.youtube.com/user/CS186Berkeley/playlists)
      - Youtube動画なので、自動翻訳で字幕を出し、それでもついていくのが難しければ再生速度を遅くするというテクが使えます
- [MITのDATABASE SYSTEMS](https://ocw.mit.edu/courses/6-830-database-systems-fall-2010/)
  - MITのデータベースをスクラッチから作ってみようという講義
  - 2010年のもので時代を感じるが講義資料は公開されているし[実装](https://github.com/awelm/simpledb)もあるように見える
  - Optimizerに関してもSelingerだけどちゃんと説明と実装があって良さそう

## Database System に関連する情報源
- 上のセクションと基本同じ感じですが、自作RDBMSというところからは離れてるかもーというものもOKとします
- [DBSJ最強データベース講義](https://www.youtube.com/channel/UCaOkRhbjsqviiDQdKn-p0HA/videos)
  - 日本のデータベースシステム研究者の方々がおおむね自身の研究分野を講義風に整理して説明している動画が公開されています
  - どういう位置づけとして捉えるかは微妙ですが、Database Systemの世界も研究分野としては様々な方向性があるのだなー、というのを感じるには良いコンテンツのように思います
- [Database of Databases](https://dbdb.io/)
  - 名前はわざとひねりをつけてこうしてあるのだろうと思いますが、要は Database System の Database（データ・情報の方）です
  - "オープンコースウェアを活用して本格的な RDBMS の実装について学ぼう" のセクションで紹介した講義の公開なども行っている [Carnegie Mellon Database Group](https://db.cs.cmu.edu/) が運営しているサイトのようです
  - 誰しも知るプロダクトから、hobbyで開発されたようなものまで幅広く情報がインデックスされています
  - 各々がどのような設計をとっているか、機能をサポートしているかといった情報も（入力されていれば）あるようなので、何かの用事で比較が必要な場合は便利そうです
  - 自作(R)DBMS勢であればただダラダラ眺めても面白いかもしれません

## 交流の場（Slack）
- 同好の士で交流を持てればと思い、『自作DBMS Slack』というものを作ってみました
- 自作（R）DBMSやってる方、やってみたいと考えている方、いつかやれたらいいなあと思っている方、DBMSについて内部の仕組みまで知りたいと考えている方、などなどご興味があればご参加ください
- ROM専も可です b
- [招待リンク](https://join.slack.com/t/jisaku-dbms/shared_invite/zt-1bgotsi4g-~NRndNwaEjvEn98M5WjzTQ)

## ライセンス
- 本サイトのコンテンツには [表示 4.0 国際 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.ja) のライセンスが適用されます
- 詳細はリポジトリ内のLICENCEファイルをご参照下さい
- faviconについて
  - [vaadin](https://icon-icons.com/ja/users/QLAfZ5Txo40x6pWfXduTy/icon-sets/)により作成されたアイコンであり [表示 4.0 国際 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.ja) のライセンスの下で提供されているものです

