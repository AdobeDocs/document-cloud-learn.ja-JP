---
title: Microsoft Dynamics 365およびMarketo向けAcrobat Signを使用した通知の送信
description: テキストメッセージ、電子メール、またはプッシュ通知を送信して、契約書が処理中であることを署名者に知らせる方法について説明します。
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Microsoft Dynamics 365およびMarketo向けAcrobat Signを使用した通知の送信

テキストメッセージ、電子メール、またはプッシュ通知を送信して、Microsoft向けAcrobat Sign Dynamic、Marketo Marketo、およびAcrobat Sign Microsoft Dynamics Syncを使用して契約書が処理中であることを署名者に知らせる方法について説明します。 Marketoから通知を送信するには、まずMarketo SMS管理機能を購入または設定する必要があります。 このチュートリアルでは[Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)を使用しますが、他のMarketo SMSソリューションも利用できます。

## 前提条件

1. Marketo Microsoft Dynamics Syncをインストールします。

   Microsoft Dynamics Syncの情報と最新のプラグインは、[こちら](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)から入手できます。

1. Microsoft Dynamics用Acrobat Signをインストールします。

   このプラグインに関する情報は、[こちら](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)から入手できます。

## カスタムオブジェクトの検索

Microsoft Dynamics SyncとDynamics用Acrobat SignのMarketoの設定が完了すると、Marketo管理ターミナルに2つの新しいオプションが表示されます。

![管理者](assets/adminTerminal.png)

* **[!UICONTROL Dynamicsエンティティ同期]**&#x200B;をクリックします。

  カスタムエンティティを同期する前に、同期を無効にする必要があります。 初めて使用する場合は、[**[!UICONTROL スキーマの同期]**]をクリックします。 それ以外の場合は、[**[!UICONTROL スキーマの更新]**]をクリックします。

  ![更新](assets/refreshSchema.png)

## カスタムオブジェクトの同期

1. 右側で、[!UICONTROL リード]、[!UICONTROL 取引先担当者]、および[!UICONTROL 取引先企業]ベースのカスタムオブジェクトを見つけます。

   * Dynamicsでリードが契約書に追加されたときにトリガーする場合は、リードの下にあるオブジェクトに対して&#x200B;**[!UICONTROL 同期]**&#x200B;を有効にします。

   * Dynamicsで取引先担当者が契約書に追加されたときにトリガーする場合は、取引先担当者のオブジェクトに対して&#x200B;**[!UICONTROL 同期]**&#x200B;を有効にします。

   * Dynamicsでアカウントが契約書に追加されたときにトリガーする場合は、[アカウント]の下にあるオブジェクトに対して&#x200B;**[!UICONTROL 同期]**&#x200B;を有効にします。

   * 目的の親（リード、取引先担当者、または取引先企業）の下にある契約オブジェクトの&#x200B;**同期を有効にする**。

   ![カスタムオブジェクト](assets/enableSyncDynamics.png)

1. 新しいウィンドウで、「契約書」の下で必要なプロパティを選択します。

   「**[!UICONTROL 制約]**」と「**[!UICONTROL トリガー]**」のボックスを有効にして、マーケティング活動に公開します。

   ![カスタム同期1](assets/entitySync1.png)

   ![カスタム同期2](assets/entitySync2.png)

1. カスタムオブジェクトで同期を有効にした後、同期を再アクティベートします。

   [!UICONTROL 管理ターミナル]に戻り、**[!UICONTROL Microsoft Dynamics]**&#x200B;をクリックしてから、**[!UICONTROL 同期を有効にする]**&#x200B;をクリックします。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![グローバルを有効にする](assets/enableGlobalDynamics.png)

## プログラムの作成

1. [!UICONTROL マーケティング活動]で、左側のバーの&#x200B;**[!UICONTROL マーケティング活動]**&#x200B;を右クリックし、**[!UICONTROL 新しいキャンペーンフォルダー]**&#x200B;を選択して、名前を入力します。

   ![新しいフォルダー](assets/newFolder.png)

1. 作成されたフォルダーを右クリックし、**[!UICONTROL 新規プログラム]**&#x200B;を選択して、名前を付けます。

   その他はすべて既定のままにして、[**[!UICONTROL 作成]**]をクリックします。

   ![新しいプログラム1](assets/newProgram1.png)

   ![新しいプログラム2](assets/newProgram2.png)

## [!DNL Twilio] SMSの設定

まず、アクティブな[!DNL Twilio]アカウントがあり、必要なSMS機能を購入していることを確認します。

Marketoを設定しています – [!DNL Twilio] SMS webhookには、アカウントから3つの[!DNL Twilio]パラメーターが必要です。

* アカウントSID
* アカウントトークン
* Twilioの電話番号

これらのパラメーターをアカウントから取得して、Marketoインスタンスを開きます。

1. 右上の&#x200B;**[!UICONTROL 管理者]**&#x200B;をクリックします。

   ![管理者](assets/adminTab.png)

1. **[!UICONTROL [Webhook]]**&#x200B;をクリックし、**[!UICONTROL [新しいWebhook]]**&#x200B;をクリックします。

   ![Webhooks](assets/webhooks.png)

1. **[!UICONTROL Webhook名]**&#x200B;と&#x200B;**[!UICONTROL 説明]**&#x200B;を入力します。

1. 次のURLを入力して、`ACCOUNT_SID`と`AUTH_TOKEN`を[!DNL Twilio]資格情報で置き換えてください。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. リクエストの種類として「**[!UICONTROL POST]**」を選択します。

1. 次の&#x200B;**テンプレート**&#x200B;を入力し、`MY_TWILIO_NUMBER`を[!DNL Twilio]電話番号に、`YOUR_MESSAGE`を任意のメッセージにそれぞれ置き換えてください。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. **[!UICONTROL Request Token Encoding]**&#x200B;を&#x200B;*Form/URL*&#x200B;に設定します。

1. 応答の種類を&#x200B;*JSON*&#x200B;に設定し、**[!UICONTROL [保存]]**&#x200B;をクリックしてください。

## スマートキャンペーントリガーの設定

1. [マーケティング活動]セクションで、作成したプログラムを右クリックし、[**[!UICONTROL 新しいスマートキャンペーン]**]を選択します。

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 名前を付けて、「**[!UICONTROL 作成]**」をクリックします。

   ![スマートキャンペーン2](assets/smartCampaign3.png)

   Microsoftフォルダーには、使用可能ないくつかのトリガーが表示されます。

1. 「**[!UICONTROL 契約書に追加]**」をクリックして&#x200B;**[!UICONTROL スマートリスト]**&#x200B;にドラッグし、トリガーに制約を追加します。

   ![契約書に追加されました](assets/addedToAgreementDynamics.png)

## スマートキャンペーンフローの設定

1. [!UICONTROL スマートキャンペーン]で「**[!UICONTROL フロー]**」タブをクリックします。

   **Webhook呼び出し**&#x200B;フローを検索してキャンバスにドラッグし、前のセクションで作成したwebhookを選択します。

   ![Webhookの呼び出し](assets/callWebhook.png)

1. 契約書に追加されたリードのSMS通知キャンペーンが設定されました。
