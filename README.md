# Hearable HeadTracker
---
### Overview
Hearable HeadTrackerはヒアラブルデバイス（フォスター電機 RN002）に実装されているヘッドトラッキング機能のフロントエンドアプリケーションです。

WebBluetoothを用いてヒアラブルデバイスRN002からデータ取得を行い、ブラウザに表示されているオブジェクトの回転、およびWebSocket経由で任意の宛先に送出します。\
オブジェクトの回転およびWebSocketのデータは、ヒアラブルデバイスのジャイロセンサー／加速度センサーの出力をMadgwickフィルタにより四元数（Quaternion）に変換しており、Thress.jsやUnityなどの3Dオブジェクト制御に使用することが可能です。

### 対応ブラウザ
WebBluetoothに対応したブラウザ　参考：[ブラウザー互換性一覧表 Mozilla.org](https://developer.mozilla.org/ja/docs/Web/API/Web_Bluetooth_API#ブラウザーの互換性)

#### 動作することを確認しているブラウザ
- Chrome（Windows,Mac）
- Edge（Windows,Mac）
  
#### 動作しないことを確認しているブラウザ
- Safari（Mac,iOS）





