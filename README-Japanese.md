<h1 align="center">Ereshkigal</h1>

<p align="center">
  <img src="icon.png" alt="Ereshkigal Icon" width="300" height="300" style="object-fit: cover;">
</p>

<p align="center">
  <a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FArifmaulanaazis%2FEreshkigal&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Total+Viewer&edge_flat=false"/></a>
  <img src="https://img.shields.io/github/downloads/Arifmaulanaazis/Ereshkigal/total?style=flat-square" alt="GitHub downloads"/>
</p>

<h2 align="center">ライセンス</h2>
<p align="center"><strong>ライセンス:</strong> GPLv3</p>

## Pilih Bahasa / Select Language / Chọn Ngôn Ngữ / เลือกภาษา / 言語を選択
- [Indonesia](README.md)
- [English](README-English.md)
- [Vietnamese](README-Vietnam.md)
- [Thailand](README-Thailand.md)
- [Japanese](README-Japanese.md)


## アプリケーションの説明
Ereshkigalは、RTL8720DNモジュールと連携して使用することを目的としたWiFiパケットインジェクション（deauther）テストアプリケーションです。このアプリケーションは、ユーザーがWiFiネットワークをテストし、deauthentication攻撃を実行して脆弱なアクセスポイントを特定する能力を提供します。

## アプリケーションの特徴
- WiFiネットワークのセキュリティをテストするためのdeauthenticationパケットインジェクション。
- シンプルで直感的なユーザーインターフェース。
- RTL8720DNモジュール（AI-Thinker BW16）との互換性。
- 2.4GHzおよび5GHzネットワークでのdeauthenticationパケットインジェクションをサポート。
- Ereshkigal Flasherによる簡単なフラッシュプロセス。

## 必要な材料
- RTL8720DNモジュール（AI-Thinker BW16）[こちらで購入](https://tokopedia.link/1k7qXB2VENb)
- モジュールとコンピュータを接続するためのUSB Type Cケーブル
- Windows OSを搭載したコンピュータ
- Ereshkigal V1.0.3.bin（アプリケーションのバイナリファイル）
- Ereshkigal Flasher V1.0.0.exe（フラッシュ用アプリケーション）

## インストールと使用方法のビデオチュートリアル
インストールと使用方法のチュートリアルについては、[YouTube](https://youtu.be/r1fH1nWJnAg)でビデオを視聴してください。

## フラッシュ手順
1. RTL8720DNモジュールをUSB Type Cケーブルでコンピュータに接続します。
2. Ereshkigal Flasher V1.0.0.exeをダウンロードして実行します。
3. 以前ダウンロードしたEreshkigal V1.0.3.binファイルを選択します。
4. 「Start Flash」ボタンをクリックしてフラッシュプロセスを開始します。
5. フラッシュプロセスが完了するまで待ちます。モジュールは自動的に再起動します。

## 使用方法
1. フラッシュが完了したら、モジュールを電源に接続します。
2. WiFiネットワークを開くと、EreshkigalというSSIDが表示されます。
3. Ereshkigalのパスワードは masukangin です。
4. Ereshkigalに接続したら、IPアドレス192.168.1.1を開きます。
5. テストしたいWiFiネットワークを選択してチェックします。
6. 「Deauth」ボタンを押してテストを開始します。
7. 「Scan」ボタンを使用してネットワークを再スキャンします。
8. RTL8720DNの「RST」ボタンを押してテストを停止します。

---

**注意:** このアプリケーションは、個人のネットワークテスト目的のみで使用し、適用される法律に従って使用してください。
