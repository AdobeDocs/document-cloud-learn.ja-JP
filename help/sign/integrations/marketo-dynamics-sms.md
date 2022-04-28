---
title: Acrobat Sign for Microsoft Dynamics 365 およびMarketoを使用した通知の送信
description: テキストメッセージ、電子メール、プッシュ通知を送信して、署名者に契約書が署名中であることを知らせる方法を説明します。
role: Admin
product: acrobat sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: f63e7630f43cf7a5d049c286458f9f3549b29869
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Acrobat Sign for Microsoft Dynamics 365 およびMarketoを使用した通知の送信

Acrobat Sign、Microsoft Dynamic 向けAcrobat Sign、Marketo、Marketo Microsoft Dynamics Sync を使用して、テキストメッセージ、電子メール、プッシュ通知を送信し、署名者に契約書が処理中であることを知らせる方法を説明します。 Marketoから通知を送信するには、まずMarketo SMS 管理機能を購入するか、設定する必要があります。 このチュートリアルでは [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)その他のMarketo SMS ソリューションも利用できます。

## 前提条件

1. Marketo Microsoft Dynamics Sync をインストールします。

   Microsoft Dynamics Sync の情報と最新のプラグインを利用できます [はい。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Microsoft Dynamics 用Acrobat Signをインストールします。

   このプラグインに関する情報は利用可能です [はい。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## カスタムオブジェクトの検索

Marketo Microsoft Dynamics 同期とAcrobat Sign for Dynamics の設定が完了すると、Marketo Admin Terminal に 2 つの新しいオプションが表示されます。

![管理者](assets/adminTerminal.png)

* クリック **[!UICONTROL Dynamics エンティティの同期]**&#x200B;を選択します。

   カスタムエンティティを同期する前に、同期を無効にする必要があります。 クリック **[!UICONTROL スキーマの同期]** 初めての方は。 それ以外の場合は、「 **[!UICONTROL スキーマの更新]**&#x200B;を選択します。

   ![更新](assets/refreshSchema.png)

## カスタムオブジェクトの同期

1. 右側で、 [!UICONTROL リード], [!UICONTROL 連絡先]および [!UICONTROL アカウント]を参照してください。

   * **[!UICONTROL 同期を有効にする]** Dynamics の契約書にリードが追加されたときにトリガーする場合は、「リード」の下にあるオブジェクトに対して実行します。

   * **[!UICONTROL 同期を有効にする]** Dynamics の契約書に取引先担当者が追加されたときにトリガーする場合は、「取引先担当者」の下にあるオブジェクトに対して実行します。

   * **[!UICONTROL 同期を有効にする]** を使用します。

   * **同期を有効にする** をクリックします。

   ![カスタムオブジェクト](assets/enableSyncDynamics.png)

1. 新しいウィンドウの「契約」で、必要なプロパティを選択します。

   下のボックスを有効にします **[!UICONTROL 制約]** および **[!UICONTROL トリガー]** マーケティング活動に公開します。

   ![カスタム同期 1](assets/entitySync1.png)

   ![カスタム同期 2](assets/entitySync2.png)

1. カスタムオブジェクトの同期を有効にした後、同期を再度有効にします。

   再び [!UICONTROL 管理ターミナル]を選択し、「 **[!UICONTROL Microsoft Dynamics]**」を選択し、「 **[!UICONTROL 同期を有効にする]**&#x200B;を選択します。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![グローバルを有効にする](assets/enableGlobalDynamics.png)

## プログラムの作成

1. 入力 [!UICONTROL マーケティング活動]を右クリックします **[!UICONTROL マーケティング活動]** 左側のバーで、「 **[!UICONTROL 新しいキャンペーンフォルダー]**&#x200B;に名前を付けます。

   ![新規フォルダー](assets/newFolder.png)

1. 作成したフォルダを右クリックし、「 **[!UICONTROL 新規プログラム]**&#x200B;に名前を付けます。

   その他はすべてデフォルトのままにして、「 **[!UICONTROL 作成]**&#x200B;を選択します。

   ![新規プログラム 1](assets/newProgram1.png)

   ![新しいプログラム 2](assets/newProgram2.png)

## 設定 [!DNL Twilio] SMS

まず、アクティブな [!DNL Twilio] アカウントを作成し、必要な SMS 機能を購入した。

Marketoの設定 — [!DNL Twilio] SMS Webhook には 3 つ必要です [!DNL Twilio] パラメーターを使用します。

* アカウント SID
* アカウントトークン
* Twilio 電話番号

アカウントからこれらのパラメーターを取得し、Marketoインスタンスを開きます。

1. クリック **[!UICONTROL 管理者]** をクリックします。

   ![管理者](assets/adminTab.png)

1. クリック **[!UICONTROL Webhooks]**&#x200B;を選択し、「 **[!UICONTROL 新しい Webhook]**&#x200B;を選択します。

   ![Webhooks](assets/webhooks.png)

1. Enter a **[!UICONTROL Webhook 名]** および **[!UICONTROL 説明]**&#x200B;を選択します。

1. 次の URL を入力し、 `ACCOUNT_SID` および `AUTH_TOKEN` を [!DNL Twilio] 資格情報。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選択 **[!UICONTROL POST]** をリクエストの種類に指定します。

1. 以下を入力します **テンプレート** 必ず `MY_TWILIO_NUMBER` を [!DNL Twilio] 電話番号と `YOUR_MESSAGE` お好みのメッセージを添えて

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 設定 **[!UICONTROL 要求トークンエンコーディング]** を *フォーム/URL*&#x200B;を選択します。

1. 応答の種類を *JSON* 次に、「 **[!UICONTROL 保存]**&#x200B;を選択します。

## スマートキャンペーントリガーの設定

1. 「Marketing Activities」セクションで、作成したプログラムを右クリックし、「 **[!UICONTROL 新しいスマートキャンペーン]**&#x200B;を選択します。

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. 名前を入力して、「 **[!UICONTROL 作成]**&#x200B;を選択します。

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Microsoftフォルダーの下に、使用可能なトリガーがいくつか表示されます。

1. クリック&amp;ドラッグ **[!UICONTROL 契約書に追加]** を **[!UICONTROL スマート・リスト]**&#x200B;を選択し、トリガーに対して必要な制約を追加します。

   ![契約書に追加](assets/addedToAgreementDynamics.png)

## スマート・キャンペーン・フローの設定

1. ツールバーの「 **[!UICONTROL 流量]** タブを [!UICONTROL Smart Campaign]を選択します。

   テキストを検索して **Webhook の呼び出し** カンバスにフローし、前のセクションで作成した webhook を選択します。

   ![Webhook の呼び出し](assets/callWebhook.png)

1. 契約書に追加されたリードに対する SMS 通知キャンペーンが設定されました。
>[!TIP]
>
>このチュートリアルはコースの一部です [Acrobat Sign for Microsoft Dynamics とMarketoで販売サイクルを加速](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) それは無料で利用できますExperience League!