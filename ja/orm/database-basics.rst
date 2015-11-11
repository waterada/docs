<<<<<<< Updated upstream
データベースの基本
###################

CakePHPデータベースアクセス層は、リレーショナルデータベースを扱うほとんどの面を
抽象化して、サーバコネクションの保持、クエリーの生成、SQLインジェクションの防止、
スキーマチェックと変更、デバッグとデータベースに送信したクエリーのプロファイリング
などの支援を提供します。

クイック ツアー
=================

この章で説明する機能は、下位レベルのデータベースアクセスAPIでできることを説明します。
もし ORM についてもっと詳細に知りたい場合は、 :doc:`クエリービルダー</orm/query-builder>` 
の項か、 :doc:`/orm/table-objects` の項を参照してください。

データベースコネクションを作る一番簡単な方法は、 ``DSN`` 文字列を使います。::
=======
..
    Database Basics

データベースの基本
#################

..
    The CakePHP database access layer abstracts and provides help with most aspects
    of dealing with relational databases such as, keeping connections to the server,
    building queries, preventing SQL injections, inspecting and altering schemas,
    and with debugging and profiling queries sent to the database.

CakePHP のデータベースアクセス層の抽象クラスとプロバイド★は　リレーショナルデータベースが持つ多くの特徴を役に立つ★
たとえば、サーバとのコネクションを維持する、クエリを構築する、SQLインジェクションを防ぐ、スキーマを検査し、アラートを出す、
デバッグモードの場合にデータベースに送信されたクエリをプロファイリングするなどです。

..
    Quick Tour

クイック・ツアー
===============

..
    The functions described in this chapter illustrate what is possible to do with
    the lower-level database access API. If instead you want to learn more about the
    complete ORM, you can read the :doc:`/orm/query-builder` and
    :doc:`/orm/table-objects` sections.

この章で語られる諸機能★はローレベルのDBアクセスAPIを用いてとりあえず何ができるのかを説明します。
もし完全な ORM についてより詳しく知りたいのなら  :doc:`/orm/query-builder` と :doc:`/orm/table-objects` の章を読むと良いでしょう。

..
    The easiest way to create a database connection is using a ``DSN`` string::

DBコネクションを作成する最も簡単な方法は ``DSN`` 文字列を使うことです::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;

    $dsn = 'mysql://root:password@localhost/my_database';
    ConnectionManager::config('default', ['url' => $dsn]);

<<<<<<< Updated upstream
作成したら、コネクションオブジェクトにアクセスして使えるようになります。::

    $connection = ConnectionManager::get('default');

サポートしているデータベース
------------------------------

CakePHP は下記のリレーショナルデータベースをサポートしています。:
=======
..
    Once created, you can access the connection object to start using it::

一旦作成すれば、その文字列を使ってコネクションオブジェクトにアクセスすることができます::

    $connection = ConnectionManager::get('default');


..
    Supported Databases

サポート対象のデータベース
-------------------------
..
    CakePHP supports the following relational database servers:

CakePHP は次のリレーショナル・データベース・サーバをサポートします:
>>>>>>> Stashed changes

* MySQL 5.1+
* SQLite 3
* PostgreSQL 8+
* SQLServer 2008+

<<<<<<< Updated upstream
上記のデータベースそれぞれについて、適切な PDO拡張がインストールされている必要が
あります。
プロシージャー型APIはサポートされていません。

.. _running-select-statements:

Select 文の実行
-------------------------

生の SQL クエリーを実行するのは非常に簡単です。::
=======
..
    You will need the correct PDO extension installed for each of the above database
    drivers. Procedural API's are not supported.

上記のDBドライバごとに正しい PDO エクステンションをインストールしておく必要があります。
手続き的な API はサポートされません。

..
    Running Select Statements

SELECT文を走らせる
-------------------------

..
    Running raw SQL queries is a breeze::

素の SQL クエリを走らせるのは実に簡単です::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;

    $connection = ConnectionManager::get('default');
    $results = $connection->execute('SELECT * FROM articles')->fetchAll('assoc');

<<<<<<< Updated upstream
パラメータを追加するには、プリペアドステートメントを使います。::
=======
..
    You can use prepared statements to insert parameters::

プリペアド・ステートメントを使ってパラメータを差し込むことができます::
>>>>>>> Stashed changes

    $results = $connection
        ->execute('SELECT * FROM articles WHERE id = :id', ['id' => 1])
        ->fetchAll('assoc');

<<<<<<< Updated upstream
これは引数として複合データ型を使用することも可能です::
=======
..
    It is also possible to use complex data types as arguments::

複雑なデータタイプを引数として使うこともできます::
>>>>>>> Stashed changes

    $results = $connection
        ->execute(
            'SELECT * FROM articles WHERE created >= :created',
            ['created' => DateTime('1 day ago')],
            ['created' => 'datetime']
        )
        ->fetchAll('assoc');

<<<<<<< Updated upstream
SQL文を手で書く代わりに、クエリービルダーを使うこともできます。::
=======
..
    Instead of writing the SQL manually, you can use the query builder::

SQL を手動で書くのではなく、クエリビルダを使うことができます::
>>>>>>> Stashed changes

    $results = $connection
        ->newQuery()
        ->select('*')
        ->from('articles')
        ->where(['created >' => new DateTime('1 day ago'), ['created' => 'datetime']])
        ->order(['title' => 'DESC'])
        ->execute()
        ->fetchAll('assoc');

<<<<<<< Updated upstream
Insert 文の実行
-------------------------

データベースに行を追加するのは、通常は数行の話しです。::
=======
..
    Running Insert Statements

INSERT文を走らせる
-------------------------

..
    Inserting rows in the database is usually a matter of a couple lines::

データベースの行をINSERTすることは通常２～３行でできます::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;

    $connection = ConnectionManager::get('default');
    $connection->insert('articles', [
        'title' => 'A New Article',
        'created' => new DateTime('now')
    ], ['created' => 'datetime']);

<<<<<<< Updated upstream
Update 文の実行
-------------------------

データベースの行の更新も同様に直感的に可能で、下記の例では article の **id** が 10 の
データを更新しています。::
=======
..
    Running Update Statements

UPDATE文を走らせる
-------------------------

..
    Updating rows in the database is equally intuitive, the following example will
    update the article with **id** 10::

データベースの行をUPDATEすることは同様に直感的で、下記の例では **id** 10 の article をUPDATEします::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;
    $connection = ConnectionManager::get('default');
    $connection->update('articles', ['title' => 'New title'], ['id' => 10]);

<<<<<<< Updated upstream
Delete 文の実行
-------------------------

同様に ``delete()`` メソッドはデータベースから行を削除するために使われ、
下記の例では article の **id** が 10 の行を削除しています。::
=======
..
    Running Delete Statements

DELETE文を走らせる
-------------------------

..
    Similarly, the ``delete()`` method is used to delete rows from the database, the
    following example deletes the article with **id** 10::

同様に、``delete()`` メソッドはデータベースの行を削除するのに使われます。
次の例では **id** 10 の article をDELETEします::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;
    $connection = ConnectionManager::get('default');
    $connection->delete('articles', ['id' => 10]);

.. _database-configuration:

<<<<<<< Updated upstream
設定
=============

慣例として、データベース接続は **config/app.php** に設定します。
このファイルに定義された接続情報は、アプリケーションが使用する接続構成を生成する 
:php:class:`Cake\\Datasource\\ConnectionManager` に引き渡します。
サンプルとなる接続情報が **config/app.default.php** にあります。
サンプルの接続設定は、次のようになります。::
=======
..
    Configuration

