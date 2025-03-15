---
title: 【0から始めるDB入門 Part0】SQLトライアル編
tags:
  - SQL
  - DB
  - 初心者
  - Database
private: false
updated_at: '2025-01-26T00:28:44+09:00'
id: ebd4971c6f2b6ccecdc7
organization_url_name: rits-rcc
slide: false
ignorePublish: false
---
# はじめに
これは[SQLab](https://sqlab.net/)さんの問題を解いていきながら，ステップバイステップでSQLについて学んでいこうと思います。

https://sqlab.net/

# トライアル編

## 1
- 問題  
    出版年(release_year)が不明の書籍一覧を取得してください。

<details><summary>解答・解説</summary>

- 解答
    ```sql
    SELECT * FROM books
        WHERE release_year IS NULL;
    ```
<br/>

- 解説  
    ```sql
    SELECT * FROM books
    ```
    `books`テーブルからすべての列を取得します。

    ```sql
        WHERE release_year IS NULL;
    ```
    `release_year`が`NULL`である行を条件として指定します。

</details>

:::note info
**ポイント**
- 条件検索は`WHERE`句を使います。
- `NULL`値の判定には`IS NULL`を使用します。
- `=`や`!=`では`NULL`値の比較ができないため注意が必要です。
:::

---

## 2
- 問題  
    書籍一覧をページ数が多い順に並び替えてください。  
    出力項目は`name`(書籍名)`total_page`(総ページ数)です。

<details><summary>解答・解説</summary>

- 解答
    ```sql
    SELECT name, total_page FROM books
        ORDER BY total_page DESC;
    ```
<br/>

- 解説  
    ```sql
    SELECT name, total_page FROM books
    ```
    `books`テーブルから`name`と`total_page`の列を取得します。

    ```sql
        ORDER BY total_page DESC;
    ```
    `total_page`を基準に降順（大きい順）で並び替えます。

</details>

:::note info
**ポイント**
- 特定の列を選択する際は`SELECT`句でカラム名を指定します。
- 並び替えには`ORDER BY`句を使用します。
- 降順に並び替える場合は`DESC`を指定します。昇順（小さい順）は`ASC`または省略可能です。
- ASC→ascending（昇順）、DESC→descending（降順）みたいですが、わたしはAdd（増えていく）とDecrease（減っていく）と覚えています。以下のものも覚えやすいと思います

:::

https://qiita.com/ryosuketter/items/eaaa66aa93a311635628

---

## 3
- 問題  
    書籍一覧をカテゴリー毎に集計して多い順に、カテゴリー名は昇順に並び替えてください。データの取得件数は先頭から3件のみにしてください。  
    出力項目は`name`(カテゴリー名)と`num`(書籍数)です。

<details><summary>解答・解説</summary>

- 解答
    ```sql
    SELECT cat.name, COUNT(book.name) AS num FROM categories AS cat
        INNER JOIN book_categories AS book_cat
            ON cat.id = book_cat.category_id
        INNER JOIN books AS book
            ON book_cat.book_id = book.id
        GROUP BY cat.name
        ORDER BY num DESC, cat.name ASC
        LIMIT 3;
    ```
<br/>

- 解説  
    ```sql
    SELECT cat.name, COUNT(book.name) AS num FROM categories AS cat
    ```
    - `categories`テーブルを`cat`と別名を付け、その`name`列と、`book.name`の数をカウントしたものを`num`として選択します。

    ```sql
        INNER JOIN book_categories AS book_cat
            ON cat.id = book_cat.category_id
    ```
    - `categories`テーブルと`book_categories`テーブルを`category_id`で内部結合します。`book_categories`テーブルを`book_cat`と別名を付けています。

    ```sql
        INNER JOIN books AS book
            ON book_cat.book_id = book.id
    ```
    - `book_categories`テーブルと`books`テーブルを`book_id`で内部結合します。`books`テーブルを`book`と別名を付けています。

    ```sql
        GROUP BY cat.name
    ```
    - `cat.name`でグループ化し、カテゴリーごとに集計します。

    ```sql
        ORDER BY num DESC, cat.name ASC
    ```
    - `num`を降順に、同じ`num`の場合は`cat.name`を昇順に並び替えます。

    ```sql
        LIMIT 3;
    ```
    - 先頭から3件のみ取得します。

</details>

:::note info
**ポイント**
- テーブルを結合する際には`JOIN`句を使用し、結合条件を`ON`で指定します。
- 別名（エイリアス）は`AS`を使って付けられます。
- 集計関数（例：`COUNT`）を使用する際には、`GROUP BY`句でグループ化します。
- 取得件数を制限するには`LIMIT`句を使用します。
:::

---

## 4
- 問題  
    idが1のデータを削除後、イベント一覧を取得してください。

<details><summary>解答・解説</summary>

- 解答
    ```sql
    DELETE FROM events
        WHERE id = 1;
    SELECT * FROM events;
    ```
<br/>

- 解説  
    ```sql
    DELETE FROM events
    ```
    - `events`テーブルからデータを削除します。

    ```sql
        WHERE id = 1;
    ```
    - `id`が1の行を削除対象として指定します。

    ```sql
    SELECT * FROM events;
    ```
    - `events`テーブルの全データを取得し、削除が正しく行われたか確認します。

</details>

:::note info
**ポイント**
- データを削除する際は`DELETE FROM`文を使用します。
- 削除条件は`WHERE`句で指定し、条件を明確にすることで誤ったデータ削除を防ぎます。
- データ操作後に結果を確認するために`SELECT`文を使います。
:::

---

# おわりに
今回はトライアル編の問題の解き，解説を行いました。これらの問題を通して、SQLの基本的な操作であるデータの取得、並び替え、集計、削除について学ぶことができました。

今後も引き続き、より高度なSQLの機能や実践的なクエリの書き方について学んでいく予定です。

---

# 次回Part2 SQL初級編を待て...
