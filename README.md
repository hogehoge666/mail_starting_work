

# 概要
- 始業と終業の報告メールをOutlookで送るAppleScript


---


# ビルド
- scptソースファイルをスクリプトエディタで開く
- メニューから「ファイル」＞「書き出す」を選択
- ファイルフォーマットから「アプリケーション」を選択して保存する

---


# 実行
- starting_work_message.txtに始業報告メッセージを記載する
  - 例
```
おはようございます。
在宅勤務を開始します。


■ 本日の業務内容
- XXXX
- YYYY
- XXXX

■ 勤務予定時間
<START>～18:00
 
山田太郎

```
- ending_work_message.txtに終業報告のメッセージを記載する
  - 例
```
本日の業務を終了いたします。

山田太郎

```
- settings.plistに設定を記載する
  - 例
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>dontSend</key>
	<false/>
	<key>lastStartTime</key>
	<string>9:00</string>
	<key>myID</key>
	<string>orenoID</string>
	<key>recipient</key>
	<string>joushi@kaisha.co.jp</string>
</dict>
</plist>

```
- 実行ファイルを実行する

---


# ファイル一覧

### mail_starting_work.app
- 始業メッセージアプリの実行ファイル
### mail_ending_work.app- 終業メッセージアプリの実行ファイル

### mail_starting_work.scpt
- 始業メッセージアプリのソースファイル
### mail_ending_work.scpt- 終業メッセージアプリのソースファイル
### settings.plist
- 始業メッセージアプリと終業メッセージアプリが読み込む設定ファイル

### starting_work_message.txt
- 始業メッセージの文面

### ending_work_message.txt
- 終業メッセージの文面


---


# 始業メッセージアプリの動作概要

- 現在日時と設定ファイルのmyIDをもとにSubjectを生成する
- 現在時刻をもとにメールに記載する業務開始時刻を以下の中から選ぶ
  - 9:00, 9:30, 10:00
  - 遅すぎる場合はエラーとする
- starting_work_message.txtと業務開始時刻を組み合わせて本文を生成する
- 設定ファイルのrecipient宛にメールを送信する
  - 設定ファイルでdontSendがtrueの場合は送信を意図的に失敗させる
  - 送信失敗したメールは下書きフォルダに保存される
- 業務開始時刻を設定ファイルに保存する
  - 終業メッセージで利用する


---


# 終業メッセージアプリの動作概要

- 現在日時と設定ファイルのmyIDをもとにSubjectを生成する
- starting_work_message.txt、ending_work_message.txt、設定ファイルのlastStartTimeを組み合わせて本文を生成する
- 設定ファイルのrecipient宛にメールを送信する
  - 設定ファイルでdontSendがtrueの場合は送信を意図的に失敗させる
  - 送信失敗したメールは下書きフォルダに保存される


---


# AppleScriptで開発した理由

- MacのOutlookはAutomatorで自動化できない
- MacのOutlookでQuick Actionや拡張機能を実装する方法を検索してもよい文献が見つからない


---


# AppleScript参考
https://www.youtube.com/playlist?list=PL5iB9WEZe2j04doUAKVxqxaCv3JJ8TxQr


