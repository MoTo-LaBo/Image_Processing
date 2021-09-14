# Image processing (画像処理基礎)
### <u>フィルタリング, パターン認識, 撮像過程</u>
- **Scikit-image, OpenCV, PIL, ScipyなどのPythonモジュールを駆使して画像処理**

- *Docker を使用した環境構築*
  - ANACONDA, Jupyterlab, ubuntu, docker, 各種 pip

・jupyter notebookを用いたpythonによる画像処理例

・カメラ映像をpythonでリアルタイムに画像処理する方法

・OpenCVを用いた画像処理

・Scikit-imageを用いた画像処理
## 学習領域
- グレースケール画像とカラー画像，ヒストグラム，トーンカーブ，コントラスト，画像間演算

- 二値画像処理，しきい値，ラベリング，モルフォロジー処理，細線化

- 動画像処理，背景差分，フレーム間差分，オプティカルフロー，カルマンフィルタ，パーティクルフィルタ

- 画像の幾何変換，回転，並進，補間，合成，アフィン変換，射影変換，同次座標

- フィルタリング，平均値フィルタ，ガウスフィルタ，エッジフィルタ，ラプラシアンフィルタ，Cannyエッジ検出，非線形フィルタ

- 2次元フーリエ変換，スペクトル，2DFFT，周波数空間でのフィルタリング，ローパスフィルタ，ハイパスフィルタ，リンギング

- 逆フィルタ，ウィーナフィルタ，超解像，HDR

- 領域分割，テクスチャ特徴量，クラスタリング（k-means, GMM, mean shift），動的輪郭モデル，グラフカット

- テンプレートマッチング，ハフ変換，特徴点検出（Harris, FAST），特徴量マッチング（SIFT, ORB, KAZE），パノラマ画像作成

- パターン認識，教師あり・教師なし・半教師あり学習，kNN 最近傍法，SVM サポートベクトルマシン，Boosting，顔検出，ランダムフォレスト

- ディープラーニング，MLP 多層パーセプトロン，CNN 畳込みネットワーク，物体検出などの応用例

- 撮像過程，透視投影，ピンホールカメラモデル，レンズモデル，歪曲収差，被写界深度，撮像素子，シャッター

- 3次元復元，ステレオ視，エピポーラ幾何，キャリブレーション，アクティブステレオ，SfM

- 色，分光分布，RGB表色系，XYZ表色系，カラーマッチング，YUV

- 視覚系，眼球，視細胞，視覚情報経路

##  環境構築
### <u>1. Dockerfile build で docker image を作成</u>
    docker build .<directory>
- .(ドット)はカレントdirectory ※ 基本は Dockerfile のある directory に移動して docker build を使用するので、$ `docker build .< directory >` の形で覚えておく
### <u>2. Dockerfile build -t を付けると name も一緒に付けることができる</u>
    docker build -t <name> .<directory>
### <u>3. image 確認</u>
    docker images
### <u>4. docker images で name が < none > だと使いにくい</u>
    docker build -t < name >:latest .
- . ( ドット ) はカレントdirectory で Dockerfile の場所を指定する
- latest :
- docker build の時に -t を付ける(tag): 名前をつけて build する
- 名前をつけないと none で表示される
  - **dangling : ダングリングイメージ(ぶら下がっているの意)**
### <u>5. 1, 2, 3 を踏まえて docker build する</u>
    docker build -t pyimage:latest .
- biuld する時の場所は Image_Processing directory にいる事
- .(ドット：カレントディレクトリを指定している)
### <u>6. container を立てる</u>
    docker run -v ~/udemy/Image_Processing:/work -p 1212:8888 --name image-env pyimage
- -v option を付けると、container の file system を Host に mount する事ができる
- -p option : port (ポート) Jupyterlab は web のアプリケーション。ネットワークを介してアクセスするものなので、指定した port の上で動かす必要がある
- 今回は *1212*:8888 という port の上で動くようにしてある default の Jupyter の port の番号
- container の port を Host に繋げてあげないと動かない。なので host 側の localhost.8888 に接続すると container 8888 に届くようになっている
-   -- name で container に名前を付ける事ができる
    -   名前を付けないと container の方で default で変な名前が付けられてしまう
### <u>7. browser に移動 -> Jupyter lab 起動</u>
-  ブラウザで **localhost:8888** アクセス
   -  Firefox, chrome が良い
-  Jupyter lab が表示される
-  Docker を使用する事で簡単に環境構築ができる
## Docker の基本操作
### コンテナ一覧表示
    docker ps -a
### docker image 一覧表示
    docker images
### docker image から container 起動
    docker run -v ~/udemy/Image_Processing:/work -p 1212:8888 --name image-env pyimage
### コンテナを止める
    docker stop <container>
### コンテナを削除
    docker rm <container>
### コンテナを restart
    docker restart <container>