コンフィグレーション
===================

..
    By convention database connections are configured in **config/app.php**. The
    connection information defined in this file is fed into
    :php:class:`Cake\\Datasource\\ConnectionManager` creating the connection configuration
    your application will be using. Sample connection information can be found in
    **config/app.default.php**. A sample connection configuration would look
    like::

慣例により、DBコネクションは **config/app.php** 内で設定します。
このファイルで定義されるコネクション情報は、あなたのアプリケーションで使われることになるコネクション設定を作成する
:php:class:`Cake\\Datasource\\ConnectionManager` に渡されます。
コネクション情報の例が **config/app.default.php** にあります。
コネクション情報の例は次のようなものです::
>>>>>>> Stashed changes

    'Datasources' => [
        'default' => [
            'className' => 'Cake\Database\Connection',
            'driver' => 'Cake\Database\Driver\Mysql',
            'persistent' => false,
            'host' => 'localhost',
            'username' => 'my_app',
            'password' => 'sekret',
            'database' => 'my_app',
            'encoding' => 'utf8',
            'timezone' => 'UTC',
            'cacheMetadata' => true,
        ]
    ],

<<<<<<< Updated upstream
上記は指定されたパラメータを持つ 'default' 接続を生成します。
あなたは設定ファイルに必要な数だけ接続を定義することができます。
また、 :php:meth:`Cake\\Datasource\\ConnectionManager::config()` を使って
実行時に追加の設定をおこなうこともできます。
その一例は次のようになります。::
=======
★★★★★★

..
    The above will create a 'default' connection, with the provided parameters. You
    can define as many connections as you want in your configuration file. You can
    also define additional connections at runtime using
    :php:meth:`Cake\\Datasource\\ConnectionManager::config()`. An example of that
    would be::

上記は提供されたパラメータを伴う 'default' コネクションを作成します。
設定ファイル上にいくつでもコネクションを定義できます。
:php:meth:`Cake\\Datasource\\ConnectionManager::config()` を使えば、実行中にコネクションの定義を追加することもできます。
たとえば次のようにです::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;

    ConnectionManager::config('default', [
        'className' => 'Cake\Database\Connection',
        'driver' => 'Cake\Database\Driver\Mysql',
        'persistent' => false,
        'host' => 'localhost',
        'username' => 'my_app',
        'password' => 'sekret',
        'database' => 'my_app',
        'encoding' => 'utf8',
        'timezone' => 'UTC',
        'cacheMetadata' => true,
    ]);

<<<<<<< Updated upstream
設定オプションは :term:`DSN` 文字列形式で設定することもできます。
これは、環境変数や :term:`PaaS` 環境で作業する時に便利です。::
=======
..
    Configuration options can also be provided as a :term:`DSN` string. This is
    useful when working with environment variables or :term:`PaaS` providers::

設定オプションは :term:`DSN` 文字列で渡すこともできます。
これは環境変数や :term:`PaaS` プロバイダを使うときに便利です::
>>>>>>> Stashed changes

    ConnectionManager::config('default', [
        'url' => 'mysql://my_app:sekret@localhost/my_app?encoding=utf8&timezone=UTC&cacheMetadata=true',
    ]);

<<<<<<< Updated upstream
DSN 文字列を使用するときには、クエリー文字列引数として追加のパラメータやオプションを
定義することができます。

デフォルトでは、すべてのテーブルオブジェクトは ``default`` の接続を使用します。
デフォルト以外の接続を使用するには、 :ref:`configuring-table-connections` を参照してください。

データベース設定ではいくつかのキーがサポートされています。使用可能なキーは下記の通りです。:

className
    データベースサーバへの接続を行うクラスの名前空間名付きの完全クラス名。
    このクラスは、データベースドライバをロードし、SQLトランザクションメカニズムを提供し、
    SQLを生成したりといったことを担当しています。
driver
    ドライバクラス名は、データベースエンジンのすべての特異性を実装するために使われます。
    これは :term:`プラグイン記法 <plugin syntax>` を用いた短いクラス名でも、
    完全名前空間名でも、どちらでもドライバインスタンスを生成することが可能です。
    短いクラス名の例は、 Mysql, Sqlite, Postgres, Sqlserver などです。
persistent
    データベースへの持続的接続を使うかどうか。
host
    データベースサーバのホスト名 （または IP アドレス）。
username
    アカウントのユーザー名。
password
    アカウントのパスワード。
database
    接続するデータベース名。
port (*optional*)
    サーバに接続する際に使用する TCP ポート または Unix ソケット。
encoding
    サーバに SQL 文を送信する際に使用する文字セットを示します。
    DB2 以外のデータベースでは、データベースのデフォルトエンコーディングが
    デフォルト設定されます。
    もし MySQL で UTF-8 で接続したいのなら、ハイフンなしで 'utf8' と指定してください。
timezone
    サーバーのタイムゾーンがセットされます。
schema
    PostgreSQL データベースで特定のスキーマを使う時に設定します。
unix_socket
    Unixソケットファイルを経由して接続することをサポートしているドライバによって
    使用されます。PostgreSQLを使用していて、Unixソケットを使用する場合は、 
    host を空白のままにします。
ssl_key
    SSLキー・ファイルへのファイルパス。 （MySQLのみでサポートされています）。
ssl_cert
    SSL証明書ファイルへのファイルパス。 （MySQLのみでサポートされています）。
ssl_ca
    SSL証明書の認証局へのファイルパス。 （MySQLのみでサポートされています）。
init
    接続が作成されたときに、データベースサーバに送信されるクエリーのリスト。
log
    クエリーログを有効にするには ``true`` をセットします。
    有効なクエリーで ``debug`` レベルの時に、 ``queriesLog`` スコープでログ出力されます。
quoteIdentifiers
    あなたがテーブルやカラム名に予約語や特殊文字を使用している場合は ``true`` に設定します。
    この設定を有効にすると、SQLを生成する際に :doc:`クエリービルダー</orm/query-builder>` 
    によって引用符で囲まれたクエリーが生成されます。
    これはクエリーを実行する前に横断的に処理を行う必要があるため、パフォーマンスを
    低下させることに注意してください。
flags
    ベースになる PDO のインスタンスに引き継がれる、 PDO 定数の連想配列。
    flags がサポートしている内容については、お使いの PDO ドライバのマニュアルを
    ご覧ください。
cacheMetadata
    boolean 型の ``true`` か、メタデータを格納するキャッシュ設定の文字列のどちらか。
    メタデータのキャッシュをオフにする事はお勧めしませんし、パフォーマンスがとても
    悪化します。詳細は :ref:`メタデータのキャッシュ<database-metadata-cache>` の項を
    参照してください。

この時点で、あなたは :doc:`/intro/conventions` を見たいと思うかもしれません。
正しいテーブル名（といくつかのカラムの追加）によって、いくつかの機能を獲得して、
設定を回避することができます。
例えば、もしデータベースのテーブル名が big\_boxes でしたら、 テーブルクラス 
BigBoxesTable と、コントローラ BigBoxesController は、全て自動的に一緒に
動作します。
慣例としてデータベースのテーブル名は、例えば bakers, pastry\_stores, savory\_cakes 
といった具合に、アンダースコア区切り・小文字・複数形とします。

.. php:namespace:: Cake\Datasource

=======
..
    When using a DSN string you can define any additional parameters/options as
    query string arguments.

