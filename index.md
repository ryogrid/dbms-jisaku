# 自作RDBMSやろうぜ!
## このサイトの目的
- RDBMS（いわゆるリレーショナルデータベース）というものはプログラミング言語の処理系や、OSなどと同様に、世の中で広く使われているソフトウェアであるにも関わらず、自作してみようと思うと日本語で記述されたサイトで、必要な情報・情報源がまとまったサイトがないことに気づきました
- そこで、叩き台として、本サイト管理人および数名のコミッタで開発している自作RDBMSである [SamehadaDB](https://github.com/ryogrid/SamehadaDB) が軌道に乗るまでの経験をベースに、自作RDBMSに関する情報をある程度分かりやすくまとめてみました
  - 各々の情報・情報源はあいかわらず多くが英語で記述されていますが、その点はご容赦下さい
- なお、本サイトは技術的な解説を提供するのではなく、適切と思われる情報・情報源をポイントするようなサイトとなることを想定しています
- GitHub Pagesで構築したWebページですので、Pull Requestなど送っていただければ可能な限り反映しますし、集合知的なやり方で良いものにしていければと考えています
  - 個人的なメモとして作成したコンテンツではないので、原型が残らないレベルでガンガンPR送ってもらってOKです
  - ただし、趣旨からズレるものはNGです

## ハードコース
- 英語スラスラ読めるし、とっかかりさえあれば自分でどうにかできるという方はこちら
- 以下のページに Database System について学ぶための情報源がリストされているので、適宜参照しながら進められると良いでしょう
  - [awesome-database-learning](https://github.com/pingcap/awesome-database-learning)
- 以下の書籍で丸っとDatabase Systemに関する基礎知識と実装まで抑えるというのもよいと思います
  - [ Edward Sciore 『Database Design and Implementation (Second Edition) 』](https://link.springer.com/book/10.1007/978-3-030-33836-7)

## 段階的に進んでいこうコース（= おおむね管理人が歩んだ道）
- いきなり英語とか辛いので日本語の書籍などで基本を押さえてから段階的に進んでいきます
- これがベストと言うつもりはないので、こういう世界線もあるよ、という方はよろしくサイト内リンクで飛べるような形でまとめてPR送っていただければ幸い

### 日本語の書籍でデータベースシステムの基本について押さえよう
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

### オープンコースウェアで本格的なデータベースシステムの実装について学ぼう
- ここについては以下のGitHubリポジトリにまとめておいたので、ひとまずそちらをご参照下さい
  - [ryogrid/CMU_lecture_DATABASE_SYSTEMS_materials](https://github.com/ryogrid/CMU_lecture_DATABASE_SYSTEMS_materials)
- 管理人および数名のコミッタは、前出ですが、自作RDBMSとして [SamehadaDB](https://github.com/ryogrid/SamehadaDB) というものをちまちまと開発していますが、これは現状、上記のCMUの講義で扱っている教育用RDBMS実装 BusTubを C++ から Go言語にポーティングすることが主な作業となっています
  - brunocalza氏が先だって [brunocalza/go-bustub](https://github.com/brunocalza/go-bustub) というプロジェクトを進めていたため、全てのポーティングを管理人らが行ったわけではありません
  - なお、brunocalza氏は、時間が取れなくなったそうで、go-bustub プロジェクトは管理人が fork するしばらく前から更新されておらず、今後更新できる見込みも無いとのこと
    - 現状、やっている作業がgo-bustubのやろうとしていたことに類似しているだけであって、プロジェクトを引き継いだわけではありません
  - 本家BusTubは講義の課題として実装の穴埋めをさせるように作られているため、歯抜けになっていますが、brunocalza氏及び管理人らはそれらの部分を埋める形でポーティングを行ったため、全てではないですが一応、一通り実装が行われています
  - 従って、手前味噌ですが、BusTub相当の機能までであれば、SamehadaDBのコードベースを参考にしていただくのも良いのではないかと思います
    - 更新しきれていない部分も多いですが、[なんちゃってクラスダイアグラム](https://github.com/ryogrid/SamehadaDB/wiki/class_diagram_of_samehadaDB) も go-bustub読解の時点で作成したので、ご活用ください
  - (Go言語にポーティングしているのは写経的な意味と、個人的にC++のまま拡張していくの辛いな・・・と思ったためです)

### アドバンスドなところも実装していこう
- BusTubには残念ながら planner/optimizer に相当するところの実装やフロントエンドの実装がありません
- [awesome-database-learning](https://github.com/pingcap/awesome-database-learning) を参照して気合で実装するのも良いかもしれませんが、なかなか大変らしいです（管理人らもまだそこまで達していない）
- というわけで、英語ではありますが以下の書籍を参考に実装するとよいらしいです
  - [ Edward Sciore 『Database Design and Implementation (Second Edition) 』](https://link.springer.com/book/10.1007/978-3-030-33836-7)
  - 通称、SimpleDB本とも呼ばれたりするらしく、SimpleDBというRDBMS実装（Java）をフロントエンドからストレージエンジンのところまで丸っと実装しています
  - SimpleDBのソースコードは著者のWebページから入手可能です
    - [The SimpleDB Database System](http://www.cs.bc.edu/~sciore/simpledb/)
  - 同書を読みながらSimpleDBをC++で実装したという方がいて、GitHubにコードがあったりもします
    - [yutaroyamanaka/SimpleDB](https://github.com/yutaroyamanaka/SimpleDB)  
    - なお、本家SimpleDBの全てをカバーしているわけではないようです

### 戦いはさらに続く
- ここまでに挙げたものは基本的なところを、比較的一般的かつ、さほど難度の高くない手法で実装している認識ですが、RDBMSをより良いものにしようと思えば、やれることは際限なくあります
- 例えば、logging/recoveryにおけるsnapshotにARIESなどを採用するというのもよいでしょう
- そのあたりは [awesome-database-learning](https://github.com/pingcap/awesome-database-learning) など参照して各自追求していきましょう（一緒に）
- あと、自作 (R)DBMSの世界で定番？なコンテンツとして通称redbook（赤本）と呼ばれる 『Readings in Database Systems』というものがありまして、その内容は押さえておくとよいのだろうと思います
  - [Peter Bailis, Joseph M. Hellerstein, Michael Stonebraker, editors『Readings in Database Systems, 5th Edition』](https://www.redbook.io/)

### 余談
- インデックスの実装にB+木が広く利用されているということで、ここまでに挙げた書籍でも採用されていることが多いですが、レコードの削除・更新および並行トランザクション実行における排他制御までサポートしようとすると途端に難易度が跳ね上がるそうです
  - それもあり、SamehadaDBでは 木構造ベースなインデックスの実装は後回しとする判断をしていたりします（2022/05/10 時点）
- 従って、B+木でインデックスを実装してみるというのは学習という観点では良いことだと考えていますが、実用に耐えうるとは言わないまでも、基本的なSQLが通るものに仕上げようと思った際には地獄が待っているかもしれない、ということは念頭に置いておくとよいかもしれません
  - 排他制御に関してはテーブル単位で丸っとロックするといった対処も可能ですが、パフォーマンスは当然落ちます
- ちなみに、B木（とその亜種）ベースのインデックスないしその手のものの設計・実装には様々なバリエーションがあるそうで、それだけで分厚い専門書が1冊存在します
  - [Goetz Graefe『Modern B-Tree Techniques (Foundations and Trends(r) in Databases)』](https://www.amazon.co.jp/Modern-B-Tree-Techniques-Foundations-Databases/dp/1601984820)
  - うわぁ、いいお値段するし絶版本かぁと思ったあなた。元々、論文が書籍化されたものであり、元論文はpdfの形で公開されています
    - [元論文](https://w6113.github.io/files/papers/btreesurvey-graefe.pdf)
    - Graefe氏への respect を忘れないようにしつつ拝読しましょう

## その他の自作RDBMSに関連するトピック
- 何か載せたいものがあれば Pull Requestお願いします
- 下の"ほげほげ"のような感じで並べていければと思います
  - 必要であれば、<https://github.com/dbms-jisaku> の中にmdファイルなりhtmlファイルなり置いてもらって構いません
- [ほげほげ](https://ryogrid.github.io/dbms-jisaku)

## データベースシステムに関連するトピック
- 上のセクションと基本同じ感じですが、自作RDBMSというところからは離れたトピックもOKとします
- [DBSJ最強データベース講義](https://www.youtube.com/channel/UCaOkRhbjsqviiDQdKn-p0HA/videos)
  - 日本のアカデミアのデータベース研究者の方々がおおむね自身の研究分野を講義風に整理して説明している動画が公開されています
  - どういう位置づけとして捉えるかは微妙ですが、データベースシステムの世界も研究分野としては様々な方向性があるのだなー、というのを感じるには良いコンテンツのように思います

## ライセンス
- 本サイトのコンテンツには [表示 4.0 国際 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.ja) のライセンスが適用されます
- 詳細はリポジトリ内のLICENCEファイルをご参照下さい
- faviconについて
  - [vaadin](https://icon-icons.com/ja/users/QLAfZ5Txo40x6pWfXduTy/icon-sets/)により作成されたアイコンであり [表示 4.0 国際 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.ja) のライセンスの下で提供されているものです

