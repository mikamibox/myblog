---
title: "手打ちサイトでRSS対応の更新履歴作った"
date: "2024-12-30T12:03:00.000Z"
lastmod: "2025-01-08T07:54:00.000Z"
draft: false
series: []
authors:
  - "三上五月"
tags:
  - "CSS"
  - "HTML"
  - "Javascript"
  - "python"
categories:
  - "Tool"
summary: "RSSフィードを導入して自サイトの更新履歴を自動化。AIを活用し、jQueryやPythonスクリプトで効率的な作業環境を構築しました。更\
  新内容を簡単に反映できる仕組みを解説しています。"
NOTION_METADATA:
  object: "page"
  id: "16c68b3f-4dba-80fc-8c70-d33ebdf620fa"
  created_time: "2024-12-30T12:03:00.000Z"
  last_edited_time: "2025-01-08T07:54:00.000Z"
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
      checkbox: false
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
        - id: "8afe8bd4-4395-4f86-bce0-c2512047d3b5"
          name: "python"
          color: "yellow"
    categories:
      id: "nbY%3F"
      type: "multi_select"
      multi_select:
        - id: "bda43e76-13da-4025-8607-4343ad835e46"
          name: "Tool"
          color: "green"
    Last edited time:
      id: "vbGE"
      type: "created_time"
      created_time: "2024-12-30T12:03:00.000Z"
    summary:
      id: "x%3AlD"
      type: "rich_text"
      rich_text:
        - type: "text"
          text:
            content: "RSSフィードを導入して自サイトの更新履歴を自動化。AIを活用し、jQueryやPythonスクリプトで効率的な作業環境を構築しました。更\
              新内容を簡単に反映できる仕組みを解説しています。"
            link: null
          annotations:
            bold: false
            italic: false
            strikethrough: false
            underline: false
            code: false
            color: "default"
          plain_text: "RSSフィードを導入して自サイトの更新履歴を自動化。AIを活用し、jQueryやPythonスクリプトで効率的な作業環境を構築しまし\
            た。更新内容を簡単に反映できる仕組みを解説しています。"
          href: null
    Name:
      id: "title"
      type: "title"
      title:
        - type: "text"
          text:
            content: "手打ちサイトでRSS対応の更新履歴作った"
            link: null
          annotations:
            bold: false
            italic: false
            strikethrough: false
            underline: false
            code: false
            color: "default"
          plain_text: "手打ちサイトでRSS対応の更新履歴作った"
          href: null
  url: "https://www.notion.so/RSS-16c68b3f4dba80fc8c70d33ebdf620fa"
  public_url: "https://tropical-kitchen-d64.notion.site/RSS-16c68b3f4dba80fc8c70d\
    33ebdf620fa"
MANAGED_BY_NOTION_HUGO: true

---


## はじめに