DSN 文字列を使う際にはいかなる追加パラメータやオプションもクエリ文字列の引数として定義することができます。

..
    By default, all Table objects will use the ``default`` connection. To
    use a non-default connection, see :ref:`configuring-table-connections`.

デフォルトでは、すべてのテーブルオブジェクトが ``default`` コネクションを使います。
デフォルト以外のコネクションを使いたい場合は :ref:`configuring-table-connections` を参照してください。

..
    There are a number of keys supported in database configuration. A full list is
    as follows:

データベース設定でサポートされているキーはたくさんあります。
下記に挙げます:

..
    className
    The fully namespaced class name of the class that represents the connection to a database server.
    This class is responsible for loading the database driver, providing SQL
    transaction mechanisms and preparing SQL statements among other things.

className
    DBサーバへのコネクションを表すクラスの、名前空間を含む完全なクラス名。
    このクラスはデータベースドライバのロード、SQLトランザクション機構の提供、
    そして特にSQL文の準備(prepare)を担当します。

..
    driver
    The class name of the driver used to implements all specificities for
    a database engine. This can either be a short classname using :term:`plugin syntax`,
    a fully namespaced name, or a constructed driver instance.
    Examples of short classnames are Mysql, Sqlite, Postgres, and Sqlserver.

driver
    データベースエンジンのすべての特異性が実装されているドライバのクラス名。
    これには :term:`plugin syntax` を使う短いクラス名でも、名前空間を含む完全なクラス名でも、生成済みのドライバのインスタンスでも指定できます。

..
    persistent
    Whether or not to use a persistent connection to the database.

persistent
    データベースに持続接続(persistent connection)を使うか。

..
    host
    The database server's hostname (or IP address).

host
    データベースサーバのホスト名 (もしくはIPアドレス)。

..
    username
    The username for the account.

username
    接続アカウントのユーザ名。

..
    password
    The password for the account.

password
    接続ユーザのパスワード。

..
    database
    The name of the database for this connection to use.

database
    このコネクションで利用(use)したいのデータベース名。

..
    port (*optional*)
    The TCP port or Unix socket used to connect to the server.

port (*optional*)
    サーバに接続するのに使うTCPポートもしくはUnixソケット。

..
    encoding
    Indicates the character set to use when sending SQL statements to
    the server. This defaults to the database's default encoding for
    all databases other than DB2. If you wish to use UTF-8 encoding
    with MySQL connections you must use 'utf8' without the
    hyphen.

encoding
    SQL文をサーバに送る際に使うキャラクタセットを指定します。
    DB2 以外のすべてのデータベースで、これがデータベースのデフォルトエンコーディングとなります。
    もし MySQL 接続で UTF-8 エンコーディングを使いたいなら、ハイフン(-)なしで 'utf8' と指定する必要があります。

..
    timezone
    Server timezone to set.

timezone
    セットしたいサーバのタイムゾーン。

..
    schema
    Used in PostgreSQL database setups to specify which schema to use.

schema
    PostgreSQL のDBセットアップで、どのスキーマを利用(use)するのか指定するのに使われます。

..
    unix_socket
    Used by drivers that support it to connect via Unix socket files. If you are
    using PostgreSQL and want to use Unix sockets, leave the host key blank.

unix_socket
    Unix ソケットファイルを介しての接続をサポートするドライバによって使われます。
    もしも PostgreSQL を使っており、Unix を使いたいなら、ホストキー(host key)は空欄(blank)にしてください。

..
    ssl_key
    The file path to the SSL key file. (Only supported by MySQL).

ssl_key
    SSLキーファイルのファイルパス(MySQLでのみサポート)。

..
    ssl_cert
    The file path to the SSL certificate file. (Only supported by MySQL).

ssl_cert
    SSL証明書ファイル(SSL certificate file)のファイルパス(MySQLでのみサポート)。

..
    ssl_ca
    The file path to the SSL certificate authority. (Only supported by MySQL).

ssl_ca
    SSL認証局(SSL certificate authority)のファイルパス(MySQLでのみサポート)。

..
    init
    A list of queries that should be sent to the database server as
    when the connection is created.

init
    コネクションが生成された際にデータベースサーバに送信すべきクエリのリスト。

..
    log
    Set to ``true`` to enable query logging. When enabled queries will be logged
    at a ``debug`` level with the ``queriesLog`` scope.

log
    ``true`` をセットした場合はクエリのログ出力が有効になります。
    有効なクエリは、``queriesLog`` スコープ、``debug`` レベルでログ出力されます。

..
    quoteIdentifiers
    Set to ``true`` if you are using reserved words or special characters in your
    table or column names. Enabling this setting will result in queries built using the
    :doc:`/orm/query-builder` having identifiers quoted when creating SQL. It should be
    noted that this decreases performance because each query needs to be traversed
    and manipulated before being executed.

quoteIdentifiers
    予約語や特殊文字をテーブル名や列名で使用しているなら ``true`` をセットしてください。
    この設定を有効にすると、:doc:`/orm/query-builder` を使って構築した場合、SQL生成時にクエリ内の識別子に引用符が付きます。
    これを設定すると、各クエリの実行前に検査と変更が必要になるため、パフォーマンスが下がることに注意してください。

..
    flags
    An associative array of PDO constants that should be passed to the
    underlying PDO instance. See the PDO documentation for the flags supported
    by the driver you are using.

flags
    内部の PDO インスタンスに渡される PDO 定数の連想配列。
    使用するドライバでサポートされるフラグについては PDO のドキュメントを参照してください。

..
    cacheMetadata
    Either boolean ``true``, or a string containing the cache configuration to store
    meta data in. Having metadata caching disable is not advised and can result
    in very poor performance. See the :ref:`database-metadata-cache` section
    for more information.

cacheMetadata
    boolean の ``true`` か、もしくはメタデータを保存するキャッシュ設定の入った文字列。
    メタデータのキャッシュを無効にすることはオススメできません。パフォーマンスが著しく落ちます。
    :ref:`database-metadata-cache` の章を参照してください。

..
    At this point, you might want to take a look at the
    :doc:`/intro/conventions`. The correct
    naming for your tables (and the addition of some columns) can score
    you some free functionality and help you avoid configuration. For
    example, if you name your database table big\_boxes, your table
    BigBoxesTable, and your controller BigBoxesController, everything will
    work together automatically. By convention, use underscores, lower case,
    and plural forms for your database table names - for example:
    bakers, pastry\_stores, and savory\_cakes.

この辺で、:doc:`/intro/conventions` を覗いてみたくなるかもしれません。
テーブル（といくつかの列）を正しく命名すると、いくつか自由★な機能が得られ、設定を避けることができます。
たとえば、もしデータベーステーブルを big\_boxes、テーブルを BigBoxesTable、コントローラを BigBoxesController と名付けていれば、すべてが自動で動くようになります。
慣例により、データベースのテーブル名はアンダースコアつなぎの、小文字の複数形にしてください。例: bakers 、 pastry\_stores 、 savory\_cakes

.. php:namespace:: Cake\Datasource

..
    Managing Connections

>>>>>>> Stashed changes
コネクションの管理
====================

.. php:class:: ConnectionManager

<<<<<<< Updated upstream
``ConnectionManager`` クラスは、あなたのアプリケーションがデータベース接続に
アクセスするためのレジストリとして機能します。
これは他のオブジェクトが既存のコネクションへの参照を取得するための場所を提供します。

コネクションへのアクセス
-----------------------------

