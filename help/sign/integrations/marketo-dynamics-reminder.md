---
title: Microsoft Dynamics 365およびMarketo向けAcrobat Signを使用したリマインダーの送信
description: 一定期間後に契約書が未署名のままになったときに電子メールでリマインダーを送信する方法について説明します
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# Microsoft Dynamics 365およびMarketo向けAcrobat Signを使用したリマインダーの送信

一定期間後に契約書が未署名のままになったときに電子メールでリマインダーを送信する方法について説明します。 この統合には、Acrobat Sign、Microsoft Dynamics向けAcrobat Sign、Marketo、Marketo Microsoft Dynamics Syncが使用されます。

## 前提条件

1. Marketo Microsoft Dynamics Syncをインストールします。

   Microsoft Dynamics Syncに関する情報と最新のプラグインを入手できます [はい。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. インストール [Microsoft Dynamics向けAcrobat Sign](https://appsource.microsoft.com/ja-jp/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   このプラグインに関する情報が利用可能です [はい。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## カスタムオブジェクトの検索

Marketo Microsoft Dynamics SyncとAcrobat Sign for Dynamicsの設定が完了すると、Marketo管理ターミナルに2つの新しいオプションが表示されます。

![管理者](assets/adminTerminal.png)

1. クリック **[!UICONTROL Dynamicsエンティティの同期]**.

   カスタムエンティティを同期する前に、同期を無効にする必要があります。 クリック **スキーマの同期** 初めてお使いの場合 それ以外の場合は、 **スキーマの更新**.

   ![更新](assets/refreshSchema.png)

## カスタムオブジェクトの同期

1. 右側で、次の項目を探します。 [!UICONTROL 鉛], [!UICONTROL 連絡先]、および [!UICONTROL アカウント]ベースのカスタムオブジェクト。

   * **同期を有効にする** 下にある物体に対して **[!UICONTROL 鉛]** リマインダーを送信するタイミング [!UICONTROL 鉛] 様はDynamicsで契約書に署名していません。

   * **同期を有効にする** 下にある物体に対して **[!UICONTROL 連絡先]** リマインダーを送信するタイミング [!UICONTROL 連絡先] 様はDynamicsで契約書に署名していません。

   * **同期を有効にする** 下にある物体に対して **[!UICONTROL アカウント]** 次の場合にリマインダーを送信 [!UICONTROL アカウント] 様はDynamicsで契約書に署名していません。

   * **同期を有効にする** 目的の下の契約書オブジェクトの場合 **[!UICONTROL 親]** ([!UICONTROL 鉛], [!UICONTROL 連絡先]、または [!UICONTROL アカウント])を参照してください。

   ![カスタムオブジェクト](assets/enableSyncDynamics.png)

1. 新しいウィンドウで、「契約書」の下から必要なプロパティを選択し、 **制約** および **トリガー** をクリックして、マーケティング活動に公開します。

   ![カスタム同期1](assets/entitySync1.png)

   ![カスタム同期2](assets/entitySync2.png)

1. カスタムオブジェクトで同期を有効にした後、同期を再アクティベートします。

   管理ターミナルに戻り、 **Microsoft Dynamics**&#x200B;を選択し、 **同期を有効にする**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![グローバルを有効化](assets/enableGlobalDynamics.png)

## プログラムとトークンの作成

1. Marketoの「Marketing Activities」セクションで、次を右クリックします。 **マーケティング活動** をクリックします。

   選択 **新規キャンペーンフォルダー**&#x200B;名前を付けてください。

   ![新規フォルダー](assets/newFolder.png)

1. 作成したフォルダを右クリックし、 **新しいプログラム**&#x200B;名前を付けてください。

   それ以外をデフォルトのままにして、 **作成**.

   ![新規プログラム1](assets/newProgram1.png)

   ![新規プログラム2](assets/newProgram2.png)

1. をクリック **マイトークン**&#x200B;をドラッグします **電子メールスクリプト** カンバスに向かって

   ![電子メールスクリプト](assets/emailScript.png)

1. 名前を付けてからクリックしてください **クリックして編集**.

   ![名前を付けて編集](assets/nameAndSave.png)

1. 展開 **[!UICONTROL カスタムオブジェクト]** 右側で、 **[!UICONTROL 契約書]** オブジェクトです。

   検索とドラッグ [!UICONTROL 名前]、契約書のステータス、送信日、現在の署名者のUrlをキャンバスに表示します。

1. これらのトークンを使用してVelocityスクリプトを記述し、1週間署名されていない契約書の契約書URLを表示します。 現在の日付を送信日と比較する例を次に示します。

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. 「**[!UICONTROL 保存]**」をクリックします。

## リマインダーを作成してパーソナライズする

パーソナライズの例としては、署名者の名前、契約書の名前、契約書へのリンクなどがあります。

1. 作成したプログラムを右クリックし、 **[!UICONTROL 新しいローカルアセット]**&#x200B;を選択します **[!UICONTROL 電子メール]**.

   ![新しい電子メール](assets/createNewEmail.png)

1. 新しいタブで、aと入力します。 **[!UICONTROL 名前]** および **[!UICONTROL 説明]** 電子メールの場合は、テンプレートピッカーからテンプレートを選択します。

   ![テンプレートピッカー](assets/templatePicker.png)

1. 「**[!UICONTROL 作成]**」をクリックします。

1. 設定する **[!UICONTROL 名前から]** および **[!UICONTROL アドレスから]**.

   ![リマインダーメール](assets/reminderEmail.png)

1. メッセージ本文をクリックして、エディターをアクティブにします。

   アイコンをクリック **[!UICONTROL トークンの挿入]** ボタンをクリックし、作成したカスタム契約書URLトークンを見つけて、 **[!UICONTROL 挿入]**. 電子メールのカスタマイズを完了して、 **[!UICONTROL 保存]**.

   ![トークンの挿入](assets/insertToken.png)

1. 契約書が割り当てられたプロファイルを使用してプレビューする。

   契約書名をラベルとして含んだURLへのリンクが表示されます。

   ![電子メールリンク](assets/emailLink.png)

## スマートキャンペーンフィルターの設定

1. 作成したプログラムを右クリックし、 **[!UICONTROL 新しいスマートキャンペーン]**.

   ![スマートキャンペーン1](assets/smartCampaign1.png)

1. 選択した名前を入力し、 **[!UICONTROL 作成]**.

   ![スマートキャンペーン2](assets/smartCampaign2.png)

1. を検索し、クリック&amp;ドラッグします **[!UICONTROL 契約書あり]** をスマート・リストに追加します。

   ![契約書あり](assets/hasAgreementDynamics1.png)

   トリガーに公開したフィールドは、 **[!UICONTROL 拘束を追加]**.

1. 選択 **[!UICONTROL 契約書ステータス]** およびフィルターに使用するその他のフィールド。

   追加した各フィールドについて、フィルターに使用する値を定義します。 この場合、トリガーされるのは **[!UICONTROL 契約書ステータス]** が *署名用に送信* および **[!UICONTROL 送信日]** が *過去1週間以内*.

   ![契約書ステータス](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > 次のように、制約に一意の識別子を追加します **名前**&#x200B;特定の契約書に対してのみ、このキャンペーンを実行する場合は、

1. 「スケジュール」タブで、キャンペーン対象ユーザーを確認し、資格を付与するユーザーを確認します。

   ![修飾子](assets/qualifiers.png)

## スマートキャンペーンフローの設定

キャンペーンフィルターです **有効期限までの日数** が使用されました。キャンペーンに対してスケジュールされた定期的なアイテムを使用できます。

1. 「 **[!UICONTROL 流量]** タブを [!UICONTROL スマートキャンペーン].

   検索してドラッグ **電子メールを送信** キャンバスに移動し、前のセクションで作成したリマインダーメールを選択します。

   ![電子メールを送信](assets/sendEmail.png)

1. 「 **[!UICONTROL スケジュール]** タブをクリックします。 キャンペーンフローが個人に1回のみ実行されるように制限されていることを確認します。 **スマートキャンペーン設定**. 次に、 **繰り返しのスケジュール** タブをクリックします。

   ![「スケジュール」タブ](assets/scheduleTab.png)

1. 設定する **スケジュール** から _毎日_. 必要に応じて、キャンペーンの開始日時および終了日を選択します。

   ![スケジュール設定](assets/scheduleSettings.png)

>[!TIP]
>
>このチュートリアルはコースの一部です [Microsoft DynamicsおよびMarketo向けのAcrobat Signを使用して、販売サイクルを短縮](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) それはExperience Leagueで無料で入手できます！