---
title: 埋め込みの電子サインと文書エクスペリエンスを作成
description: Acrobat Sign API を使用して、電子サインと文書エクスペリエンスを web プラットフォームやコンテンツ管理システム、文書管理システムに組み込む方法を説明します
role: User, Developer
level: Intermediate
topic: Integrations
jira: KT-7489
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 2%

---

# 組み込みの電子サインと文書エクスペリエンスを作成

Acrobat Sign API を使用して、電子サインや文書エクスペリエンスを web プラットフォームやコンテンツ管理システム、文書管理システムに組み込む方法を説明します。 この実践チュートリアルには 4 つのパートがあります。

## パート 1:必要なもの

パート 1 では、パート 2 ～ 4 に必要なすべての作業の開始方法を学習します。 まず、API 資格情報を取得します。

+++API 資格情報を取得する方法の詳細を表示

* [Acrobat Sign デベロッパーアカウント](https://acrobat.adobe.com/jp/ja/sign/developer-form.html)
* [スターターコード](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS コード（または任意のエディター）](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — ビルトインインストーラー
   * Windows — Chocolatey
   * すべて — https://www.python.org/downloads/

+++

## パート 2:低/コードなし — Web フォームのパワー

パート 2 では、Web フォームの使用に関する低コード/コードなしオプションについて説明します。 最初にコードを書くのを避けることができるかどうかを確認することは、常に良い考えです。

+++ Web フォームの作成方法の詳細を表示

1. 開発者アカウントでAcrobat Signにアクセスします。

1. 選択 **Web フォームの公開** をクリックします。

   ![スクリーンショットAcrobat Signホームページ](assets/embeddedesignature/embed_1.png)

1. 契約書を作成します。

   ![Web フォームの作成方法のスクリーンショット](assets/embeddedesignature/embed_2.png)

1. 契約書をフラットな埋め込みページにHTMLします。

1. 動的にクエリパラメーターを追加してみます。

   ![クエリパラメーターの追加のスクリーンショット](assets/embeddedesignature/embed_3.png)

+++

## パート 3:フォームと結合データを使用した契約書の送信

パート 3 では、契約書を動的に作成します。

+++契約書の動的な作成方法の詳細を表示

まず、アクセス権を設定する必要があります。 Acrobat Signでは、API 経由で接続する方法が 2 つあります。 OAuth トークンと統合キー。 アプリケーションで OAuth を使用する特別な理由がない限り、まず統合キーを調べる必要があります。

1. 選択 **統合キー** 」を **API 情報** メニューを **アカウント** 」タブをクリックします。

   ![統合キーの場所を示すスクリーンショット](assets/embeddedesignature/embed_4.png)

API にアクセスして操作できるようになったので、API で何ができるかを確認してください。

1. 次の場所にある [Acrobat Sign REST API バージョン 6 メソッド](http://adobesign.com/public/docs/restapi/v6)を選択します。

   ![Acrobat Sign REST API バージョン 6 メソッドを操作するスクリーンショット](assets/embeddedesignature/embed_5.png)

1. トークンを「ベアラー」値として使用します。

   ![ベアラー値のスクリーンショット](assets/embeddedesignature/embed_6.png)

最初の契約書を送信するには、API の使用方法を理解するのが最善です。

1. 一時的なドキュメントを作成して送信します。

>[!NOTE]
>
>JSON ベースのリクエスト呼び出しには、「モデル」と「最小モデルスキーマ」オプションがあります。 これにより、仕様と最小ペイロードセットが提供されます。

![一時ドキュメント作成のスクリーンショット](assets/embeddedesignature/embed_7.png)

契約書を初めて送信した後は、ロジックを追加する準備が整います。 繰り返しを最小限に抑えるために、いくつかのヘルパーを確立することをお勧めします。 次に例をいくつか示します。

**バリデーター**

![検証ロジックのスクリーンショット](assets/embeddedesignature/embed_8.png)

**ヘッダー/認証**

![ヘッダー/認証ロジックのスクリーンショット](assets/embeddedesignature/embed_9.png)

**ベース URI**

![ベース URI ロジックのスクリーンショット](assets/embeddedesignature/embed_10.png)

Transient ドキュメントが Sign エコシステムの壮大なスキーム内のどこに位置するかに注意してください。
一時的 —> 契約一時的 —> テンプレート —> 契約一時的 —> ウィジェット —> 契約書

この例では、テンプレートをドキュメントソースとして使用しています。 署名用にドキュメントを動的に生成する明確な理由（レガシーコードやドキュメント生成など）がない限り、通常はこれが最善の方法です。

このコードはかなり単純です。ドキュメントソースとしてライブラリ文書（テンプレート）を使用します。 最初と 2 番目の署名者は動的に割り当てられます。 この `IN_PROCESS` state は、文書がすぐに送信されることを意味します。 また、 `mergeFieldInfo` フィールドへの動的な入力に利用されます。

![署名を動的に追加するコードのスクリーンショット](assets/embeddedesignature/embed_11.png)

+++

## パート 4:署名エクスペリエンスやリダイレクトなどの埋め込み

多くのシナリオでは、トリガーした参加者がすぐに契約書に署名できるようにする必要があります。 これは、顧客向けのアプリケーションやキオスクで便利です。

+++署名エクスペリエンスを埋め込む方法について詳しく見る

最初の送信メールがトリガーされないようにするには、API 呼び出しを変更して動作を管理する方法が簡単です。

![メール送信をトリガーしないコードのスクリーンショット](assets/embeddedesignature/embed_12.png)

署名後リダイレクトを制御する方法は次のとおりです。

![署名後リダイレクトを制御するコードのスクリーンショット](assets/embeddedesignature/embed_13.png)

契約書作成プロセスを更新した後、最後の手順は署名 URL の生成です。 この呼び出しも非常に簡単で、署名者が署名プロセスの自分の部分にアクセスするために使用できる URL を生成します。

![署名者 URL を生成するコードのスクリーンショット](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>契約書作成の呼び出しは、技術的には非同期です。 これは、「POST」契約書の呼び出しは可能であるが、契約書はまだ準備ができていないことを意味します。 最適な方法は、再試行ループを確立することです。 お使いの環境に最適な方法で再試行を行ってください。

![再試行ループを確立することがベストプラクティスであるというスクリーンショット](assets/embeddedesignature/embed_15.png)

すべての要素を組み合わせれば、解決は非常に容易になります。 契約書を作成してから、署名者がクリックして署名の儀式を開始するための署名 URL を生成します。

+++

## その他のトピック

* [JS イベント](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook イベント
   * [REST API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Acrobat Sign v6 の Webhooks](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [リクエスト電子メールの再アクティベート（イベントあり）](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [タイムアウトを再試行に置き換える](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* カスタムリマインダー
   * 最初の作成時

     ![Power Automate への移動のスクリーンショット](assets/embeddedesignature/embed_16.png)

   * または、1 つ追加します [機内で](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)