.. php:staticmethod:: get($name)

一度設定した接続は、 :php:meth:`Cake\\Datasource\\ConnectionManager::get()` を
使って取り出すことができます。
このメソッドはすでに確立しているコネクションを返すか、もしまだ接続していないのであれば
ロードして接続してから返します。::
=======
    The ``ConnectionManager`` class acts as a registry to access database connections your
    application has. It provides a place that other objects can get references to
    existing connections.

``ConnectionManager`` クラスはアプリケーションが持つDBコネクションにアクセスするためのレジストリの役割を担います。

..
    Accessing Connections

コネクションへのアクセス
---------------------

.. php:staticmethod:: get($name)

..
    Once configured connections can be fetched using
    :php:meth:`Cake\\Datasource\\ConnectionManager::get()`. This method will
    construct and load a connection if it has not been built before, or return the
    existing known connection::

一旦設定されたコネクションは :php:meth:`Cake\\Datasource\\ConnectionManager::get()` を使ってフェッチできます。
このメソッドはまだビルドされていないなら、コネクションをロードし、構築します。ビルドされていればビルド済のコネクションを返します::
>>>>>>> Stashed changes

    use Cake\Datasource\ConnectionManager;

    $conn = ConnectionManager::get('default');

<<<<<<< Updated upstream
存在しない接続をロードしようとしたら、例外を throw します。
=======
..
    Attempting to load connections that do not exist will throw an exception.

存在しないコネクションをロードしようとしたら、例外を投げます。

..
    Creating Connections at Runtime
>>>>>>> Stashed changes

実行時にコネクションを生成する
-------------------------------

<<<<<<< Updated upstream
``config()`` や ``get()`` を使用して、実行時に設定ファイルに定義されていない
コネクションを生成することができます。::
=======
..
    Using ``config()`` and ``get()`` you can create new connections that are not
    defined in your configuration files at runtime::

``config()`` と ``get()`` を使うことで、設定ファイルに定義されていない新たなコネクションを実行時に生成することができます::
>>>>>>> Stashed changes

    ConnectionManager::config('my_connection', $config);
    $conn = ConnectionManager::get('my_connection');

<<<<<<< Updated upstream
コネクション生成時の設定についての詳細は :ref:`database-configuration` を参照してください。
=======
..
    See the :ref:`database-configuration` for more information on the configuration
    data used when creating connections.

コネクションを生成する際に使われる設定データの詳細は :ref:`database-configuration` を参照してください。
>>>>>>> Stashed changes

.. _database-data-types:

.. php:namespace:: Cake\Database

<<<<<<< Updated upstream
データの型
==============

.. php:class:: Type

各ベンダーのデータベースは全て同じデータ型を持つわけではなく、似たようなデータ型が
同じ名前になっているわけでもありませんので、 CakePHP ではデータベース層で使用するために
基本的なデータ型のセットを提供しています。CakePHP がサポートしている型は、

string
    一般的に CHAR または VARCHAR のカラムが指定されます。
    ``fixed`` オプションを使うと、強制的に CHAR カラムとなります。
    SQL Server では、NCHAR と NVARCHAR 型になります。
text
    TEXT 型に変換します。
uuid
    データベースがサポートするなら UUID 型に、さもなければ CHAR(36) に変換します。
integer
    データベースがサポートするなら INTEGER 型に変換します。
biginteger
    データベースがサポートするなら BIGINT 型に変換します。
float
    データベースに応じて DOUBLE 型か FLOAT 型に変換されます。
    精度（小数点以下桁数）を指定するために ``precision`` オプションを使うことができます。
decimal
    DECIMAL 型に変換されます。 ``length`` と ``precision`` オプションをサポート
    します。
boolean
    BOOLEAN に変換します。（ MySQL の場合は TINYINT(1) になります。）
binary
    データベースに応じて BLOB または BYTEA 型に変換します。
date
    タイムゾーン情報を持たない DATE 型に変換されます。
datetime
    タイムゾーン情報を持たない DATETIME 型に変換されます。
    PostgreSQL と SQL Server では、TIMESTAMP 型に変換されます。
    この型のデフォルトの戻り値は、内蔵の ``DateTime`` クラスと 
    `Carbon <https://github.com/briannesbitt/Carbon>`_ を拡張した 
    :php:class:`Cake\\I18n\\Time` クラスになります。
timestamp
    TIMESTAMP 型に変換します。
time
    全てのデータベースで TIME 型に変換します。

これらの型は、テストフィクスチャを使用している時に、CakePHP が提供する
スキーマリフレクション機能とスキーマ生成機能の両方で使用されます。

また、各型は PHP と SQL の表現の変換を行う機能も提供します。
これらのメソッドはクエリー実行時に型のヒントに基づいて呼び出されます。
例えば、 'datetime' という名前の項目なら、入力パラメータを自動的に ``DateTime`` から 
timestamp か 整形した日付文字列に変換します。
同様に 'binary' という名前の項目ならファイルハンドラを受け入れ、データを読み込むときには
ファイルハンドラを生成します。

.. _adding-custom-database-types:

独自の型を作成する
=======
..
    Data Types

データ型
==========

.. php:class:: Type

..
    Since not every database vendor includes the same set of data types, or
    the same names for similar data types, CakePHP provides a set of abstracted
    data types for use with the database layer. The types CakePHP supports are:

すべてのDBベンダが、まったく同じデータ型一式を持っているわけではありませんし、同じようなデータ型に同じ名前がついているとも限りませんので、
CakePHP では DBレイヤーで利用できる抽象的なデータ型を提供します。CakePHP がサポートするのは次の型です:

..
    string
        Generally backed by CHAR or VARCHAR columns. Using the ``fixed`` option
        will force a CHAR column. In SQL Server, NCHAR and NVARCHAR types are used.
    text
        Maps to TEXT types
    uuid
        Maps to the UUID type if a database provides one, otherwise this will
        generate a CHAR(36) field.
    integer
        Maps to the INTEGER type provided by the database.
    biginteger
        Maps to the BIGINT type provided by the database.
    float
        Maps to either DOUBLE or FLOAT depending on the database. The ``precision``
        option can be used to define the precision used.
    decimal
        Maps to the DECIMAL type. Supports the ``length`` and  ``precision``
        options.
    boolean
        Maps to BOOLEAN except in MySQL, where TINYINT(1) is used to represent
        booleans.
    binary
        Maps to the BLOB or BYTEA type provided by the database.
    date
        Maps to a timezone naive DATE column type.
    datetime
        Maps to a timezone naive DATETIME column type. In PostgreSQL, and SQL Server
        this turns into a TIMESTAMP type. The default return value of this column
        type is :php:class:`Cake\\I18n\\Time` which extends the built-in
        ``DateTime`` class and `Carbon <https://github.com/briannesbitt/Carbon>`_.
    timestamp
        Maps to the TIMESTAMP type.
    time
        Maps to a TIME type in all databases.

string
    多くの場合は CHAR や VARCHAR の列とみなされます。 ``fixed`` オプションで、 CHAR 列であることを強制できます。SQL サーバでは、NCHAR and NVARCHAR 型が使われます。
text
    TEXT 型にマッピングされます。
uuid
    DB がサポートしているなら UUID 型にマッピングされます。そうでないなら CHAR(36) の列が生成されます。
integer
    DB が提供する INTEGER 型にマッピングされます。
biginteger
    DB が提供する BIGINT 型にマッピングされます。
