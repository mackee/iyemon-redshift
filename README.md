# README.md

## 概要

fluentdでRedshiftに入れた行動ログを閲覧するためのツールです。

行動ログについては、こちらを参照すること。

http://hisaichi5518.hatenablog.jp/entry/2014/07/27/120322

## インストール

```
cpanm --installdeps .
cp config/common.sample.pl config/common.pl
$EDITOR config/common.pl # and add redshift config.
plackup -a app.psgi -p 50004
```

## テーブル構造

テーブルがない場合、Redshiftにつないで以下のようなテーブルを作成する。

```perl
handler->dbh->do(<<"...");
    CREATE TABLE action_logs (
    uid INTEGER NOT NULL DEFAULT 0,
    time INTEGER NOT NULL SORTKEY,
    type varchar(max),
    json varchar(max)
  );
...
```


## テスト用のデータ

テスト用のデータを挿入したい場合は、以下のようにする。

```perl
INSERT INTO action_logs (uid, time, type, json) VALUES (12, 1405555200, 'test.test.test', '{"test": "ほげほげ"}';
```

## LICENSE

Copyright (C) hisaichi5518.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

## AUTHOR

hisaichi5518 E<lt>hisaichi5518@gmail.comE<gt>
