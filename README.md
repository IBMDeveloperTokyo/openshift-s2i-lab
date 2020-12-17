## 事前準備
1. IBM Cloudライトアカウント作成
2. GitHubアカウント作成

## OpenShiftへのいろいろな入力パターン
![](./images/001.png)

本ハンズオンワークショップではこの中からSource to Image (S2I) を試します。
![](./images/002.png)

## ハンズオンワークショップの流れ
1. OpenShift環境の準備
2. ソースコードのFork
3. アプリケーションのDeploy
4. Webhookの設定
5. ソースコードの修正及びDeploy(⾃動）

## 1. OpenShift環境の準備
ワークショップ⽤のIBM Cloud環境にご⾃⾝のIBM Cloud IDを関連付けます。

注意事項
```
・ブラウザはFirefox, Chromeをご利⽤ください
・本ワークショップ⽤のIBM Cloud環境はセミナー開催時から24時間限定でお使いいただけます
```

### 1.1 下記URLにFirefoxブラウザでアクセス
https://openshiftdojo.mybluemix.net/

### 1.2 ハンズオン環境へSubmit
[Lab Key] 、[Your IBMid]にご⾃⾝のIDを⼊⼒し、チェックボックスにチェックを⼊れて[Submit]をクリックします。
![](./images/003.png)

### 1.3 IBM Cloudダッシュボードの起動
Congratulations! が表⽰されたら[1. Log in IBM Cloud]リンクをクリックします。
![](./images/004.png)

### 1.4 アカウントの切り替え
IBM Cloudダッシュボードの右上のアカウント情報の右横の「v」をクリックして、ワークショップ用のアカウントへ切り替えます。<br>
[1840867 – Advowork] のような「数字の羅列 - Advowork」がワークショップ用に準備されたアカウントです。 (数字部分は自動的に割り当てられます)<br>
※このアカウントは1日程度で無効になる一時的なアカウントです。
![](./images/005.png)

### 1.5 OpenShiftクラスタへのアクセス
IBM Cloudダッシュボードの右上のアカウント情報が変更されたことを確認し、[リソースの要約]の[Clusters]をクリックします。
![](./images/006.png)

Clustersの下のクラスター名をクリックします。 (クラスター名は⾃動的に割り当てられます)
![](./images/007.png)

### 1.6 OpenShift Webコンソールの起動
[OpenShift Webコンソール]ボタンをクリックします。<br>
※ポップアップが制御されていると動作しませんので解除してください。
![](./images/008.png)

新しいウィンドウ（またはタブ）でOpenShiftのコンソールが開けばOKです。アクセスするURLはポート30000番台（⾃動で割り当てられます）を使っているので、社内プロキシなどで制限している場合はポートを開いておいてください。<br>
Webコンソールは、通常以下のようなURLでリダイレクトされます。
```https://c100-e.jp-tok.containers.cloud.ibm.com:31379/```
![](./images/009.png)

これでOpenShiftワークショップの環境準備は完了です。


## 2. ソースコードのFork
ここからはGitHubへアクセスして自分のリポジトリへサンプルソースコードをForkしていきます。

### 2.1 GitHubへのサインイン
GitHubにサインイン(Sign in)してください。まだアカウント登録されていない方は[こちら](https://github.com/)からサインアップ(Sign up)してください。<br>
![](./images/010.png)

### 2.2 リポジトリーのFork
ブラウザーで[https://github.com/osonoi/node-build-config-openshift](https://github.com/osonoi/node-build-config-openshift)を開いてください。<br>
[Fork]ボタンをクリックして、自分のアカウントを選択してください。
![](./images/011.png)

### 2.3 自分のリポジトリーの確認
Forkする際に指定した自分のリポジトリーへ、対象のプロジェクトがForkされたことを確認します。<br>
リポジトリーのパスの最初の部分が自分のGitHubアカウントになっていればOKです。
![](./images/012.png)


## 3. アプリケーションのDeploy
ここからは、先程用意したOpenShiftの環境へ、自分のGitHubリポジトリーにあるアプリケーションをデプロイします。

### 3.1 OpenShift Projectの作成
OpenShiftのWebコンソールへ戻り、[Project]ボタンをクリックします。<br>
その後[Create Project]ボタンをクリックするとCreate Project画面が開きますので、任意のプロジェクト名を入力してください。例では「Dojo」としています。
![](./images/013.png)

### 3.2 OpenShiftユーザータイプの切り替え
左上のメニューにて、[Administrator]から[Developer]に切り替えます。<br>
切り替えたら[From Git]をクリックしてください。
![](./images/014.png)

### 3.3 デプロイするアプリケーションのソースコードを指定
先ほどコピーした、自分のGitHubリポジトリーのURLを[Git Repo URL]に入力します。<br>
下の[Show Advanced Git Option]をクリックすると入力エリアが展開するので、[Content Dir]に「/site」と入力してください。
![](./images/015.png)

### 3.4 デプロイするアプリケーションのタイプを選択
言語やタイプの一覧がタイルで表示されるので、Node.jsを選択します。今回GitHubリポジトリーへForkしたプロジェクトはNode.jsアプリケーションだからです。<br>
選択したら[Create]ボタンをクリックしてください。
![](./images/016.png)

### 3.5 アプリケーションのデプロイ
アプリケーションのデプロイが始まります。1分弱お待ちください。中の丸が青くなったら完成です。丸の中をクリックすると右側にメニューが出てくるので[Routes]の下のURLをクリックするとWebへ公開されたアプリケーションへアクセスできます。
![](./images/017.png)

### 3.6 アプリケーションへのアクセス
デプロイされ、Webへ公開されたアプリケーションへアクセスできました。<br>
実際にこのアプリケーションへログインしてみましょう。ID,Passwordともに「test」と入れてログインしてください。<br>
医療関連のデータを管理するサンプルアプリケーションへログインできたかと思います。
![](./images/018.png)

ここまでで、GitHub上のソースコードをダイレクトにOpenShiftへデプロイする方法を学びました。


## 4. Webhookの設定
ここでは、GitHub上のソースコードが変更された際に、自動的にOpenShiftへデプロイされるようにWebhookをGitHub上へ設定していきたいと思います。

### 4.1 OpenShiftのWebhook URLの取得
OpenShiftのWebコンソールへアクセスします。左側のメニューから[Build]を選択し、右側のワークスペースに表示される[node-build-config-openshift]をクリックします。
![](./images/019.png)

下にスクロールして一番右の[Copy URL with Secret]をクリックしてWebhookのURLとSecretをクリップボードにコピーしてください。
![](./images/020.png)

### 4.2 GitHubにWebhookを設定
GitHubの自分のリポジトリーへ戻り、[Settings] -> [Webhooks] -> [Add webhook]を選択します。
![](./images/021.png)

先ほどクリップボードにコピーしたURL+secretを[Payload URL]に貼り付けてください。[Control type]は[application/json]を選択してください。
![](./images/022.png)

入力後、以下の図の様に緑のチェックマークが付いたら設定成功です。
![](./images/023.png)

これでwebhookの設定は完了です。後はソースコードの修正で自動的にアプリケーションがデプロイされます。
