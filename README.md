# HLS-sample-with-AWS-S3
AWS S3によるHLS サンプル

## 使用するサービス

- Amazon S3
- Amazon Elastic Transcoder

## 手順

1. 変換対象のMP4ファイルを用意する。
2. S3に変換元動画、変換後動画を配置するためのディレクトリを作成する。  
今回は下記。
- s3://ittimfn-public/HLS/upload/
  - 変換元のファイルを配置する
- s3://ittimfn-public/HLS/transcoded/
  - 変換後のファイルの出力先
3. ファイルアップロード用ディレクトリに変換対象のMP4を配置する。
4. AWSマネジメントコンソールからElastic Transcoderへ遷移する。
5. 「Create New Pipeline」ボタンを押下。
6. 各項目を入力し、画面下部の「Create Pipeline」ボタンを押下する。
  - Create New Pipeline
    - Pipeline Name : 任意のPipeline名
    - Input Bucket : 変換元ファイルを配置するS3バケット
    - IAM Role : 変換権限。（デフォルトでOK。）
  - Configuration for Amazon S3 Bucket for Transcoded Files and Playlists
    - Bucket : 出力先のS3バケット
    - Storage Class : バケットのclass。（Standardでいいはず…）
  - Configuration for Amazon S3 Bucket for Thumbnails
    - Bucket : Create New Pipelineと同値。（詳細未確認。サムネイル画像の入力バケット？） 
    - Storage Class : バケットのclass。（Standardでいいはず…）
7. 「Create New Job」ボタンを押下し、Jobの作成画面に遷移する。
8. 下記値を入力し、画面下部の「Create New Job」ボタンを押下。
  - Create a New Transcoding Job
    - Pipeline : 手順6で作成したPipeline
    - Output Key Prefix : 出力先ディレクトリを指定。
  - Input Details (1 of 1)
    - Input Key : 変換元ファイル
    - Decryption Parameters : デフォルトでOK。（詳細未確認）
    - Available Settings : デフォルトでOK。（詳細未確認）
  - Output Details (1 of 1)
    - Preset : System preset: HLS Video - 1M （詳細未確認。「HLS Video」を選択すればいいはず…）
    - Segment Duration : 動画を何秒ごとに分割するか
    - Output Key : 出力ファイル名
    - 以降のメニューについてはデフォルトで実行。（詳細未確認。）
9. 下記に変換されたファイルが出力される。
  - バケット
    - 手順6の「Configuration for Amazon S3 Bucket for Transcoded Files and Playlists - Bucket」で指定したバケット
  - ディレクトリ
    - 手順8の「Create a New Transcoding Job - Output Key Prefix」で指定したディレクトリ
  - ファイル名
    - 手順8の「Output Details (1 of 1) - Output Key」で指定したファイル名

## 参考

- [Qiita:AWS S3だけでHLSの原理試作](https://qiita.com/yokobonbon/items/b5ae32ab50e3cf24c1b2)
- [MDN web docs:\<video\>: 動画埋め込み要素](https://developer.mozilla.org/ja/docs/Web/HTML/Element/video)
- [NHKクリエイティブライブラリー](https://www2.nhk.or.jp/archives/creative/material/view.cgi?m=D0002161323_00000)
  - 動画の取得元

## Github Pages

[https://sampleuser0001.github.io/HLS-sample-with-AWS-S3/](https://sampleuser0001.github.io/HLS-sample-with-AWS-S3/)

## Repository

[https://github.com/SampleUser0001/HLS-sample-with-AWS-S3](https://github.com/SampleUser0001/HLS-sample-with-AWS-S3)