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
source-wordcount: '672'
ht-degree: 0%

---

# Acrobat Signを使用して[!DNL Salesforce]と[!DNL Marketo]に通知を送信します

テキストメッセージ、電子メール、またはプッシュ通知を送信して、Acrobat Sign、Salesforce向けAcrobat Sign、Marketo、Marketo Salesforce Syncを使用して契約書が作成されていることを署名者に知らせる方法について説明します。 Marketoから通知を送信するには、まずMarketo SMS管理機能を購入または設定する必要があります。 このチュートリアルでは[Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)を使用しますが、他のMarketo SMSソリューションも利用できます。

## 前提条件

1. Marketo Salesforce Syncをインストールします。

   情報およびSalesforce Syncの最新プラグインは、[こちら](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)から入手できます。

1. Salesforce用Acrobat Signをインストールします。

   このプラグインに関する情報は、[こちら](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)から入手できます。

## カスタムオブジェクトの検索

Marketo Salesforce SyncとSalesforce向けAcrobat Signの設定が完了すると、Marketo管理ターミナルに新しいオプションがいくつか表示されます。

![管理者](assets/adminTab.png)

![オブジェクトの同期](assets/salesforceAdmin.png)

1. 初めて使用する場合は、[**スキーマの同期**]をクリックします。 それ以外の場合は、[**スキーマの更新**]をクリックします。

   ![更新](assets/refreshSchema1.png)

1. グローバル同期が実行されている場合は、[**グローバル同期を無効にする**]をクリックして無効にします。

   ![無効](assets/disableGlobal.png)

1. **[スキーマの更新]**&#x200B;をクリックします。

   ![更新2](assets/refreshSchema2.png)

## カスタムオブジェクトの同期

右側には、リード、取引先担当者、およびアカウントベースのカスタムオブジェクトを参照してください。

Salesforceでリードが契約書に追加されたときにトリガーする場合は、リードの下にあるオブジェクトの&#x200B;**同期を有効**&#x200B;にします。

Salesforceで連絡先が契約書に追加されたときにトリガーする場合は、連絡先のオブジェクトに対して&#x200B;**同期**&#x200B;を有効にします。

Salesforceでアカウントが契約書に追加されたときにトリガーする場合は、「アカウント」のオブジェクトに対して&#x200B;**同期**&#x200B;を有効にします。

1. 目的の親（リード、取引先担当者、または取引先企業）の下に表示されるカスタムオブジェクトに対して&#x200B;**同期を有効にする**。

   ![カスタムオブジェクト](assets/customObjects.png)

1. 次のアセットは、**同期を有効にする**&#x200B;方法を示しています。

   ![カスタム同期1](assets/customObjectSync1.png)

   ![カスタム同期2](assets/customObjectSync2.png)

1. カスタムオブジェクトの同期の有効化が完了したら、同期を再アクティベートします。

   ![グローバルを有効にする](assets/enableGlobal.png)

## プログラムの作成

1. Marketoの「マーケティング活動」セクションで、左側のバーの&#x200B;**マーケティング活動**&#x200B;を右クリックし、**新規キャンペーンフォルダー**&#x200B;を選択して、名前を付けます。

   ![新しいフォルダー](assets/newFolder.png)

1. 作成されたフォルダーを右クリックし、**新規プログラム**&#x200B;を選択して、名前を付けます。 その他はすべて既定のままにして、[**作成**]をクリックします。

   ![新しいプログラム1](assets/newProgram1.png)

   ![新しいプログラム2](assets/newProgram2.png)

## Twilio SMSの設定

まず、有効なTwilioアカウントがあり、必要なSMS機能を購入していることを確認します。

Marketoの設定 – Twilio SMS webhookには、アカウントから3つのTwilioパラメーターが必要です。

- アカウントSID
- アカウントトークン
- Twilioの電話番号

これらのパラメーターをアカウントから取得して、Marketoインスタンスを開きます。

1. 右上の&#x200B;**管理者**&#x200B;をクリックします。

   ![管理者](assets/adminTab.png)

1. **Webhook**&#x200B;をクリックし、次に&#x200B;**新しいWebhook**&#x200B;をクリックします。

   ![Webhooks](assets/webhooks.png)

1. **Webhook名**&#x200B;と&#x200B;**説明**&#x200B;を入力します。

1. 次のURLを入力して、**[ACCOUNT_SID]**&#x200B;と&#x200B;**[AUTH_TOKEN]**&#x200B;をTwilio資格情報に置き換えてください。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. リクエストの種類として「**POST**」を選択します。

1. 次の&#x200B;**テンプレート**&#x200B;を入力し、**[MY_TWILIO_NUMBER]**&#x200B;をTwilioの電話番号に、**[YOUR_MESSAGE]**&#x200B;を任意のメッセージにそれぞれ置き換えてください。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 「リクエストトークンエンコーディング」を「Form/URL」に設定します。

1. 応答の種類をJSONに設定し、[**保存**]をクリックします。

## スマートキャンペーントリガーの設定

1. [マーケティング活動]セクションで、作成したプログラムを右クリックし、[**新しいスマートキャンペーン**]を選択します。

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 名前を付けて、「**作成**」をクリックします。

   ![スマートキャンペーン2](assets/smartCampaign3.png)

   カスタムオブジェクト同期の設定が正しく行われた場合、Salesforceフォルダーに次のトリガーが表示され、使用できる必要があります。

1. 「契約書に追加」をクリックして、スマートリストにドラッグします。 トリガーに設定する制約を追加します。

   ![契約書2](assets/addedToAgreement2.png)に追加されました

## スマートキャンペーンフローの設定

1. スマートキャンペーンの「**フロー**」タブをクリックします。 **Webhook呼び出し**&#x200B;フローを検索してキャンバスにドラッグし、前のセクションで作成したwebhookを選択します。

   ![Webhookの呼び出し](assets/callWebhook.png)

1. 契約書に追加されたリードのSMS通知キャンペーンが設定されました。

>[!TIP]
>
>このチュートリアルは、Experience Leagueで無料で利用できる[SalesforceおよびMarketo向けAcrobat Signを使用して、販売サイクルを加速する](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)コースの一部です。