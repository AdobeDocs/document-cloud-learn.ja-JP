---
title: Salesforce 用Acrobat SignおよびMarketoを使用した通知の送信
description: テキストメッセージ、電子メール、プッシュ通知を送信して、署名者に契約書が署名中であることを知らせる方法を説明します。
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: ad54f7afa78b0fbb31eccf455723a8890cb92355
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Acrobat Sign for [!DNL Salesforce] および [!DNL Marketo]

Acrobat Sign、Salesforce 用Acrobat Sign、Marketo、Marketo Salesforce の同期を使用して、契約書が署名者に送信されていることを知らせるテキストメッセージ、電子メール、プッシュ通知の送信方法について説明します。 Marketoから通知を送信するには、まずMarketo SMS 管理機能を購入するか、設定する必要があります。 このチュートリアルでは [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)その他のMarketo SMS ソリューションも利用できます。

## 前提条件

1. Marketo Salesforce Sync をインストールします。

   情報と Salesforce Sync 用の最新プラグインが利用可能です [はい。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Salesforce 用Acrobat Signをインストールします。

   このプラグインに関する情報は利用可能です [はい。](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## カスタムオブジェクトの検索

Marketo Salesforce 同期と Salesforce 用Acrobat Signの設定が完了すると、Marketo管理ターミナルにいくつかの新しいオプションが表示されます。

![管理者](assets/adminTab.png)

![Object Sync](assets/salesforceAdmin.png)

1. クリック **スキーマの同期** 初めての方は。 それ以外の場合は、「 **スキーマの更新**&#x200B;を選択します。

   ![更新](assets/refreshSchema1.png)

1. グローバル同期が実行されている場合は、「 **グローバル同期を無効にする**&#x200B;を選択します。

   ![無効にする](assets/disableGlobal.png)

1. クリック **スキーマの更新**&#x200B;を選択します。

   ![更新 2](assets/refreshSchema2.png)

## カスタムオブジェクトの同期

右側のセクションでは、リード、コンタクト、アカウントベースのカスタムオブジェクトを参照してください。

**同期を有効にする** Salesforce の契約書にリードが追加されたときにトリガーする場合は、リードの下にあるオブジェクトに対して実行します。

**同期を有効にする** Salesforce の契約書に取引先担当者が追加されたときにトリガーする場合は、「取引先担当者」の下にあるオブジェクトに対して実行します。

**同期を有効にする** Salesforce の契約書にアカウントが追加されたときにトリガーする場合は、アカウントの下にあるオブジェクトに対して実行します。

1. **同期を有効にする** をクリックします。

   ![カスタムオブジェクト](assets/customObjects.png)

1. 次のアセットは、 **同期を有効にする**&#x200B;を選択します。

   ![カスタム同期 1](assets/customObjectSync1.png)

   ![カスタム同期 2](assets/customObjectSync2.png)

1. カスタムオブジェクトの同期の有効化が終了したら、同期を再アクティブ化します。

   ![グローバルを有効にする](assets/enableGlobal.png)

## プログラムの作成

1. Marketoの「Marketing Activities」セクションで、 **マーケティング活動** 左側のバーで、「 **新しいキャンペーンフォルダー**&#x200B;に名前を付けます。

   ![新規フォルダー](assets/newFolder.png)

1. 作成したフォルダを右クリックし、「 **新規プログラム**&#x200B;に名前を付けます。 その他はすべてデフォルトのままにして、「 **作成**&#x200B;を選択します。

   ![新規プログラム 1](assets/newProgram1.png)

   ![新しいプログラム 2](assets/newProgram2.png)

## Twilio SMS の設定

まず、アクティブな Twilio アカウントがあり、必要な SMS 機能を購入したことを確認します。

Marketo - Twilio SMS webhook の設定には、アカウントから 3 つの Twilio パラメーターが必要です。

- アカウント SID
- アカウントトークン
- Twilio 電話番号

アカウントからこれらのパラメーターを取得し、Marketoインスタンスを開きます。

1. クリック **管理者** をクリックします。

   ![管理者](assets/adminTab.png)

1. クリック **Webhooks**&#x200B;を選択します **新しい Webhook**&#x200B;を選択します。

   ![Webhooks](assets/webhooks.png)

1. Enter a **Webhook 名** および **説明**&#x200B;を選択します。

1. 次の URL を入力し、 **[ACCOUNT_SID]** および **[AUTH_TOKEN]** Twilio の認証情報を使用します。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選択 **POST** をリクエストの種類に指定します。

1. 以下を入力します **テンプレート** 必ず **[MY_TWILIO_NUMBER]** Twilio の電話番号と **[YOUR_MESSAGE]** お好みのメッセージを添えて

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 「要求トークンエンコーディング」を「フォーム/URL」に設定します。

1. 応答タイプを JSON に設定し、「 **保存**&#x200B;を選択します。

## スマートキャンペーントリガーの設定

1. 「Marketing Activities」セクションで、作成したプログラムを右クリックし、「 **新しいスマートキャンペーン**&#x200B;を選択します。

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. 名前を入力して、「 **作成**&#x200B;を選択します。

   ![Smart Campaign 2](assets/smartCampaign3.png)

   カスタムオブジェクト同期の設定が正しく完了している場合は、Salesforce フォルダーで次のトリガーを使用できます。

1. 「契約書に追加」をクリックして、スマートリストにドラッグします。 トリガーに必要な制約を追加します。

   ![契約書 2 に追加](assets/addedToAgreement2.png)

## スマート・キャンペーン・フローの設定

1. ツールバーの「 **流量** タブをクリックします。 テキストを検索して **Webhook の呼び出し** カンバスにフローし、前のセクションで作成した webhook を選択します。

   ![Webhook の呼び出し](assets/callWebhook.png)

1. 契約書に追加されたリードに対する SMS 通知キャンペーンが設定されました。

>[!TIP]
>
>このチュートリアルはコースの一部です [Salesforce 向けAcrobat SignとMarketoで販売サイクルを加速](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) それは無料で利用できますExperience League!