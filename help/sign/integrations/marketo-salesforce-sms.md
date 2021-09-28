---
title: Adobe Sign for SalesforceとMarketoを使用して通知を送信する
description: 署名者に契約が進行中であることを知らせるために、テキストメッセージ、電子メール、またはプッシュ通知を送信する方法を説明します
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Adobe Sign for SalesforceとMarketoを使用して通知を送信する

Adobe Sign、Adobe Sign for Salesforce、Marketo、およびMarketo Salesforce Syncを使用して契約が進行中であることを署名者に知らせるために、テキストメッセージ、電子メール、またはプッシュ通知を送信する方法を説明します。 Marketoから通知を送信するには、まずMarketo SMS管理機能を購入または構成する必要があります。 このチュートリアルでは、[Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)を使用しますが、他のMarketo SMSソリューションも利用できます。

## 前提条件

1. Marketo Salesforce Syncをインストールします。

   Salesforce Syncの情報と最新のプラグインは、[ここで入手できます。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Salesforce用Adobe Signをインストールします。

   このプラグインに関する情報は、[ここで入手できます。](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## カスタムオブジェクトを検索する

Marketo Salesforce SyncとAdobe Sign for Salesforceの設定が完了すると、Marketo Admin Terminalに新しいオプションがいくつか表示されます。

![管理者](assets/adminTab.png)

![オブジェクト同期](assets/salesforceAdmin.png)

1. 初めての場合は、[**スキーマの同期**]をクリックします。 それ以外の場合は、**[スキーマの更新]**&#x200B;をクリックします。

   ![更新](assets/refreshSchema1.png)

1. グローバル同期が実行中の場合は、**[グローバル同期を無効にする]**&#x200B;をクリックして無効にします。

   ![無効にする](assets/disableGlobal.png)

1. [**スキーマの更新**]をクリックします。

   ![更新2](assets/refreshSchema2.png)

## カスタムオブジェクトの同期

右側の「Lead」、「Contact」、「Account」の各カスタム・オブジェクトを参照してください。

**Salesforceの契** 約にリードが追加されたときにトリガーする場合は、「リード」の下のオブジェクトに対して「同期」を有効にします。

**Salesforceの契** 約にContactが追加されたときにトリガーする場合は、「Contact」の下のオブジェクトに対して「Sync」を有効にします。

**Salesforceで** 免除承諾にAccountが追加されたときにトリガーする場合は、「Account」の下のオブジェクトに対して「Sync」を有効にします。

1. **目的の** 親（リード、連絡先、またはアカウント）の下に表示されるカスタム・オブジェクトに対して「同期」を有効にします。

   ![カスタムオブジェクト](assets/customObjects.png)

1. 次のアセットは、**Enable Sync**&#x200B;の方法を示します。

   ![カスタム同期1](assets/customObjectSync1.png)

   ![カスタム同期2](assets/customObjectSync2.png)

1. カスタムオブジェクトでの同期の有効化が終了したら、同期を再アクティブ化します。

   ![グローバルを有効にする](assets/enableGlobal.png)

## プログラムの作成

1. 「マーケティング」の「マーケティング活動」セクションで、左側のバーの「**マーケティング活動**」を右クリックし、「**新規キャンペーンフォルダ**」を選択して名前を付けます。

   ![新しいフォルダ](assets/newFolder.png)

1. 作成したフォルダを右クリックし、[**新しいプログラム**]を選択して、名前を付けます。 他の設定はデフォルトのままにし、**作成**&#x200B;をクリックします。

   ![新しいプログラム1](assets/newProgram1.png)

   ![新しいプログラム2](assets/newProgram2.png)

## Twilio SMSの設定

まず、Twilioのアカウントがアクティブで、必要なSMS機能を購入します。

Marketo - Twilio SMS Webフックを設定するには、アカウントから3つのTwilioパラメータが必要です。

- アカウントSID
- アカウントトークン
- Twilio電話番号

アカウントからこれらのパラメータを取得し、Marketoインスタンスを開きます。

1. 右上の&#x200B;**Admin**&#x200B;をクリックします。

   ![管理者](assets/adminTab.png)

1. [**Webhooks**]をクリックし、[**新しいWebhook**]をクリックします。

   ![Webhooks](assets/webhooks.png)

1. **Webhook名**&#x200B;と&#x200B;**説明**&#x200B;を入力します。

1. 次のURLを入力し、**[ACCOUNT_SID]**&#x200B;と&#x200B;**[AUTH_TOKEN]**&#x200B;をTwilioの資格情報で置き換えてください。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. リクエスト・タイプとして&#x200B;**POST**&#x200B;を選択します。

1. 次の&#x200B;**テンプレート**&#x200B;を入力し、**[MY_TWILIO_NUMBER]**&#x200B;をTwilioの電話番号に、**[YOUR_MESSAGE]**&#x200B;を選択したメッセージに置き換えてください。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 要求トークンのエンコードを「フォーム/URL」に設定します。

1. 応答の種類をJSONに設定し、**保存**&#x200B;をクリックします。

## スマート・キャンペーン・トリガーの設定

1. 「マーケティング活動」セクションで、作成したプログラムを右クリックし、「**新規スマート・キャンペーン**」を選択します。

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 名前を付け、[**作成**]をクリックします。

   ![スマートキャンペーン2](assets/smartCampaign3.png)

   Custom Object Syncの構成が正しく行われた場合は、Salesforceフォルダで使用可能な次のトリガが表示されます。

1. 「契約に追加」をクリックし、スマート・リストにドラッグします。 トリガーに対して必要な制約を追加します。

   ![契約2に追加](assets/addedToAgreement2.png)

## スマート・キャンペーン・フローの設定

1. スマート・キャンペーンの「**フロー**」タブをクリックします。 **Call Webhook**&#x200B;フローを検索してキャンバスにドラッグし、前のセクションで作成したWebhookを選択します。

   ![Webhookの呼び出し](assets/callWebhook.png)

1. 契約に追加された潜在顧客に対するSMS通知キャンペーンが設定されました。

>[!TIP]
>
>このチュートリアルは、エクスペリエンス・リーグで無料で利用できるAdobe Sign for SalesforceとMarketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)を使用して、セールス・サイクルを短縮するコース[の一部です。