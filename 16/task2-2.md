# データ操作言語・DML
  DML(Data Manipulation Language)とは、データの格納や取り出し、更新、削除などの命令の総称です。

DMLの例には以下のようなものがあります。

SELECT
INSERT
UPDATE
DELETE
EXPLAIN
LOCK TABLE
データベース内のテーブルへ行う操作ですね。

テーブルの中のデータを取得したり、削除したりという感じ。


# トランザクション制御言語・TCL
  TCL(Transaction Control Language)とは、トランザクションの開始や終了の命令の総称です。

TCLの例には以下のようなものがあります。

COMMIT
ROLLBACK
SET TRANSACTION
SAVEPOINT
TCLも同じく、データベース内のテーブル操作を支持する命令です。

一部のDBMS製品などでは、BEGIN・COMMIT・ROLLBACKは、DCLに分類される場合もあります。


# データ定義言語・DDL
  DDL(Data Definition Language)とは、テーブルなどの作成や削除、各種設定など命令の総称です。

DDLには以下のようなものがあります。

CREATE
ALTER
DROP
TRUNCATE
データベース内のテーブル自体への命令ですね。

テーブルそのものを作ったり、削除したりという感じです。

# データ制御言語・DCL
  DCL(Data Control Language)とは、DMLやDDLの利用に関する許可や禁止を設定する命令の総称です。

DCLには以下のようなものがあります。

GRANT
REVOKE
DCLは誰にどのようなデータ・テーブルを操作させるかなどの権限を設定する命令です。

ユーザーAはテーブルBを操作してもよい、などの許可を与えたりします。

https://kirohi.com/sql_4_languages