---
title: "WebP画像とサムネイルを一括で生成"
date: "2024-12-30T12:27:00.000Z"
lastmod: "2025-01-01T07:51:00.000Z"
draft: false
series: []
authors:
  - "三上五月"
tags:
  - "Javascript"
  - "Node.js"
categories:
  - "Tool"
summary: "Node.js の「sharp」を使った画像変換スクリプトを作成しました。このスクリプトでは、フォルダ内の画像を一括で WebP
  形式に変換したり、指定サイズへのリサイズやサムネイルの生成も簡単に行えます。"
NOTION_METADATA:
  object: "page"
  id: "16c68b3f-4dba-807d-bb69-d5e2fc4eb324"
  created_time: "2024-12-30T12:27:00.000Z"
  last_edited_time: "2025-01-01T07:51:00.000Z"
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
        - id: "e30485aa-08ee-4ce8-9812-482ff4a56c2c"
          name: "Javascript"
          color: "yellow"
        - id: "4b5d7f11-1a54-4078-863e-ada5dd6220a3"
          name: "Node.js"
          color: "green"
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
      created_time: "2024-12-30T12:27:00.000Z"
    summary:
      id: "x%3AlD"
      type: "rich_text"
      rich_text:
        - type: "text"
          text:
            content: "Node.js の「sharp」を使った画像変換スクリプトを作成しました。このスクリプトでは、フォルダ内の画像を一括で WebP
              形式に変換したり、指定サイズへのリサイズやサムネイルの生成も簡単に行えます。"
            link: null
          annotations:
            bold: false
            italic: false
            strikethrough: false
            underline: false
            code: false
            color: "default"
          plain_text: "Node.js の「sharp」を使った画像変換スクリプトを作成しました。このスクリプトでは、フォルダ内の画像を一括で WebP
            形式に変換したり、指定サイズへのリサイズやサムネイルの生成も簡単に行えます。"
          href: null
    Name:
      id: "title"
      type: "title"
      title:
        - type: "text"
          text:
            content: "WebP画像とサムネイルを一括で生成"
            link: null
          annotations:
            bold: false
            italic: false
            strikethrough: false
            underline: false
            code: false
            color: "default"
          plain_text: "WebP画像とサムネイルを一括で生成"
          href: null
  url: "https://www.notion.so/WebP-16c68b3f4dba807dbb69d5e2fc4eb324"
  public_url: "https://tropical-kitchen-d64.notion.site/WebP-16c68b3f4dba807dbb69\
    d5e2fc4eb324"
MANAGED_BY_NOTION_HUGO: true

---


## webp 変換スクリプト


