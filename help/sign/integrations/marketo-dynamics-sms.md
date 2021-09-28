---
title: Microsoft Dynamics 365およびMarketo用Adobe Signを使用して通知を送信する
description: 署名者に契約が進行中であることを知らせるために、テキストメッセージ、電子メール、またはプッシュ通知を送信する方法を説明します
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Microsoft Dynamics 365およびMarketo用Adobe Signを使用して通知を送信する

Adobe Sign、Adobe Sign for Microsoft Dynamic、Marketo、およびMarketo Microsoft Dynamics Syncを使用して契約が途中であることを署名者に知らせるために、テキストメッセージ、電子メール、またはプッシュ通知を送信する方法を説明します。 Marketoから通知を送信するには、まずMarketo SMS管理機能を購入または構成する必要があります。 このチュートリアルでは、[Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)を使用しますが、他のMarketo SMSソリューションも利用できます。

## 前提条件

1. Marketo Microsoft Dynamics Syncをインストールします。

   Microsoft Dynamics Syncの情報と最新のプラグインは、[ここで入手できます。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Microsoft Dynamics用Adobe Signをインストールします。

   このプラグインに関する情報は、[ここで入手できます。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## カスタムオブジェクトを検索する

Marketo Microsoft Dynamics SyncとAdobe Sign for Dynamicsの構成が完了すると、Marketo管理者ターミナルに2つの新しいオプションが表示されます。

![管理者](assets/adminTerminal.png)

* [**[!UICONTROL ダイナミクスエンティティ] [同期]**]をクリックします。

   カスタムエンティティを同期する前に、同期を無効にする必要があります。 初めての場合は、[**[!UICONTROL スキーマの同期]**]をクリックします。 それ以外の場合は、**[!UICONTROL [スキーマの更新]]**&#x200B;をクリックします。

   ![更新](assets/refreshSchema.png)

## カスタムオブジェクトを同期する

1. 右側で、[!UICONTROL リード]、[!UICONTROL 連絡先]、[!UICONTROL アカウント]ベースのカスタムオブジェクトを探します。

   * **[!UICONTROL Dynamicsで]** リードが免除承諾に追加されたときにトリガーする場合は、「リード」の下のオブジェクトに対して「同期」を有効にします。

   * **[!UICONTROL Dynamicsで]** 契約に連絡先が追加されたときにトリガーする場合は、[連絡先]の下のオブジェクトに対して[同期]を有効にします。

   * **[!UICONTROL Dynamicsでアカウ]** ントが免除承諾に追加されたときにトリガーする場合は、[アカウント]の下のオブジェクトに対して[同期]を有効にします。

   * **希望す** る親（リード、連絡先、またはアカウント）の下で、契約オブジェクトの同期を有効にします。

   ![カスタムオブジェクト](assets/enableSyncDynamics.png)

1. 新しいウィンドウで、[契約]で必要なプロパティを選択します。

   **[!UICONTROL 制約]**&#x200B;と&#x200B;**[!UICONTROL トリガー]**&#x200B;の下のボックスを有効にして、マーケティング活動に公開します。

   ![カスタム同期1](assets/entitySync1.png)

   ![カスタム同期2](assets/entitySync2.png)

1. カスタムオブジェクトで同期を有効にした後、同期を再アクティブ化します。

   [!UICONTROL 管理端末]に戻り、**[!UICONTROL Microsoft Dynamics]**&#x200B;をクリックし、**[!UICONTROL [同期を有効にする]]**&#x200B;をクリックします。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![グローバルを有効にする](assets/enableGlobalDynamics.png)

## プログラムの作成

1. [!UICONTROL 「マーケティング活動」]で、左側のバーの&#x200B;**[!UICONTROL 「マーケティング活動」]**&#x200B;を右クリックし、**[!UICONTROL 「新しいキャンペーンフォルダ」]**&#x200B;を選択して名前を付けます。

   ![新しいフォルダ](assets/newFolder.png)

1. 作成したフォルダを右クリックし、[**[!UICONTROL 新しいプログラム]**]を選択して、名前を付けます。

   他の設定はデフォルトのままにし、**[!UICONTROL 作成]**&#x200B;をクリックします。

   ![新しいプログラム1](assets/newProgram1.png)

   ![新しいプログラム2](assets/newProgram2.png)

## [!DNL Twilio] SMSを設定します。

まず、[!DNL Twilio]アカウントがアクティブで、必要なSMS機能を購入します。

Marketo - [!DNL Twilio] SMS Webフックを設定するには、アカウントから3つの[!DNL Twilio]パラメータが必要です。

* アカウントSID
* アカウントトークン
* Twilio電話番号

アカウントからこれらのパラメータを取得し、Marketoインスタンスを開きます。

1. 右上の&#x200B;**[!UICONTROL Admin]**&#x200B;をクリックします。

   ![管理者](assets/adminTab.png)

1. **[!UICONTROL Webhooks]**&#x200B;をクリックし、**[!UICONTROL 新しいWebhook]**&#x200B;をクリックします。

   ![Webhooks](assets/webhooks.png)

1. **[!UICONTROL Webhook名]**&#x200B;と&#x200B;**[!UICONTROL 説明]**&#x200B;を入力します。

1. 次のURLを入力し、`ACCOUNT_SID`と`AUTH_TOKEN`を[!DNL Twilio]の資格情報で置き換えてください。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. リクエスト・タイプとして&#x200B;**[!UICONTROL POST]**&#x200B;を選択します。

1. 次の&#x200B;**テンプレート**&#x200B;を入力し、`MY_TWILIO_NUMBER`を[!DNL Twilio]の電話番号に、`YOUR_MESSAGE`を選択したメッセージに置き換えてください。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. **[!UICONTROL Request Token Encoding]**&#x200B;を&#x200B;*Form/URL*&#x200B;に設定します。

1. 応答の種類を&#x200B;*JSON*&#x200B;に設定し、**[!UICONTROL 保存]**&#x200B;をクリックします。

## スマート・キャンペーン・トリガーの設定

1. 「マーケティング活動」セクションで、作成したプログラムを右クリックし、「**[!UICONTROL 新規スマート・キャンペーン]**」を選択します。

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 名前を付け、[**[!UICONTROL 作成]**]をクリックします。

   ![スマートキャンペーン2](assets/smartCampaign3.png)

   Microsoftフォルダの下に、使用可能なトリガがいくつか表示されます。

1. [**[!UICONTROL 契約]**&#x200B;に追加]をクリックして&#x200B;**[!UICONTROL スマート・リスト]**&#x200B;にドラッグし、トリガーに適用する制約を追加します。

   ![契約に追加](assets/addedToAgreementDynamics.png)

## スマート・キャンペーン・フローの設定

1. [!UICONTROL スマートキャンペーン]の&#x200B;**[!UICONTROL 「フロー]**」タブをクリックします。

   **Call Webhook**&#x200B;フローを検索してキャンバスにドラッグし、前のセクションで作成したWebhookを選択します。

   ![Webhookの呼び出し](assets/callWebhook.png)

1. 契約に追加された潜在顧客に対するSMS通知キャンペーンが設定されました。
>[!TIP]
>
>このチュートリアルは、エクスペリエンスリーグで無料で入手できるAdobe Sign for Microsoft Dynamics and Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)を使用して、コース[セールスサイクルを短縮するコースの一部です。