ほかの個人サイト運営してある方々の更新をてがろぐの RSS で把握しているので自サイトの更新履歴にも対応できないかな～と思った。
[ChatGPT](https://chatgpt.com/)と[Claude](https://claude.ai/)にめちゃくちゃ頼った。


## RSS の土台を用意して rss.xml で保存


RSS の基本コードはこんな感じ。


```xml
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0">
  <channel>
    <title>サイト名</title>
    <link>サイトアドレス</link>
    <description>サイト名：更新情報</description>
    <language>ja</language>
    <item>
      <title>更新内容</title>
      <pubDate>Wed, 20 Nov 2024 21:25:04 +0900</pubDate>
      <enclosure url="自サイトのOGP画像" type="image/png"/>
      <link>サイトアドレス</link>
    </item>
    <item>
      <title>更新内容</title>
      <pubDate>Wed, 19 Nov 2024 21:25:04 +0900</pubDate>
      <enclosure url="自サイトのOGP画像" type="image/png"/>
      <link>サイトアドレス</link>
    </item>
    <item>
      <title>更新内容</title>
      <pubDate>Wed, 18 Nov 2024 21:25:04 +0900</pubDate>
      <enclosure url="自サイトのOGP画像" type="image/png"/>
      <link>サイトアドレス</link>
    </item>
  </channel>
</rss>
```


## AI に質問する


index ページ に RSS を埋め込みたかったので方法をググった。
php と jQuery を使う方法があるらしい。
jQuery を丁度使ってたので jQuery の方を採用。
質問した内容は以下のような感じ。


```text
同じ階層にある `rss.xml` の最新 3 件を `index.html` に jQuery を使って表示したいです。

現在、更新履歴の HTML は以下の形式です：
<section class="white-1">
 <h2 class="news">Update</h2>
  <dl class="news">
    <dt>2024.11.18</dt>
    <dd>更新内容</dd>
  </dl>
    <dl class="news">
    <dt>2024.09.11</dt>
    <dd>更新内容</dd>
  </dl>
    <dl class="news">
    <dt>2024.08.13</dt>
    <dd>更新内容</dd>
  </dl>
</section>


`rss.xml` の内容は以下です：
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0">
  <channel>
    <title>サイト名</title>
    <link>サイトアドレス</link>
    <description>サイト名：更新情報</description>
    <language>ja</language>
    <item>
      <title>更新内容</title>
      <pubDate>Wed, 20 Nov 2024 21:25:04 +0900</pubDate>
      <enclosure url="自サイトのOGP画像" type="image/png"/>
      <link>サイトアドレス</link>
    </item>
    <item>
      <title>更新内容</title>
      <pubDate>Wed, 19 Nov 2024 21:25:04 +0900</pubDate>
      <enclosure url="自サイトのOGP画像" type="image/png"/>
      <link>サイトアドレス</link>
    </item>
    <item>
      <title>更新内容</title>
      <pubDate>Wed, 18 Nov 2024 21:25:04 +0900</pubDate>
      <enclosure url="自サイトのOGP画像" type="image/png"/>
      <link>サイトアドレス</link>
    </item>
  </channel>
</rss>


jQuery を使った実装例を教えていただけますか？
```


**※HTML はうちのサイトで使ってるやつ。自作かテンプレートかで全然違うので注意。**


AI が出力したコードを `rss.js` で保存。


## index.html の</body>前に jQuery と rss.js を設置する


```html
<script src="<https://ajax.googleapis.com/ajax/libs/jquery/3.6.3/jquery.min.js>"></script>
<script src="assets/js/rss.js"></script>
</body>

```


うちは[do](https://do.gt-gt.org/)様作成プログラムのいいねボタン改とコイブミをすでに設置していたので、設置マニュアルに載ってた jQuery の CDN を読み込んだ。
`rss.js` はパスに注意。うちは `assets` フォルダに `js` フォルダ作ってたのでこんなパスになった。


## CSS の高さを AI に計算してもらう


読み込み中は内容が表示されずレイアウト崩れが起きるので、更新履歴セクションの高さを AI に計算してもらう。


```text
## 質問内容

安価なサーバーを使用しており、RSS フィードの読み込みに時間がかかります。
そのため、HTML の読み込み前後で`<section>`の高さが不安定になります。
以下のコードを元に、CSS で適切な高さを設定したいです。
読み込み後の`<section>`の高さを計算して具体的な rem 単位を教えてください。

読み込み前の HTML：
エディタに書いてる更新履歴のコードを載せる

読み込み後の HTML：
自分のサイトの更新履歴の部分ソースコードを見てそれをコピペ

css：
大元の body と、更新履歴で使ってる CSS をコピペ

```


AI が計算した数値を CSS に追加した。
これでサイトデザインが崩れなくなった。


## 動作確認


サイトに `test` フォルダ作って、画像以外のサイト構成ファイルアップロード。アドレス末尾に /test/index.html 記入してテストサイトを確認する。表示がおかしかったりエラーが出たりしたら AI に聞いて適宜修正してもらう。


動作したら完成。
更新するたびに `rss.xml` の`<item>~</item>`を足していけば自動で表示が変わっていく。更新履歴を書いたついでに RSS 発信もできる。一石二鳥だ。


---


## 【発展編】コードを楽に作成するプログラムを作った


毎回日時確認するの大変なので、そこを自動化できるプログラムが欲しくなったので AI に作成してもらった。


仕組み：`rss.xml` 同じフォルダに 更新内容を入力した `update.txt` を作って、一行の更新内容を書き、その内容を `rss.xml` 内に `<item>` として新規追加、ついでに日時も入力してもらう
（このへんのアイデアはじぇねろぐに影響を受けている）


Python が必要なので、コマンドプロンプトが怖くて使えないとか、Python をインストールしたくない人は回れ右。インストール方法はググれ。ちなみに私は Python のことを何も理解していない。どんなソフトなのかとかも分かってない。AI に言われたからやった。AI の奴隷だ。


AI に色々質問して出来た py ファイルはこちら。`rss.py` で保存する。


```python
import xml.etree.ElementTree as ET
from datetime import datetime
import xml.dom.minidom
import re

def prettify_xml(xml_string):
    """XMLを整形して返す"""
    # minidomを使用して整形
    dom = xml.dom.minidom.parseString(xml_string)
    pretty_xml = dom.toprettyxml(indent='  ', encoding='utf-8').decode('utf-8')
    
    # 空行を削除
    lines = pretty_xml.split('\n')
    # 空白行や空白文字のみの行を除去
    cleaned_lines = [line for line in lines if line.strip()]
    # 最初の行（XML宣言）を除去（後で追加するため）
    cleaned_lines = cleaned_lines[1:]
    
    # 行を結合して返す
    return '\n'.join(cleaned_lines)

def insert_updates_to_rss(rss_file_path, update_file_path):
    try:
        # 既存のXMLファイルを文字列として読み込む
        with open(rss_file_path, 'r', encoding='utf-8') as f:
            xml_content = f.read()
        
        # XMLパーサーを作成
        parser = ET.XMLParser(encoding='utf-8')
        tree = ET.fromstring(xml_content, parser=parser)
        
        # channelタグを見つける
        channel = tree.find('channel')
        if channel is None:
            raise ValueError("Channel element not found in RSS")
        
        # update.txtから更新情報を読み込む
        with open(update_file_path, 'r', encoding='utf-8') as f:
            updates = f.readlines()
        
        # 現在時刻をRFC822フォーマットで取得
        current_time = datetime.now().strftime('%a, %d %b %Y %H:%M:%S +0900')
        
        # channelの既存の要素を取得
        existing_items = channel.findall('item')
        
        # 既存のitem要素を一時的に削除
        for item in existing_items:
            channel.remove(item)
        
        # 新しいitem要素を追加
        for update in updates:
            update = update.strip()
            if update:
                item = ET.SubElement(channel, 'item')
                
                title = ET.SubElement(item, 'title')
                title.text = update
                
                pubdate = ET.SubElement(item, 'pubDate')
                pubdate.text = current_time
                
                enclosure = ET.SubElement(item, 'enclosure')
                enclosure.set('url', 'https://mikamibox.com/img/OGP.png')
                enclosure.set('length', '0')
                enclosure.set('type', 'image/png')
                
                link = ET.SubElement(item, 'link')
                link.text = 'https://mikamibox.com/'
        
        # 既存のitem要素を元の位置に戻す
        for item in existing_items:
            channel.append(item)
        
        # XMLツリーを文字列に変換して整形
        rough_string = ET.tostring(tree, encoding='utf-8')
        pretty_xml = prettify_xml(rough_string)
        
        # 整形済みXMLを保存
        with open(rss_file_path, 'w', encoding='utf-8') as f:
            f.write('<?xml version="1.0" encoding="utf-8"?>\n')
            f.write(pretty_xml)
            
        print("RSS file has been successfully updated!")
        
    except Exception as e:
        print(f"Error occurred: {e}")

# プログラムの実行
if __name__ == '__main__':
    rss_file_path = 'rss.xml'
    update_file_path = 'update.txt'
    insert_updates_to_rss(rss_file_path, update_file_path)
```


このコードができるようなプロンプトを逆算してもらった。この内容を自分の要望に合わせてカスタマイズして質問してみるといいのかもしれない。（試してない）


```text
RSSフィードを更新するPythonスクリプトを作成してください。以下の要件を満たすものが必要です：

1. 既存のRSS XMLファイルを読み込み、新しい更新情報をチャンネルの最上部に追加する
2. 更新情報は別のテキストファイル（update.txt）から読み込む
3. 各更新項目に対して以下の要素を含める：
   - タイトル（更新テキストそのもの）
   - 公開日時（現在時刻、RFC822フォーマット）
   - エンクロージャー（OGP画像のURL）
   - リンク（ウェブサイトURL）
4. XMLの整形機能を含める（インデント付きの読みやすいフォーマット）
5. 既存の項目は保持したまま、新しい項目を追加する
6. エラーハンドリングを実装する

コードは完全に機能する形で、必要なすべてのインポートと関数を含めて提供してください。また、XMLの整形のための補助関数も含めてください。
```


## プログラムを動かすバッチファイルを作成する（Win のみ）


新しいテキストファイルを作って、以下の内容をコピペして `rss.bat` という名前を付けて保存。


```text
@echo off
python rss.py
pause
```


これからは `update.txt` に更新内容を書いて、`rss.bat` をダブルクリックし、コマンドプロンプトを閉じ、`rss.xml` を確認して FTP ソフトでアップロードするだけで `index.html` をいじらずとも、更新履歴と RSS が自動で作成されるぞ！やったー！


…意外と面倒くさいな。面倒くさいとか言ってたら静的サイトベタ打ちしません。そりゃそうじゃ。