参考リンク：[【Node.js】sharp でサクッと「AVIF」「WebP」生成 - Qiita](https://qiita.com/taqumo/items/60de0af9699415150035)


この記事を参考にし環境構築し、AI に聞いて自分好みにカスタマイズしたスクリプトを作った。
src フォルダに入れた png 画像が dest フォルダに webp 変換されて出力される。


```javascript
import c from 'ansi-colors';
import log from 'fancy-log';
import fs from 'fs';
import globule from 'globule';
import sharp from 'sharp';

class ImageFormatConverter {
  constructor(options = {}) {
    this.srcBase = options.srcBase || 'src';
    this.destBase = options.destBase || 'dest';
    this.includeExtensionName = options.includeExtensionName || false;
    this.formats = options.formats || [
      {
        type: 'webp',
        quality: 80,
      },
    ];
    this.srcImages = `${this.srcBase}/**/*.{jpg,jpeg,png}`;
    this.init();
  }

  init = async () => {
    const imagePathList = this.findImagePaths();
    await this.convertImages(imagePathList);
  };

  /**
   * globパターンで指定した画像パスを配列化して返す
   * @return { array } 画像パスの配列
   */
  findImagePaths = () => {
    return globule.find({
      src: [this.srcImages],
    });
  };

  /**
   * 画像を変換する
   * @param { string } imagePath 画像パス
   * @param { object } format 画像形式と圧縮品質
   */
  convertImageFormat = async (imagePath, format) => {
    const reg = /\\/(.*)\\.(jpe?g|png)$/i;
    const [, imageName, imageExtension] = imagePath.match(reg);
    const imageFileName = this.includeExtensionName ? `${imageName}.${imageExtension}` : imageName;
    const destPath = `${this.destBase}/${imageFileName}.${format.type}`;
    await sharp(imagePath)
      .toFormat(format.type, { quality: format.quality })
      .toFile(destPath)
      .then((info) => {
        log(`Converted ${c.blue(imagePath)} to ${c.yellow(format.type.toUpperCase())} ${c.green(destPath)}`);
      })
      .catch((err) => {
        log(c.red(`Error converting image to ${c.yellow(format.type.toUpperCase())}\\n${err}`));
      });
  };

  /**
   * 配列内の画像パスのファイルを変換する
   * @param { array } imagePathList 画像パスの配列
   */
  convertImages = async (imagePathList) => {
    if (imagePathList.length === 0) {
      log(c.red('No images found to convert'));
      return;
    }
    for (const imagePath of imagePathList) {
      const reg = new RegExp(`^${this.srcBase}/(.*/)?`);
      const path = imagePath.match(reg)[1] || '';
      const destDir = `${this.destBase}/${path}`;
      if (!fs.existsSync(destDir)) {
        try {
          fs.mkdirSync(destDir, { recursive: true });
          log(`Created directory ${c.green(destDir)}`);
        } catch (err) {
          log(`Failed to create directory ${c.green(destDir)}\\n${err}`);
        }
      }
      const conversionPromises = this.formats.map((format) => this.convertImageFormat(imagePath, format));
      await Promise.all(conversionPromises);
    }
  };
}
const imageFormatConverter = new ImageFormatConverter();

```


## リサイズとサムネイル生成を同時に行う


AI に聞いたら出てきたこのスクリプトを `imageProcessor.js` という名前で同じフォルダに保存した。


```javascript
import c from 'ansi-colors';
import log from 'fancy-log';
import fs from 'fs';
import path from 'path';
import globule from 'globule';
import sharp from 'sharp';

class ImageProcessor {
  constructor(options = {}) {
    this.srcBase = options.srcBase || 'src';
    this.destBase = 'dest';
    this.includeExtensionName = options.includeExtensionName || false;
    this.formats = options.formats || [
      {
        type: 'webp',
        quality: 80,
      },
    ];
    this.miniFolder = 'mini';
    this.srcImages = `${this.srcBase}/**/*.{jpg,jpeg,png,webp,gif}`;
    this.mainWidth = 800;
    this.miniWidth = 120;
    this.init();
  }

  init = async () => {
    const imagePathList = this.findImagePaths();
    await this.processImages(imagePathList);
  };

  findImagePaths = () => {
    return globule.find({
      src: [this.srcImages],
    });
  };

  convertImageFormat = async (imagePath, format) => {
    const reg = /\\/(.*)\\.(jpe?g|png|webp|gif)$/i;
    const [, imageName, imageExtension] = imagePath.match(reg);
    const imageFileName = this.includeExtensionName ? `${imageName}.${imageExtension}` : imageName;
    const destPath = `${this.destBase}/${imageFileName}.${format.type}`;

    try {
      let sharpOptions = {};
      if (imageExtension.toLowerCase() === 'gif') {
        sharpOptions.pages = 1;
      }

      // メインの画像を800pxで出力
      await sharp(imagePath, sharpOptions)
        .resize({
          width: this.mainWidth,
          withoutEnlargement: true,
        })
        .toFormat(format.type, { quality: format.quality })
        .toFile(destPath);

      log(`Converted ${c.blue(imagePath)} to ${c.yellow(format.type.toUpperCase())} ${c.green(destPath)}`);

      // WebPの場合、ミニバージョン(120px)も作成
      if (format.type === 'webp') {
        await this.createMiniVersion(imagePath, imageFileName);
      }
    } catch (err) {
      log(c.red(`Error converting image to ${c.yellow(format.type.toUpperCase())}\\n${err}`));
    }
  };

  createMiniVersion = async (imagePath, imageFileName) => {
    const miniDestPath = path.join(this.destBase, this.miniFolder, `${imageFileName}.webp`);

    try {
      fs.mkdirSync(path.dirname(miniDestPath), { recursive: true });
      await sharp(imagePath)
        .resize({
          width: this.miniWidth,
          withoutEnlargement: true,
        })
        .toFormat('webp', { quality: 80 })
        .toFile(miniDestPath);

      log(`Created mini version: ${c.green(miniDestPath)}`);
    } catch (err) {
      log(c.red(`Error creating mini version\\n${err}`));
    }
  };

  processImages = async (imagePathList) => {
    if (imagePathList.length === 0) {
      log(c.red('No images found to process'));
      return;
    }

    for (const imagePath of imagePathList) {
      const reg = new RegExp(`^${this.srcBase}/(.*/)?`);
      const path = imagePath.match(reg)[1] || '';
      const destDir = `${this.destBase}/${path}`;

      if (!fs.existsSync(destDir)) {
        try {
          fs.mkdirSync(destDir, { recursive: true });
          log(`Created directory ${c.green(destDir)}`);
        } catch (err) {
          log(`Failed to create directory ${c.green(destDir)}\\n${err}`);
        }
      }

      const conversionPromises = this.formats.map((format) => this.convertImageFormat(imagePath, format));
      await Promise.all(conversionPromises);
    }
  };
}

const imageProcessor = new ImageProcessor();

```


### **package.json の編集**


`package.json` の `"scripts"` 内に `"imageProcessor": "node imageProcessor.js"` を追加する。


```json
{
  "name": "image-format-converter",
  "version": "1.0.0",
  "license": "UNLICENSED",
  "private": true,
  "scripts": {
    "image-format-converter": "node ./image-format-converter.js",
    "imageProcessor": "node imageProcessor.js"
  },
  "type": "module",
  "devDependencies": {
    "ansi-colors": "^4.1.3",
    "fancy-log": "^2.0.0",
    "globule": "^1.3.4",
    "sharp": "^0.33.5"
  }
}

```


## バッチファイルの作成


フォルダの上に来やすいように `!imageProcessor.bat` という名前で保存した。


```powershell
@echo off
npm run imageProcessor
pause

```


## スクリプトを実行


`!imageProcessor.bat` をダブルクリックするとコマンドプロンプトが開き画像が変換される。PhotoSwipe 用にサムネイルの比率を変更していないが、たぶん 100x100 とかに設定する方法もあると思う。


`imageProcessor.js` 内の `this.mainWidth = 800;` の部分の数値を変えれば、横幅 500px とかにもできると思う。簡単ならくがきとかは 500px とか 300px で載せてるのでその都度変更している。

