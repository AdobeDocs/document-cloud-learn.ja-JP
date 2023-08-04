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
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Microsoft Dynamics 365およびMarketo向けAcrobat Signを使用した通知の送信

Acrobat Signテキストメッセージ、電子メール、またはプッシュ通知を送信して、Microsoft向けAcrobat Sign Dynamic、Marketo、Marketo Microsoft Dynamics Syncを使用して契約書が処理中であることを署名者に知らせる方法について説明します。 Marketoから通知を送信するには、まずMarketo SMS管理機能を購入または設定する必要があります。 このチュートリアルでは、 [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)ただし、他のMarketo SMSソリューションも利用できます。

## 前提条件

1. Marketo Microsoft Dynamics Syncをインストールします。

   Microsoft Dynamics Syncに関する情報と最新のプラグインを入手できます [はい。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Microsoft Dynamics向けAcrobat Signをインストールします。

   このプラグインに関する情報が利用可能です [はい。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## カスタムオブジェクトの検索

Marketo Microsoft Dynamics SyncとAcrobat Sign for Dynamicsの設定が完了すると、Marketo管理ターミナルに2つの新しいオプションが表示されます。

![管理者](assets/adminTerminal.png)

* クリック **[!UICONTROL Dynamicsエンティティの同期]**.

  カスタムエンティティを同期する前に、同期を無効にする必要があります。 クリック **[!UICONTROL スキーマの同期]** 初めてお使いの場合 それ以外の場合は、 **[!UICONTROL スキーマの更新]**.

  ![更新](assets/refreshSchema.png)

## カスタムオブジェクトの同期

1. 右側で、次の項目を探します。 [!UICONTROL 鉛], [!UICONTROL 連絡先]、および [!UICONTROL アカウント]ベースのカスタムオブジェクト。

   * **[!UICONTROL 同期を有効にする]** は、Dynamicsでリードが契約書に追加されたときにトリガーする場合に「リード」の下にあるオブジェクトに適用されます。

   * **[!UICONTROL 同期を有効にする]** （Dynamicsで取引先担当者が契約書に追加されたときにトリガーする場合の取引先担当者のオブジェクト）。

   * **[!UICONTROL 同期を有効にする]** をクリックします。

   * **同期を有効にする** 対象の親（リード、取引先担当者、または取引先企業）の下にある契約オブジェクトの場合。

   ![カスタムオブジェクト](assets/enableSyncDynamics.png)

1. 新しいウィンドウで、「契約書」の下で必要なプロパティを選択します。

   下のボックスを有効にする **[!UICONTROL 制約]** および **[!UICONTROL トリガー]** をクリックして、マーケティング活動に公開します。

   ![カスタム同期1](assets/entitySync1.png)

   ![カスタム同期2](assets/entitySync2.png)

1. カスタムオブジェクトで同期を有効にした後、同期を再アクティベートします。

   ページに戻る [!UICONTROL 管理ターミナル]を選択し、 **[!UICONTROL Microsoft Dynamics]**&#x200B;を選択し、 **[!UICONTROL 同期を有効にする]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![グローバルを有効化](assets/enableGlobalDynamics.png)

## プログラムの作成

1. イン [!UICONTROL マーケティング活動]、右クリック **[!UICONTROL マーケティング活動]** 左側のバーで、 **[!UICONTROL 新規キャンペーンフォルダー]**、名前を入力します。

   ![新規フォルダー](assets/newFolder.png)

1. 作成したフォルダを右クリックし、 **[!UICONTROL 新しいプログラム]**&#x200B;名前を付けてください。

   それ以外をデフォルトのままにして、 **[!UICONTROL 作成]**.

   ![新規プログラム1](assets/newProgram1.png)

   ![新規プログラム2](assets/newProgram2.png)

## 設定 [!DNL Twilio] SMS

まず、アクティブになっていることを確認します [!DNL Twilio] 必要なSMS機能をアカウントに登録して購入します。

Marketoの設定 –  [!DNL Twilio] SMS webhookには3つ必要です [!DNL Twilio] アカウントからのパラメーター。

* アカウントSID
* アカウントトークン
* Twilioの電話番号

これらのパラメーターをアカウントから取得して、Marketoインスタンスを開きます。

1. クリック **[!UICONTROL 管理者]** をクリックします。

   ![管理者](assets/adminTab.png)

1. クリック **[!UICONTROL Webhooks]**&#x200B;を選択し、 **[!UICONTROL 新しいWebhook]**.

   ![Webhooks](assets/webhooks.png)

1. Aを入力 **[!UICONTROL Webhook名]** および **[!UICONTROL 説明]**.

1. 次のURLを入力し、必ず `ACCOUNT_SID` および `AUTH_TOKEN` を [!DNL Twilio] 資格情報。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選択 **[!UICONTROL POST]** をリクエストのタイプとして使用します。

1. 次のように入力します **テンプレート** を置き換えます `MY_TWILIO_NUMBER` を [!DNL Twilio] 電話番号と `YOUR_MESSAGE` あなたの選んだメッセージで

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 設定する **[!UICONTROL 要求トークンのエンコード]** から *フォーム/URL*.

1. 応答タイプをに設定 *JSON* 次に **[!UICONTROL 保存]**.

## スマートキャンペーントリガーの設定

1. 「マーケティング活動」セクションで、作成したプログラムを右クリックして「 **[!UICONTROL 新しいスマートキャンペーン]**.

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 名前を付けて、 **[!UICONTROL 作成]**.

   ![スマートキャンペーン2](assets/smartCampaign3.png)

   Microsoftフォルダーには、使用可能ないくつかのトリガーが表示されます。

1. クリック&amp;ドラッグ **[!UICONTROL 契約書に追加されました]** を **[!UICONTROL スマート・リスト]**&#x200B;次に、トリガーに設定する制約を追加します。

   ![契約書に追加されました](assets/addedToAgreementDynamics.png)

## スマートキャンペーンフローの設定

1. 「 **[!UICONTROL 流量]** タブを [!UICONTROL スマートキャンペーン].

   検索してドラッグ **Webhookを呼び出し** キャンバスに流し込み、前のセクションで作成したwebhookを選択します。

   ![Webhookを呼び出し](assets/callWebhook.png)

1. 契約書に追加されたリードのSMS通知キャンペーンが設定されました。
>[!TIP]
>
>このチュートリアルはコースの一部です [Microsoft DynamicsおよびMarketo向けのAcrobat Signを使用して、販売サイクルを短縮](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) それはExperience Leagueで無料で入手できます！