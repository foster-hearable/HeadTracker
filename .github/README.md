# Hearable HeadTracker
---
## Overview
Hearable HeadTrackerはヒアラブルデバイス（フォスター電機 RN002）に実装されているヘッドトラッキング機能のフロントエンドアプリケーションです。\
★ デモ用Webサイト [https://foster-hearable.github.io/HeadTracker/](https://foster-hearable.github.io/HeadTracker/) 

WebBluetoothを用いてヒアラブルデバイスRN002からデータ取得を行い、ブラウザに表示されているオブジェクトの回転やWebSocketでのデータ送出を行います。\
オブジェクトの回転およびWebSocketのデータは、ヒアラブルデバイスのジャイロセンサー／加速度センサーの出力をMadgwickフィルタにより四元数（Quaternion）に変換しており、Thress.jsやUnityなどの3Dオブジェクト制御に使用することが可能です。

## 対応ブラウザ
WebBluetoothに対応したブラウザ（参考：[ブラウザー互換性一覧表 Mozilla.org](https://developer.mozilla.org/ja/docs/Web/API/Web_Bluetooth_API#ブラウザーの互換性)）
#### 動作することを確認しているブラウザ
- Chrome（Windows,Mac,Android）
- Edge（Windows,Mac）
  
#### 動作しないことを確認しているブラウザ
- Safari（Mac,iOS）
- Chrome (iOS)


## 操作インターフェース
<img src="Panel.png" width="450">

#### ① Object
ヒアラブルデバイスより送られてくるデータに合わせて回転します。\
接続直後や大きく回転した直後にはフィルタによる補正が動作し、ヒアラブルデバイスが動いていない場合であっても適切な位置まで徐々に回転することがあります。

#### ② Controls
- Start Notify：クリックするとBLEデバイスの選択ウィンドウが表示されます（選択後、通知データが送られてくるまで20秒程度かかる場合があります）
- Stop Notify：ヒアラブルデバイスからのデータ通知を停止する場合にクリックします。データ通知を再開させたい場合にはブラウザをリロードしてください。
- Reposition：Objectの向きを正面に戻します。ヒアラブルデバイスの実際の向きとObjectの向きを合わせる場合にクリックしてください（データ通知停止後にはブラウザのリロードボタンに切り替わります）

#### ③ WebSocket
- WebSocket URL：WebSocketで接続するURLを指定してください。
- Connect：WebSocket URLとの接続/切断を行います。本ページがロードされた直後に自動的に接続を試みます。
  
#### ④ Status
- 接続しているデバイス名や受信したデータの種別やデータ数を表示します

## WebSocketでの拡張
WebSocketで送られてきたヒアラブルデバイスの回転データを各製品のAPIに渡すことにより、任意のアバターやロボットなどの制御を行うことが可能になります。

<img src="Expand.png" width="450">

#### WebSocketデータフォーマット
コンマ区切りで下記順序のデータ列を送出します。

|   | データ種別 | フォーマット |
|-|-|-|
| 1 | ステータス | bit7-2:使用せず、bit1:タッチ操作(1:ON、0:OFF)、bit0:装着(1:ON、0:OFF) |
| 2 | W成分 | Float値によるQuaternionのW成分データ |
| 3 | X成分 | Float値によるQuaternionのX成分データ |
| 4 | Y成分 | Float値によるQuaternionのY成分データ |
| 5 | Z成分 | Float値によるQuaternionのZ成分データ |


## 注意事項
- ヒアラブルデバイスに接続してからオブジェクトが回転するまで最大で20秒程度の時間がかかる場合があります。
- 左右のヒアラブルデバイスを使用している場合、状況に応じて自動的にどちらか片側のヒアラブルデバイスからのセンサー情報を取得します。\
  右または左の任意のヒアラブルデバイスからデータ取得を行いたい場合は、使用しないヒアラブルデバイスをチャージケースに収納してから接続してください。  
- 動作確認されているブラウザであっても、バージョンやプラグインの状況などによってはアプリケーションが正常に動作しないことがあります。また、ブラウザまたはシステムの省エネモードなどの影響によりデータ更新タイミングが変化する場合があります。
  
※ワイヤレス通信は周囲の状況によりデータ欠落や再送・遅延が発生します。センサーデータはこれらの事象を考慮したうえでご利用ください。\
※このアプリケーションはヒアラブルデバイス（フォスター電機 RN002）の評価を目的として[MITライセンス](https://github.com/foster-hearable/HeadTracker/blob/e59c1e2fe2de506fb53649f6b3cb550f1e6ca852/LICENSE.txt)の下に公開しております。

