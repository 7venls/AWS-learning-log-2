# EC2 / S3 / CloudTrail が どう連動しているかを体感する。

・「作った・触った・記録された」を一気に確認する。

# 1. EC2にSSH接続

【 ssh -i my-key.pem ec2-user@<EC2のパブリックIP> 】

・ログインできればOK。

---

# 2. Webサーバをインストール＆起動

### 2-1. nginx インストール

【 sudo yum install -y nginx 】

### 2-2. 起動 & 自動起動

【 sudo systemctl start nginx 】

【 sudo systemctl enable nginx 】

### 2-3. ステータス確認

【 systemctl status nginx 】

・active (running) ならOK。

---

# 3. HTMLを配置（表示用）

【 echo "<h1>Hello AWS Day6</h1>" | sudo tee /usr/share/nginx/html/index.html 】

実行後の表示 ⇒ 【 <h1>Hello AWS Day6</h1> 】だ出たら成功。

---

# 4. ブラウザで確認

【 http://<EC2のパブリックIP> 】

⇒ 【 Hello AWS Day6 】表示されたら成功。

⇒ EC2でアプリ（Web）が動いた。

---

# 5. CloudTrailに残すため「操作」をする

### 5-1. EC2 ⇒ インスタンス選択

### 5-2. 停止（Stop）

### 5-3. 数分待つ

### 5-4. 起動（Start）

---

# 6. CloudTrailでイベント履歴を確認

### 6-1. CloudTrail → イベント履歴

### 6-2. フィルタ設定

・イベント名：StartInstances

・リソースタイプ：AWS::EC2::Instance

### 6-3. 確認ポイント

【 イベント詳細で見る 】

・userIdentity → 自分

・eventTime → 今

・sourceIPAddress → 自分のIP

・eventName → StartInstances

「誰が・何をしたか」確認。

---

# 7. S3に保存されたログを見る

### 7-1. CloudTrailログ用S3バケットを開く

### 7-2. パスを辿る

AWSLogs/

 └─ <アカウントID>/

     └─ CloudTrail/
     
         └─ ap-northeast-1/

### 7-3. 確認

・.json.gz ファイルがある。

・Digest/ フォルダがある。

ログ保存 & 検証が動いている証拠。

---
