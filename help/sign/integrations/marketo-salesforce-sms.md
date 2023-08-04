---
title: SalesforceおよびMarketo向けAcrobat Signを使用した通知の送信
description: テキストメッセージ、電子メール、またはプッシュ通知を送信して、契約書が処理中であることを署名者に知らせる方法について説明します。
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Acrobat Signを使用して次の通知を送信： [!DNL Salesforce] および [!DNL Marketo]

テキストメッセージ、電子メール、またはプッシュ通知を送信して、Acrobat Sign、Salesforce向けAcrobat Sign、Marketo、Marketo Salesforce Syncを使用して契約書が作成されていることを署名者に知らせる方法について説明します。 Marketoから通知を送信するには、まずMarketo SMS管理機能を購入または設定する必要があります。 このチュートリアルでは、 [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)ただし、他のMarketo SMSソリューションも利用できます。

## 前提条件

1. Marketo Salesforce Syncをインストールします。

   情報およびSalesforce Syncの最新プラグインが利用可能です。 [はい。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Salesforce用Acrobat Signをインストールします。

   このプラグインに関する情報が利用可能です [はい。](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## カスタムオブジェクトの検索

Marketo Salesforce SyncとSalesforce向けAcrobat Signの設定が完了すると、Marketo管理ターミナルに新しいオプションがいくつか表示されます。

![管理者](assets/adminTab.png)

![オブジェクトの同期](assets/salesforceAdmin.png)

1. クリック **スキーマの同期** 初めてお使いの場合 それ以外の場合は、 **スキーマの更新**.

   ![更新](assets/refreshSchema1.png)

1. グローバル同期が実行されている場合は、をクリックして無効にします。 **グローバル同期を無効にする**.

   ![無効にする](assets/disableGlobal.png)

1. クリック **スキーマの更新**.

   ![更新2](assets/refreshSchema2.png)

## カスタムオブジェクトの同期

右側には、リード、取引先担当者、およびアカウントベースのカスタムオブジェクトを参照してください。

**同期を有効にする** は、Salesforceでリードが契約書に追加されたときにトリガーする場合にリードの下にあるオブジェクトです。

**同期を有効にする** （取引先担当者がSalesforceの契約書に追加されたときにトリガーする場合は「取引先担当者」のオブジェクト）。

**同期を有効にする** （Salesforceでアカウントが契約書に追加されたときにトリガーする場合は、アカウントのオブジェクト）。

1. **同期を有効にする** 目的の親（リード、取引先担当者または取引先企業）の下に表示されるカスタムオブジェクトの場合。

   ![カスタムオブジェクト](assets/customObjects.png)

1. 以下のアセットは、以下の方法を示しています **同期を有効にする**.

   ![カスタム同期1](assets/customObjectSync1.png)

   ![カスタム同期2](assets/customObjectSync2.png)

1. カスタムオブジェクトの同期の有効化が完了したら、同期を再アクティベートします。

   ![グローバルを有効化](assets/enableGlobal.png)

## プログラムの作成

1. Marketoの「Marketing Activities」セクションで、次を右クリックします。 **マーケティング活動** 左側のバーで、 **新規キャンペーンフォルダー**&#x200B;名前を付けてください。

   ![新規フォルダー](assets/newFolder.png)

1. 作成したフォルダを右クリックし、 **新しいプログラム**&#x200B;名前を付けてください。 それ以外をデフォルトのままにして、 **作成**.

   ![新規プログラム1](assets/newProgram1.png)

   ![新規プログラム2](assets/newProgram2.png)

## Twilio SMSの設定

まず、有効なTwilioアカウントがあり、必要なSMS機能を購入していることを確認します。

Marketoの設定 – Twilio SMS webhookには、アカウントから3つのTwilioパラメーターが必要です。

- アカウントSID
- アカウントトークン
- Twilioの電話番号

これらのパラメーターをアカウントから取得して、Marketoインスタンスを開きます。

1. をクリック **管理者** をクリックします。

   ![管理者](assets/adminTab.png)

1. をクリック **Webhooks**、次に **新しいWebhook**.

   ![Webhooks](assets/webhooks.png)

1. Aを入力 **Webhook名** および **説明**.

1. 次のURLを入力し、必ず **[ACCOUNT_SID]** および **[AUTH_TOKEN]** Twilioの資格情報を使用します。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選択 **POST** をリクエストのタイプとして使用します。

1. 次のように入力します **テンプレート** を置き換えます **[MY_TWILIO_NUMBER]** Twilioの電話番号を使用して **[YOUR_MESSAGE]** あなたの選んだメッセージで

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 「リクエストトークンエンコーディング」を「Form/URL」に設定します。

1. 「Response type」を「JSON」に設定し、 **保存**.

## スマートキャンペーントリガーの設定

1. 「マーケティング活動」セクションで、作成したプログラムを右クリックして「 **新しいスマートキャンペーン**.

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 名前を付けて、 **作成**.

   ![スマートキャンペーン2](assets/smartCampaign3.png)

   カスタムオブジェクト同期の設定が正しく行われた場合、Salesforceフォルダーに次のトリガーが表示され、使用できる必要があります。

1. 「契約書に追加」をクリックして、スマートリストにドラッグします。 トリガーに設定する制約を追加します。

   ![契約書2に追加されました](assets/addedToAgreement2.png)

## スマートキャンペーンフローの設定

1. アイコンをクリック **流量** タブをクリックします。 検索してドラッグ **Webhookを呼び出し** キャンバスに流し込み、前のセクションで作成したwebhookを選択します。

   ![Webhookを呼び出し](assets/callWebhook.png)

1. 契約書に追加されたリードのSMS通知キャンペーンが設定されました。

>[!TIP]
>
>このチュートリアルはコースの一部です [SalesforceおよびMarketo向けAcrobat Signで販売サイクルを加速](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) それはExperience Leagueで無料で入手できます！