float
    DB に応じて DOUBLE や FLOAT 型にマッピングされます。``precision`` オプションで使用する精度を定義できます。
decimal
    DECIMAL 型にマッピングされます。``length`` と ``precision`` オプションをサポートしています。
boolean
    MySQL 以外なら BOOLEAN 、MySQL ならそれを表すのに TINYINT(1) を使います。
binary
    DB が提供する BLOB や BYTEA 型にマッピングされます。
date
    タイムゾーンありの DATE 型にマッピングされます。
datetime
    タイムゾーンありの DATETIME 型にマッピングされます。PostgreSQL と SQLサーバの場合は、TIMESTAMP 型に変わります。
    このカラム型のデフォルトの戻り値は、組み込みクラス ``DateTime`` と `Carbon <https://github.com/briannesbitt/Carbon>`_ を継承した :php:class:`Cake\\I18n\\Time` になります。
timestamp
    TIMESTAMP 型にマッピングされます。
time
    すべての DB で TIME 型にマッピングされます。

..
    These types are used in both the schema reflection features that CakePHP
    provides, and schema generation features CakePHP uses when using test fixtures.

これらの型は CakePHP が提供する schema の 反映機能と、テストフィクスチャ(test fixture)で使われる schema 生成機能の両方で使われます。

..
    Each type can also provide translation functions between PHP and SQL
    representations. These methods are invoked based on the type hints provided when
    doing queries. For example a column that is marked as 'datetime' will
    automatically convert input parameters from ``DateTime`` instances into a
    timestamp or formatted datestrings. Likewise, 'binary' columns will accept file
    handles, and generate file handles when reading data.

それぞれの型は PHP 表現と SQL 表現の間の翻訳機能もまた提供します。それらのメソッドは提供される型ヒントに基づきクエリ実行時に呼び出されます。
たとえば、'datetime' と印のついた列は入力パラメータを ``DateTime`` のインスタンスから timestamp もしくはフォーマットされた文字列へと自動的に変換します。
'binary' の列も同様にファイルハンドルを受け入れ、読むときにはファイルハンドルを生成します。

.. _adding-custom-database-types:

..
    Adding Custom Types

カスタム型の追加
>>>>>>> Stashed changes
-------------------

.. php:staticmethod:: map($name, $class)

<<<<<<< Updated upstream
もしあなたが CakePHP に実装されていない、データベース独自の型が必要な場合、
CakePHP の型システムに新たな型を追加することができます。
Type クラスは次のメソッドを実装することが期待されます。
=======
..
    If you need to use vendor specific types that are not built into CakePHP you can
    add additional new types to CakePHP's type system. Type classes are expected to
    implement the following methods:

CakePHP に入っていないベンダー固有の型を使う必要がある場合には、 CakePHP の型システムに新しい型を追加することができます。
>>>>>>> Stashed changes

* toPHP
* toDatabase
* toStatement
* marshal

<<<<<<< Updated upstream
基本的なインタフェースを満たす簡単な方法は、 :php:class:`Cake\\Database\\Type` を
拡張することです。例えば、もしあなたが JSON型を追加したいなら、下記のような型クラスを
作成します。::
=======
..
    An easy way to fulfill the basic interface is to extend
    :php:class:`Cake\\Database\\Type`. For example if we wanted to add a JSON type,
    we could make the following type class::

基本的なインターフェイスを実現する簡単な方法は :php:class:`Cake\\Database\\Type` を継承することです。
たとえば JSON 型を追加したい場合には、下記の型のクラスを作成することができます::

>>>>>>> Stashed changes

    // in src/Database/Type/JsonType.php

    namespace App\Database\Type;

    use Cake\Database\Driver;
    use Cake\Database\Type;
    use PDO;

    class JsonType extends Type
    {

        public function toPHP($value, Driver $driver)
        {
            if ($value === null) {
                return null;
            }
            return json_decode($value, true);
        }

        public function marshal($value)
        {
            if (is_array($value) || $value === null) {
                return $value;
            }
            return json_decode($value, true);
        }

        public function toDatabase($value, Driver $driver)
        {
            return json_encode($value);
        }

        public function toStatement($value, Driver $driver)
        {
            if ($value === null) {
                return PDO::PARAM_NULL;
            }
            return PDO::PARAM_STR;
        }

    }

<<<<<<< Updated upstream
デフォルトでは ``toStatement()`` メソッドは新しい型の値を文字列として扱います。
私たちは新しい型を作成したら、型マッピングに追加しなければなりません。
アプリケーションの bootstrap 時に、次の事を行います。::
=======
..
    By default the ``toStatement()`` method will treat values as strings which will
    work for our new type. Once we've created our new type, we need to add it into
    the type mapping. During our application bootstrap we should do the following::

デフォルトで、``toStatement()`` メソッドは値を新しい型として機能する文字列として扱います。
新しい型を作ったら、それを型マッピング(type mapping)に追加しなければなりません。
アプリケーションの bootstrap で次のようにしてください::
>>>>>>> Stashed changes

    use Cake\Database\Type;

    Type::map('json', 'App\Database\Type\JsonType');

<<<<<<< Updated upstream
こうすればスキーマ情報は新しい型で上書きされ、CakePHP のデータベース層は自動的に 
JSON データを変換してクエリーを作成します。
あなたは Table の :ref:`_initializeSchema() メソッド <saving-complex-types>` で、
新たに作った型のマッピングをすることができます。::
    
=======
..
    We can then overload the reflected schema data to use our new type, and
    CakePHP's database layer will automatically convert our JSON data when creating
    queries. You can use the custom types you've created by mapping the types in
    your Table's :ref:`_initializeSchema() method <saving-complex-types>`::

こうして、反映(reflect)済の schema データをオーバーロードして新しい型を使うことができ、
CakePHP のDB層がクエリを作る際に JSON データを自動的に変換してくれます。★::

>>>>>>> Stashed changes
    use Cake\Database\Schema\Table as Schema;

    class WidgetsTable extends Table
    {
    
        protected function _initializeSchema(Schema $schema)
        {
            $schema->columnType('widget_prefs', 'json');
            return $schema;
        }
    
    }

<<<<<<< Updated upstream
Connection クラス
=======
..
    Connection Classes

コネクションクラス
>>>>>>> Stashed changes
==================

.. php:class:: Connection

<<<<<<< Updated upstream
Connection クラスは、一貫性のある方法でデータベースコネクションと対話するための
シンプルなインタフェースを提供します。
これはドライバ層への基底インタフェースであり、クエリーの実行、クエリーのロギング、
トランザクション処理といった機能を提供するためのものです。

.. _database-queries:

クエリーの実行
=======
..
    Connection classes provide a simple interface to interact with database
    connections in a consistent way. They are intended as a more abstract interface to
    the driver layer and provide features for executing queries, logging queries, and doing
    transactional operations.

コネクションクラスは一貫した方法でDBコネクションとやりとりするためのシンプルなインターフェイスを提供します。
それらはドライバ層へのより抽象的なインターフェイスであるよう意図されており、
クエリの実行機能、クエリのログ出力機能、トランザクション動作の実行機能を提供します。

.. _database-queries:

..
    Executing Queries

クエリの実行
>>>>>>> Stashed changes
-----------------

.. php:method:: query($sql)

