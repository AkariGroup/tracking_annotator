# tracking_annotator

OAK-Dのtracking機能を使い、認識できなかったフレームを自動でYOLOアノテーションし、保存するアプリ

## 概要説明

![概要図](jpg/tracking_annotator.jpg "概要図")

OAK-Dのtracking機能には、認識していた物体がロストした場合でもその前のtracking情報を元に一定時間物体位置を予測、保持する機能があります。  
この機能を用い、認識→数フレームのロスト→再度認識、となった場合にロストしていたフレームの画像と、そのフレームのYOLOアノテーションファイルを保存します。  
保存する際には、LOSTした物体だけでなく他に認識していた物体のアノテーション情報も合わせて保存します。  
これにより、**認識モデルが認識できなかった画像のみ、自動的に仮アノテーションされた状態で収集することができます。**  
**あくまで予測位置に基づくアノテーションなので、手直しが必要な点、全ての認識失敗した画像を収集できる訳ではない点に注意してください。**  

## セットアップ
1. submoduleの更新  
`git submodule update --init`  

1. 仮想環境の作成  
`python3 -m venv venv`  
`. venv/bin/activate`  
`pip install -r requirements.txt`  

## 実行
`python3 tracking_annotator.py -m "OAK-Dモデルファイルのパス" -c "OAK-Dラベルファイルのパス"-p "画像を保存するディレクトリパス"`  

-m, -cを指定しない場合、YOLOv4のCOCOデータセットの学習モデルで起動します。  
独自学習モデルでの使用には、depthaiのオンラインモデルコンバータ(http://tools.luxonis.com/) で変換したYOLOのモデルファイル(.blob)とラベルファイル(.json)が必要です。  
詳しい学習モデルの作成方法は、下記のリンク先を参照ください。  
https://akarigroup.github.io/docs/source/dev/custom_object_detection/main.html
