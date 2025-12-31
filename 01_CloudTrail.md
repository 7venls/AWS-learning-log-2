# CloudTrail（操作ログ）を理解

## CloudTrail とは？

「誰が・いつ・何をしたか」を記録する操作ログ。

【 記録される例 】

・S3バケットを作成した。

・バケットポリシーを変更した。

・EC2を起動・停止した。

【 記録されない例（重要） 】

・HTMLの中身。

・Webページを誰が見たか。

⇒ これは CloudTrailの仕事じゃない。


# 1. まずはイベント履歴を見てみる（いちばん簡単）

### 1-1. AWSコンソール ⇒ CloudTrail

### 1-2. 左メニュー ⇒ イベント履歴

### 1-3. 画面に一覧が出る

【 ここで見る列 】

・イベント名（PutObject / CreateBucket など）

・イベントソース（s3.amazonaws.com）

・ユーザー名

・イベント時刻

# 2. S3操作を絞り込んで見る

【 フィルター例 】

・イベントソース：s3.amazonaws.com

・イベント名：PutObject / PutBucketPolicy

【 確認ポイント 】

・自分が index.html をアップロードした記録があるか？

・バケットポリシーを設定した記録があるか？

 操作＝全部APIとして残ってるのが分かる。

 # 3. EC2操作も見てみる

【 フィルター例 】

・イベントソース：ec2.amazonaws.com

・イベント名：RunInstances / StopInstances

「EC2起動＝RunInstances」

AWSは全部APIで動いてると理解できる。

# 4. ログの中身を1件開いてみる（重要）

### 4-1. 