<<<<<<< Updated upstream
あなたがコネクションオブジェクトを取得したら、恐らく何らかのクエリーを発行したくなるでしょう。
CakePHP のデータベース抽象化レイヤは、PDO とネイティブドライバ上にラッパー機能を提供します。
これらのラッパーは PDO と似たようなインタフェースを提供します。
クエリーを実行する方法は、あなたが実行したいクエリーと取得したい結果の種類に応じて
いくつかあります。
もっとも基本的な方法は、完全な SQL クエリーの実行を可能にする ``query()`` です。::
=======
..
    Once you've gotten a connection object, you'll probably want to issue some
    queries with it. CakePHP's database abstraction layer provides wrapper features
    on top of PDO and native drivers. These wrappers provide a similar interface to
    PDO. There are a few different ways you can run queries depending on the type of
    query you need to run and what kind of results you need back. The most basic
    method is ``query()`` which allows you to run already completed SQL queries::

コネクションオブジェクトを取得したら、おそらくそれを使ってクエリをいくつか実行したくなるでしょう。
CakePHP の DB 抽象層は PDO とネイティブドライバに上にラッパー(包含)機能を提供します。
それらのラッパーは PDO へ繋がる同様のインターフェイスを提供します。
走らせる必要のあるクエリの種類や返す必要のある結果の種類により、クエリを走らせるのには、いくつかの違う方法が存在します。
もっとも基本的なメソッドが ``query()`` であり、これによって構築済の SQL クエリを走らせることができるようになります。 ::
>>>>>>> Stashed changes

    $stmt = $conn->query('UPDATE posts SET published = 1 WHERE id = 2');

.. php:method:: execute($sql, $params, $types)

<<<<<<< Updated upstream
``query()`` メソッドは追加パラメータを受け付けません。
もし追加パラメータが必要なら、プレースホルダを使用可能な ``execute()`` メソッドを使用します。::
=======
..
    The ``query()`` method does not allow for additional parameters. If you need
    additional parameters you should use the ``execute()`` method, which allows for
    placeholders to be used::

``query()`` メソッ ドでは追加パラメータを渡せません。追加パラメータを渡したい場合は、 ``execute()`` メソッドを使ってください。
このメソッドではプレイスホルダを使えます。 ::
>>>>>>> Stashed changes

    $stmt = $conn->execute(
        'UPDATE posts SET published = ? WHERE id = ?',
        [1, 2]
    );

<<<<<<< Updated upstream
型に関する情報がない場合は、 ``execute`` は全てのプレースホルダを文字列とみなします。
もし特定の型にバインドする必要があるなら、クエリーを生成する時に型名を指定することが
できます。::
=======
..
    Without any type hinting information, ``execute`` will assume all placeholders
    are string values. If you need to bind specific types of data, you can use their
    abstract type names when creating a query::

タイプヒンティング情報が何もない場合、 ``execute`` はすべてのプレイスホルダを文字列とみなします。
もしも特定のデータ型でバインドしたいのなら、クエリ生成時に抽象型名を使うことができます。 ::
>>>>>>> Stashed changes

    $stmt = $conn->execute(
        'UPDATE posts SET published_date = ? WHERE id = ?',
        [new DateTime('now'), 2],
        ['date', 'integer']
    );

.. php:method:: newQuery()

<<<<<<< Updated upstream
これはあなたのアプリケーションで豊富なデータ型を使用し、適切にSQL文に変換することができます。
クエリを作成する最後の、そして最も柔軟な方法は、  :doc:`クエリビルダ</orm/query-builder>` を
使用することです。
この方法では、プラットフォーム固有のSQLを使用することなく、複雑で表現力豊かなクエリを
構築することができます::
=======
..
    This allows you to use rich data types in your applications and properly convert
    them into SQL statements. The last and most flexible way of creating queries is
    to use the :doc:`/orm/query-builder`. This approach allows you to build complex and
    expressive queries without having to use platform specific SQL::

これにより、豊富なデータ型を自分のアプリケーションの中で使うことができ、それらを正しく変換して、SQL文の中へと入れることができるようになります。::
>>>>>>> Stashed changes

    $query = $conn->newQuery();
    $query->update('posts')
        ->set(['publised' => true])
        ->where(['id' => 2]);
    $stmt = $query->execute();

<<<<<<< Updated upstream
クエリビルダを使用する場合は、 ``execute()`` メソッドを呼ぶまではサーバーにSQLは
送信されず、メソッド呼び出し後に順次処理されます。
最初に送信してから、順次結果セットを作成します。::
=======
..
    When using the query builder, no SQL will be sent to the database server until
    the ``execute()`` method is called, or the query is iterated. Iterating a query
    will first execute it and then start iterating over the result set::

クエリビルダを利用する場合、``execute()`` メソッドが呼ばれるまで、もしくは、
クエリがイレテート(foreachでの繰り返し)されるまで、SQL は DB サーバに送信されません。
クエリのイレテートでは、まず実行(execute)された後、結果セットに対するイレテートが始まります。 ::
>>>>>>> Stashed changes

    $query = $conn->newQuery();
    $query->select('*')
        ->from('posts')
        ->where(['published' => true]);

    foreach ($query as $row) {
        // Do something with the row.
    }
<<<<<<< Updated upstream

.. note::

    もし :php:class:`Cake\\ORM\\Query` のインスタンスを生成しているのなら、
    SELECT クエリの結果セットを取得するのに ``all()`` を使用できます。

トランザクションを使う
--------------------------

コネクションオブジェクトは、データベーストランザクションを行うためのいくつかの簡単な
方法を提供します。
トランザクション操作の最も基本的な方法は、SQL構文と同じような ``begin()`` , 
``commit()`` , ``rollback()`` を使用するものです。::

    $conn->begin();
    $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [true, 2]);
    $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [false, 4]);
    $conn->commit();

.. php:method:: transactional(callable $callback)

このコネクションインスタンスへのインターフェースに加えて、さらに begin/commit/rollback を
簡単にハンドリングする ``transactional()`` メソッドが提供されています。::

    $conn->transactional(function ($conn) {
        $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [true, 2]);
        $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [false, 4]);
    });

基本的なクエリに加えて、 :doc:`/orm/query-builder` または :doc:`/orm/table-objects` の
いずれかを使用してより複雑なクエリを実行することができます。
トランザクションメソッドは下記のことを実行します。

- ``begin`` を呼び出します。
- 引数で渡されたクロージャーを実行します。
- もしクロージャー内で例外が発生したら、ロールバックを発行して例外を再度 throw します。
- クロージャーが ``false`` を返したら、ロールバックを発行して false を返します。
- クロージャーが正常終了したら、トランザクションをコミットします。

ステートメントとの対話
===========================

基底レベルのデータベース API を使用していると、ステートメントオブジェクトが
よく出てきます。
これらのオブジェクトで、ドライバから基になるプリペアドステートメントを操作できるように
なります。
クエリオブジェクトを生成し実行するか ``execute()`` を実行した後、あなたは
``StatementDecorator`` インスタンスを持つ事になります。
これはベースとなる基本的なステートメントオブジェクトをラップして、追加の機能を
提供します。

ステートメントを準備する
------------------------------

あなたは ``execute()`` か ``prepare()`` でステートメントオブジェクトを生成できます。
``execute()`` メソッドは引き継いだ値をバインドしたステートメントを返します。
それに対して ``prepare()`` は不完全なステートメントを返します。::

    // execute は指定された値でバインドしてSQLステートメントを実行します。
    $stmt = $conn->execute(
        'SELECT * FROM articles WHERE published = ?',
        [true]
    );

    // prepare はプレースフォルダのための準備をします。
    // 実行する前にパラメータをバインドする必要があります。
    $stmt = $conn->prepare('SELECT * FROM articles WHERE published = ?');

