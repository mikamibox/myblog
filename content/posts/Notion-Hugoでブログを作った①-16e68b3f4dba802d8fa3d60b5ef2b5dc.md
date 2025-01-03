---
title: "Notion-Hugoでブログを作った①"
date: "2025-01-01T07:18:00.000Z"
lastmod: "2025-01-02T09:24:00.000Z"
draft: true
series: []
authors:
  - "三上五月"
tags:
  - "CSS"
  - "HTML"
  - "Javascript"
  - "Node.js"
  - "Hugo"
  - "GitHub"
categories:
  - "Tips"
NOTION_METADATA:
  object: "page"
  id: "16e68b3f-4dba-802d-8fa3-d60b5ef2b5dc"
  created_time: "2025-01-01T07:18:00.000Z"
  last_edited_time: "2025-01-02T09:24:00.000Z"
  created_by:
    object: "user"
    id: "145d872b-594c-8199-9dd5-00029abc4c01"
  last_edited_by:
    object: "user"
    id: "145d872b-594c-8199-9dd5-00029abc4c01"
  cover: null
  icon: null
  parent:
    type: "database_id"
    database_id: "16c68b3f-4dba-81c0-87d8-db446c050d07"
  archived: false
  in_trash: false
  properties:
    series:
      id: "B%3C%3FS"
      type: "multi_select"
      multi_select: []
    draft:
      id: "JiWU"
      type: "checkbox"
      checkbox: true
    authors:
      id: "bK%3B%5B"
      type: "people"
      people:
        - object: "user"
          id: "145d872b-594c-8199-9dd5-00029abc4c01"
          name: "三上五月"
          avatar_url: "https://s3-us-west-2.amazonaws.com/public.notion-static.com/aec83c\
            0e-33e9-43fa-84d1-11a53e904aa5/user.png"
          type: "person"
          person:
            email: "kamemame.0515@gmail.com"
    custom-front-matter:
      id: "c~kA"
      type: "rich_text"
      rich_text: []
    tags:
      id: "jw%7CC"
      type: "multi_select"
      multi_select:
        - id: "2a3f5c1f-7046-4114-b81c-56205ffad525"
          name: "CSS"
          color: "blue"
        - id: "0c1693f1-186a-47c9-86d4-e5b3369da62f"
          name: "HTML"
          color: "orange"
        - id: "e30485aa-08ee-4ce8-9812-482ff4a56c2c"
          name: "Javascript"
          color: "yellow"
        - id: "4b5d7f11-1a54-4078-863e-ada5dd6220a3"
          name: "Node.js"
          color: "green"
        - id: "c3e8c3f9-2723-4fbc-a4d5-aed80ab9a3bf"
          name: "Hugo"
          color: "blue"
        - id: "9e4518d7-07b3-413c-9399-5d0196b31d6e"
          name: "GitHub"
          color: "default"
    categories:
      id: "nbY%3F"
      type: "multi_select"
      multi_select:
        - id: "96517a7f-e8a6-44a0-9d1d-8ce7fb058936"
          name: "Tips"
          color: "red"
    Last edited time:
      id: "vbGE"
      type: "created_time"
      created_time: "2025-01-01T07:18:00.000Z"
    summary:
      id: "x%3AlD"
      type: "rich_text"
      rich_text: []
    Name:
      id: "title"
      type: "title"
      title:
        - type: "text"
          text:
            content: "Notion-Hugoでブログを作った①"
            link: null
          annotations:
            bold: false
            italic: false
            strikethrough: false
            underline: false
            code: false
            color: "default"
          plain_text: "Notion-Hugoでブログを作った①"
          href: null
  url: "https://www.notion.so/Notion-Hugo-16e68b3f4dba802d8fa3d60b5ef2b5dc"
  public_url: "https://tropical-kitchen-d64.notion.site/Notion-Hugo-16e68b3f4dba8\
    02d8fa3d60b5ef2b5dc"
MANAGED_BY_NOTION_HUGO: true

---


## はじめに


Hugoでブログを書こう！と思ったきっかけがこの記事だったのですが、


[https://blog.code-del.com/posts/notion-hugo%E3%81%A7%E5%AF%9D%E8%BB%A2%E3%81%B3%E3%81%AA%E3%81%8C%E3%82%89%E3%83%96%E3%83%AD%E3%82%B0%E3%82%92%E6%9B%B8%E3%81%8F/](https://blog.code-del.com/posts/notion-hugo%E3%81%A7%E5%AF%9D%E8%BB%A2%E3%81%B3%E3%81%AA%E3%81%8C%E3%82%89%E3%83%96%E3%83%AD%E3%82%B0%E3%82%92%E6%9B%B8%E3%81%8F/)


書いてあることが全然理解できなかったため、まずHugoに慣れようと思いました。

そのため、最初にHugoでブログを作ったときの手順は

1. ローカルで環境構築
1. Notionに書いた記事をマークダウン式でエクスポート
1. VSCodeで整形
1. ``hugo`` コマンドで出力
1. FTPソフトでまとめてサーバーにアップロード

という手順を踏んでいました。なんという面倒くささ。しかもここまでたどり着くまでに一ヶ月かかってます。**Hugo、全然簡単じゃねぇ。**


テーマフォルダ内のcontentsフォルダとレイアウトフォルダ入れないとダメ


go.modも


画像も


yamlとtomlの違い


外部リンク設定


custom.css　最悪テーマのcssをいじる

