# scikit learn basic
・scikit-learnによる機械学習ライブラリの利用

・Docker を使用した環境構築
  - ANACONDA, Jupyterlab, ubuntu, docker

・numpy

・matplotlibによるデータの可視化

・pandasによるデータの前処理

・基本統計量のプログラミング

## 機械学習
・k-means法

・PCAによる時限削減

・線形回帰（単回帰分析・重回帰分析）

・SVM（サポート・ベクトル・マシン）

・ランダムフォレストによる分類

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
## Docker container とは？
### <u>container は localhost とは独立した環境</u>
- *hostがどういう環境であろうとcontainerを作れば同じ環境になる*