SQL文を準備したら、あなたは追加のデータをバインドし、それを実行することができます。

値をバインドする
--------------------

プリペアドステートメントを作成したら、追加のデータをバインドする必要があります。
あなたは ``bind()`` メソッドを使って一度に複数の値をバインドする事も、
``bindValue`` を使って１項目ずつバインドする事もできます。::

    $stmt = $conn->prepare(
        'SELECT * FROM articles WHERE published = ? AND created > ?'
    );

    // 複数項目のバインド
    $stmt->bind(
        [true, new DateTime('2013-01-01')],
        ['boolean', 'date']
    );

    // １項目ずつのバインド
    $stmt->bindValue(0, true, 'boolean');
    $stmt->bindValue(1, new DateTime('2013-01-01'), 'date');

ステートメントを作成する時には、項目の通し番号ではなく、項目名の配列をキーに
使用することもできます。::

    $stmt = $conn->prepare(
        'SELECT * FROM articles WHERE published = :published AND created > :created'
    );

    // 複数項目のバインド
    $stmt->bind(
        ['published' => true, 'created' => new DateTime('2013-01-01')],
        ['published' => 'boolean', 'created' => 'date']
    );

    // １項目ずつのバインド
    $stmt->bindValue('published', true, 'boolean');
    $stmt->bindValue('created', new DateTime('2013-01-01'), 'date');

.. warning::

    同じステートメント内で、項目の通し番号と項目名のキーを混在させることはできません。

実行と結果行の取得
-------------------------

プリペアドステートメントを作成してデータをバインドしたら、実行して行フェッチすることが
できます。
ステートメントは ``execute()`` メソッドで実行します。
一度実行したら、結果は ``fetch()`` か ``fetchAll()`` を使ってフェッチします。::

    $stmt->execute();

    // １行読み込む
    $row = $stmt->fetch('assoc');

    // 全行を読み込む
    $rows = $stmt->fetchAll('assoc');

    // 全行読み込んだ結果を順次処理する
    foreach ($rows as $row) {
        // Do work
    }

.. note::

    読み込んだフェッチする時には、２つのモードを使用することができます。
    結果配列のキーを項目の通番にする場合 (num) と、項目名をキーにする場合 (assoc) です。


行数を取得する
------------------

ステートメントを実行したら、下記のように対象行数を取得することができます。::

    $rowCount = count($stmt);
    $rowCount = $stmt->rowCount();


エラーコードをチェックする
---------------------------

あなたのクエリーが成功しなかった場合は、エラー関連情報を ``errorCode()`` と ``errorInfo()`` メソッド
によって取得することができます。
このメソッドは PDO で提供されているものと同じように動作します。::

    $code = $stmt->errorCode();
    $info = $stmt->errorInfo();

.. todo::
    Possibly document CallbackStatement and BufferedStatement

.. _database-query-logging:

Query Logging
=============

あなたのコネクションを設定する時に、 ``log`` オプションに ``true`` をセットすると
クエリーのログを有効にすることができます。
また、 ``logQueries`` を使って実行中にクエリログを切り替えることができます。::

    // Turn query logging on.
    $conn->logQueries(true);

    // Turn query logging off
    $conn->logQueries(false);

クエリログを有効にしていると、 'debug' レベルで 'queriesLog' スコープで
:php:class:`Cake\\Log\\Log` にクエリをログ出力します。
あなたはこのレベル・スコープを出力するようにログ設定をする必要があります。
``stderr`` にログ出力するのはユニットテストの時に便利で、files/syslog に出力するのは
Web リクエストの時に便利です。::

    use Cake\Log\Log;

    // Console logging
    Log::config('queries', [
        'className' => 'Console',
        'stream' => 'php://stderr',
        'scopes' => ['queriesLog']
    ]);

    // File logging
    Log::config('queries', [
        'className' => 'File',
        'path' => LOGS,
        'file' => 'queries.log',
        'scopes' => ['queriesLog']
    ]);

.. note::

    クエリログは、デバッグまたは開発用途での利用を想定しています。
    アプリケーションのパフォーマンスに悪影響を及ぼしますので、公開サイトでは
    利用すべきではありません。

.. _identifier-quoting:

引用識別子
==================

デフォルトの CakePHP では、生成される SQL 文は引用符で囲まれて **いません** 。
その理由は、引用識別子はいくつかの問題があるためです。

* パフォーマンスへの負荷 - 引用符を使うと、使わない時よりずっと遅く、複雑になります。
* ほとんどの場合に不要 - CakePHP の規約に従う新しいデータベースでは、引用符で囲む必要はありません。

もしあなたが引用符が必要な古いスキーマを使用しているなら、
:ref:`データベースの設定 <database-configuration>` で ``quoteIdentifiers`` を設定すると
引用符を使うことができます。
また、実行時にこの機能を有効にすることもできます。::

    $conn->driver()->autoQuoting(true);

有効にすると、引用識別子は 全ての識別子を ``IdentifierExpression`` オブジェクトに
変換するトラバーサルが発生する原因になります。

.. note::

    QueryExpression オブジェクトに含まれる SQL スニペットは変換されません。

.. _database-metadata-cache:

メタデータ・キャッシング
============================

CakePHP の ORM は、あなたのアプリケーションのスキーマ、インデックス、外部キーを
決定するために、データベースリフレクションを使用します。
このメタデータは頻繁に変更され、アクセスにコストがかかるため、一般的にキャッシュされます。
デフォルトでは、メタデータは ``_cake_model_`` キャッシュ設定に保存されます。
あなたはデータベース設定の ``cacheMetatdata`` オプションを使って
カスタムキャッシュ設定を定義することができます。::
=======

.. note::

    :php:class:`Cake\\ORM\\Query` のインスタンスを持っているなら、 ``all()`` を使って、SELECT クエリの結果セットを取得することができます。

..
    When you have an instance of :php:class:`Cake\\ORM\\Query` you can use
    ``all()`` to get the result set for SELECT queries.

..
    Using Transactions

トランザクションの利用
---------------------

..
    The connection objects provide you a few simple ways you do database
    transactions. The most basic way of doing transactions is through the ``begin()``,
    ``commit()`` and ``rollback()`` methods, which map to their SQL equivalents::

コネクション オブジェクトはデータベース トランザクションを行うためのシンプルな方法をいくつか提供します。 ::

    $conn->begin();
    $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [true, 2]);
    $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [false, 4]);
    $conn->commit();

.. php:method:: transactional(callable $callback)

..
    In addition to this interface connection instances also provide the
    ``transactional()`` method which makes handling the begin/commit/rollback calls
    much simpler::

コネクション インスタンスは、このインターフェイスに加えて、begin/commit/rollback の呼び出しを扱う ``transactional()`` メソッドも提供します。 ::

    $conn->transactional(function ($conn) {
        $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [true, 2]);
        $conn->execute('UPDATE posts SET published = ? WHERE id = ?', [false, 4]);
    });

..
    In addition to basic queries, you can execute more complex queries using either
    the :doc:`/orm/query-builder` or :doc:`/orm/table-objects`. The transactional method will
    do the following:

基本的なクエリに加えて、:doc:`/orm/query-builder` や :doc:`/orm/table-objects` を使う、より複雑なクエリを実行することができます。
transactional メソッドは下記のように使います。 ::

