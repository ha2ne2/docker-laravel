# 問い合わせフォーム営業の開発環境作成手順書

作成 2020/05/02 hashi  
更新 2020/05/02 hashi

Docker と Docker Compose を使って、 問い合わせフォーム営業の開発環境を構築します。  
Docker は簡単にいえば環境構築を簡単に行えるようにするためのソフトです。  
詳しく知りたい場合は下記サイトがおすすめです。  

Docker入門（第一回）～Dockerとは何か、何が良いのか～  
https://knowledge.sakura.ad.jp/13265/

【初心者向け】20分でLaravel開発環境を爆速構築するDockerハンズオン  
https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4

# 事前準備
dockerとdocker-composeをインストールして下さい。  
Mac / Windowsの場合はDocker Desktopというソフトを使えば簡単にインストールできます。
https://www.docker.com/products/docker-desktop

# 構築する環境の構成
- php 7.3
- laravel 5.8
- MySQL 8.0
- nginx 1.17
- redis 5.0
- phpMyAdmin 5.0

# コンテナの構成
- appコンテナ : php, laravel用です。http://localhost:10080 でアクセス出来ます。
- phpmyadminコンテナ : phpmyadmin用です。http://localhost:18080 でアクセス出来ます。
- dbコンテナ : mysql用です。
- webコンテナ : nginx用です。

# 構築手順

0. 開発ディレクトリへ移動します。  
   普段開発時に使っているディレクトリへ移動して下さい。  
   開発ディレクトリ名がworkの場合の例
   ```
   $ cd ~/work
   ```
   
   ディレクトリ構成は最終的に下記のようになります。
   ```
   work 
   ├ ...
   ├ ...
   ├ form_sales
   └ docker-laravel
   ```


1. 問い合わせフォーム営業プログラムのソースコードをDLします。
   ```
   $ git clone https://github.com/seven-chord/form_sales.git
   ```

2. dockerの構成情報ファイルをDLします。
   ```
   $ git clone https://github.com/ha2ne2/docker-laravel
   ```

3. dockerコンテナの立ち上げ
   ```
   $ cd docker-laravel
   $ docker-compose up -d --build
   ```
   初回起動時は各種ソフトのインストールが走ります。私のノートパソコンで5分ほど掛かりました。気長に待ちましょう。

4. 動作確認  
   環境構築は以上で完了です。  
   ステップ3でエラーが出る場合は、エラー文で検索をしてみるか、  
   Slackで私宛に質問してもらえると力になれると思います。  
   ステップ3が正常に終了した場合、実際に動くか動作確認をします。  
   http://localhost:10080 にアクセスしてPHPが動作しているか確認して下さい。  
   http://localhost:18080 にアクセスしてphpmyadminが動くか確認して下さい。  

5. 開発！  
  Docker を使わない場合と同様に、form_sales ディレクトリ内のソースコードを変更すれば、変更が反映されます。

# よく使うコマンドなど

- dockerコンテナの起動 (OS再起動後など)
  ```
  $ cd ~/work/docker-laravel
  $ docker-compose up -d --build
  ```

- 起動中のコンテナの停止
  ```
  $ cd ~/work/docker-laravel
  $ docker-compose down
  ```

- dockerコンテナの稼働状況を確認する
  ```
  $ docker-compose ps
  ```

- appコンテナへ入る  
  ```
  $ docker-compose exec app ash
  ```
- 各種ログファイルは docker-laravel/logs ディレクトリに出力されます。  


# その他
Docker を使ったのが初めてなので、おかしなところがあったら指摘をお願いします。
