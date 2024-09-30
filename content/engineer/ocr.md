---
title: "OCRのサンプルアプリケーション"
date: 2024-07-01T12:00:00
draft: false
---

# 概要
簡単なOCRアプリの実装を行います。様々なライブラリがあると思いますが、今回はTesseractを使用し実装してみます。デフォルトは英語のみですが、日本語の画像から日本語を抽出できるようにしたいと思います。

## Tesseractとは
Googleが主導して開発しているオープンソースのOCR（Optical Character Recognition、光学文字認識）エンジンです。OCRは、画像やPDFなどに含まれるテキスト情報を解析し、コンピュータが扱える文字データに変換する技術です。Tesseractは、その中でも高精度なテキスト認識を行うことができるツールとして広く利用されています。

### 主な特徴
- オープンソース: 無料で使用でき、カスタマイズも可能です。
- マルチプラットフォーム対応: Linux、Windows、macOSなど、さまざまなOSで動作します。
- 多言語対応: 100以上の言語データがサポートされており、日本語を含む多言語でのテキスト認識が可能です。
- 高精度: 特に印刷されたテキストの認識において非常に高い精度を誇ります。手書き文字にも対応していますが、精度は印刷文字ほど高くありません。
- 拡張性: 画像前処理や言語モデルのカスタマイズなど、OCR精度を向上させるための多くのオプションがあります。

# 環境
- Mac OS
- Python 3.11.9

# 1. 準備
## tesseractのインストール
```
brew install tesseract
```
## 多言語データのインストール
```
brew install tesseract-lang
```

## Pythonライブラリのインストール
```
pip3 install pytesseract Pillow
```

## 画像の用意
下記のように画像を用意する
ocr/
├── test.png
└── main.py

![テスト画像](/kei-ta-blog-go/test.jpg)

## main.py
```py
import os
import pytesseract
from PIL import Image

os.environ['TESSDATA_PREFIX'] = '/opt/homebrew/share/tessdata/'

# 画像ファイルのパスを指定
image_path = './test.png'

# 画像を読み込む
img = Image.open(image_path)

# OCRを日本語で実行
text = pytesseract.image_to_string(img, lang='jpn')

# 結果を表示
print(text)
```

# 2. 実行
```
python3 main.py
```
## 出力結果
```
コーヒーの豆知識

コーヒーの花は白い。コーヒーの実は赤い。
たとえば、そんなこともコーヒータイムを楽しくするエッセンス。
身体にいいワケ、もっとおいしく飲むためのマナー、知ることもまた、コーヒーをもっと豊かにする秘訣。
```
文字の大きさに関わらず一言一句完璧に読み取れてることがわかる。

# 3. 所管
今回は簡単な画像でOCRをし、問題なく読み取れてることがわかった。興味本位で行ったが、業務などで活かせそうなら改良してどんどん使っていきたい。