- ``begin`` を呼ぶ。
- 提供されたクロージャを呼ぶ。
- クロージャが例外を投げたら、ロールバックを実行し、その例外を再び投げる。
- クロージャが ``false`` を返したら、ロールバックを実行する。
- クロージャの実行に成功したら、トランザクションをコミットする。

..
    - Call ``begin``.
    - Call the provided closure.
    - If the closure raises an exception, a rollback will be issued. The original
      exception will be re-thrown.
    - If the closure returns ``false``, a rollback will be issued.
    - If the closure executes successfully, the transaction will be committed.

..
    Interacting with Statements

文を用いた対話
===========================

..
    When using the lower level database API, you will often encounter statement
    objects. These objects allow you to manipulate the underlying prepared statement
    from the driver. After creating and executing a query object, or using
    ``execute()`` you will have a ``StatementDecorator`` instance. It wraps the
    underlying basic statement object and provides a few additional features.



Preparing a Statement
---------------------

You can create a statement object using ``execute()``, or ``prepare()``. The
``execute()`` method returns a statement with the provided values bound to it. While
``prepare()`` returns an incomplete statement::

    // Statements from execute will have values bound to them already.
    $stmt = $conn->execute(
        'SELECT * FROM articles WHERE published = ?',
        [true]
    );

    // Statements from prepare will be parameters for placeholders.
    // You need to bind parameters before attempting to execute it.
    $stmt = $conn->prepare('SELECT * FROM articles WHERE published = ?');

Once you've prepared a statement you can bind additional data and execute it.

Binding Values
--------------

Once you've created a prepared statement, you may need to bind additional data.
You can bind multiple values at once using the ``bind()`` method, or bind
individual elements using ``bindValue``::

    $stmt = $conn->prepare(
        'SELECT * FROM articles WHERE published = ? AND created > ?'
    );

    // Bind multiple values
    $stmt->bind(
        [true, new DateTime('2013-01-01')],
        ['boolean', 'date']
    );

    // Bind a single value
    $stmt->bindValue(0, true, 'boolean');
    $stmt->bindValue(1, new DateTime('2013-01-01'), 'date');

When creating statements you can also use named array keys instead of
positional ones::

    $stmt = $conn->prepare(
        'SELECT * FROM articles WHERE published = :published AND created > :created'
    );

    // Bind multiple values
    $stmt->bind(
        ['published' => true, 'created' => new DateTime('2013-01-01')],
        ['published' => 'boolean', 'created' => 'date']
    );

    // Bind a single value
    $stmt->bindValue('published', true, 'boolean');
    $stmt->bindValue('created', new DateTime('2013-01-01'), 'date');

.. warning::

    You cannot mix positional and named array keys in the same statement.

Executing & Fetching Rows
-------------------------

After preparing a statement and binding data to it, you can execute it and fetch
rows. Statements should be executed using the ``execute()`` method. Once
executed, results can be fetched using ``fetch()``, ``fetchAll()`` or iterating
the statement::

    $stmt->execute();

    // Read one row.
    $row = $stmt->fetch('assoc');

    // Read all rows.
    $rows = $stmt->fetchAll('assoc');

    // Read rows through iteration.
    foreach ($rows as $row) {
        // Do work
    }

.. note::

    Reading rows through iteration will fetch rows in 'both' mode. This means
    you will get both the numerically indexed and associatively indexed results.


Getting Row Counts
------------------

After executing a statement, you can fetch the number of affected rows::

    $rowCount = count($stmt);
    $rowCount = $stmt->rowCount();


Checking Error Codes
--------------------

If your query was not successful, you can get related error information
using the ``errorCode()`` and ``errorInfo()`` methods. These methods work the
same way as the ones provided by PDO::

    $code = $stmt->errorCode();
    $info = $stmt->errorInfo();

.. todo::
Possibly document CallbackStatement and BufferedStatement

.. _database-query-logging:

Query Logging
=============

Query logging can be enabled when configuring your connection by setting the
``log`` option to ``true``. You can also toggle query logging at runtime, using
``logQueries``::

    // Turn query logging on.
    $conn->logQueries(true);

    // Turn query logging off
    $conn->logQueries(false);

When query logging is enabled, queries will be logged to
:php:class:`Cake\\Log\\Log` using the 'debug' level, and the 'queriesLog' scope.
You will need to have a logger configured to capture this level & scope. Logging
to ``stderr`` can be useful when working on unit tests, and logging to
files/syslog can be useful when working with web requests::

    use Cake\Log\Log;

    // Console logging
    Log::config('queries', [
        'className' => 'Console',
        'stream' => 'php://stderr',
        'scopes' => ['queriesLog']
    ]);

    // File logging
    Log::config('queries', [
        'className' => 'File',
        'path' => LOGS,
        'file' => 'queries.log',
        'scopes' => ['queriesLog']
    ]);

.. note::

    Query logging is only intended for debugging/development uses. You should
    never leave query logging on in production as it will negatively impact the
    performance of your application.

.. _identifier-quoting:

Identifier Quoting
==================

By default CakePHP does **not** quote identifiers in generated SQL queries. The
reason for this is identifier quoting has a few drawbacks:

* Performance overhead - Quoting identifiers is much slower and complex than not doing it.
* Not necessary in most cases - In non-legacy databases that follow CakePHP's
  conventions there is no reason to quote identifiers.

If you are using a legacy schema that requires identifier quoting you can enable
it using the ``quoteIdentifiers`` setting in your
:ref:`database-configuration`. You can also enable this feature at runtime::

    $conn->driver()->autoQuoting(true);

When enabled, identifier quoting will cause additional query traversal that
converts all identifiers into ``IdentifierExpression`` objects.

.. note::

    SQL snippets contained in QueryExpression objects will not be modified.

.. _database-metadata-cache:

Metadata Caching
================

CakePHP's ORM uses database reflection to determine the schema, indexes and
foreign keys your application contains. Because this metadata changes
infrequently and can be expensive to access, it is typically cached. By default,
metadata is stored in the ``_cake_model_`` cache configuration. You can define
a custom cache configuration using the ``cacheMetatdata`` option in your
datasource configuration::
>>>>>>> Stashed changes

    'Datasources' => [
        'default' => [
            // Other keys go here.

            // Use the 'orm_metadata' cache config for metadata.
            'cacheMetadata' => 'orm_metadata',
        ]
    ],

<<<<<<< Updated upstream
実行時に ``cacheMetadata()`` メソッドを使ってメタデータのキャッシュを
設定することもできます。::
=======
You can also configure the metadata caching at runtime with the
``cacheMetadata()`` method::
>>>>>>> Stashed changes

    // Disable the cache
    $connection->cacheMetadata(false);

    // Enable the cache
    $connection->cacheMetadata(true);

    // Use a custom cache config
    $connection->cacheMetadata('orm_metadata');
<<<<<<< Updated upstream

CakePHP にはメタデータキャッシュを管理するための CLI ツールも同梱しています。
詳細については :doc:`/console-and-shells/orm-cache` を参照してください。


.. meta::
    :title lang=ja: Database Basics
    :keywords lang=en: SQL,MySQL,MariaDB,PostGres,Postgres,postgres,PostgreSQL,PostGreSQL,postGreSql,select,insert,update,delete,statement,configuration,connection,database,data,types,custom,,executing,queries,transactions,prepared,statements,binding,fetching,row,count,error,codes,query,logging,identifier,quoting,metadata,caching
=======

CakePHP also includes a CLI tool for managing metadata caches. See the
:doc:`/console-and-shells/orm-cache` chapter for more information.
>>>>>>> Stashed changes
