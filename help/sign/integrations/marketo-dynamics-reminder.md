---
title: Acrobat Sign for Microsoft Dynamics 365 およびMarketoを使用したリマインダーの送信
description: 一定期間が経過しても契約書が署名されていない場合に、電子メールでリマインダーを送信する方法を説明します。
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# Acrobat Sign for Microsoft Dynamics 365 およびMarketoを使用したリマインダーの送信

一定期間が経過しても契約書が署名されていない場合に、電子メールでリマインダーを送信する方法を説明します。 この統合では、Acrobat Sign、Microsoft Dynamics 用Acrobat Sign、Marketo、Marketo Microsoft Dynamics 同期を使用します。

## 前提条件

1. Marketo Microsoft Dynamics Sync をインストールします。

   Microsoft Dynamics Sync の情報と最新のプラグインを利用できます [はい。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Install [Microsoft Dynamics 用Acrobat Sign](https://appsource.microsoft.com/ja-jp/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86)を選択します。

   このプラグインに関する情報は利用可能です [はい。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## カスタムオブジェクトの検索

Marketo Microsoft Dynamics 同期とAcrobat Sign for Dynamics の設定が完了すると、Marketo Admin Terminal に 2 つの新しいオプションが表示されます。

![管理者](assets/adminTerminal.png)

1. クリック **[!UICONTROL Dynamics エンティティの同期]**&#x200B;を選択します。

   カスタムエンティティを同期する前に、同期を無効にする必要があります。 クリック **スキーマの同期** 初めての方は。 それ以外の場合は、「 **スキーマの更新**&#x200B;を選択します。

   ![更新](assets/refreshSchema.png)

## カスタムオブジェクトの同期

1. 右側で、 [!UICONTROL リード], [!UICONTROL 連絡先]および [!UICONTROL アカウント]を参照してください。

   * **同期を有効にする** 」を **[!UICONTROL リード]** 次の場合にリマインダーを送信する場合： [!UICONTROL リード] は Dynamics で契約書に署名していません。

   * **同期を有効にする** 」を **[!UICONTROL 連絡先]** 次の場合にリマインダーを送信する場合： [!UICONTROL 連絡先] は Dynamics で契約書に署名していません。

   * **同期を有効にする** 」を **[!UICONTROL アカウント]** 次の場合にリマインダーを送信する場合： [!UICONTROL アカウント] は Dynamics で契約書に署名していません。

   * **同期を有効にする** 」を入力します。 **[!UICONTROL 親]** ([!UICONTROL リード], [!UICONTROL 連絡先]、または [!UICONTROL アカウント])。

   ![カスタムオブジェクト](assets/enableSyncDynamics.png)

1. 新しいウィンドウの「契約書」で必要なプロパティを選択し、「 **制約** および **トリガー** マーケティング活動に公開します。

   ![カスタム同期 1](assets/entitySync1.png)

   ![カスタム同期 2](assets/entitySync2.png)

1. カスタムオブジェクトの同期を有効にした後、同期を再度有効にします。

   管理ターミナルに戻り、「 **Microsoft Dynamics**」を選択し、「 **同期を有効にする**&#x200B;を選択します。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![グローバルを有効にする](assets/enableGlobalDynamics.png)

## プログラムとトークンの作成

1. Marketoの「Marketing Activities」セクションで、 **マーケティング活動** をクリックします。

   選択 **新しいキャンペーンフォルダー**&#x200B;に名前を付けます。

   ![新規フォルダー](assets/newFolder.png)

1. 作成したフォルダを右クリックし、「 **新規プログラム**&#x200B;に名前を付けます。

   その他はすべてデフォルトのままにして、「 **作成**&#x200B;を選択します。

   ![新規プログラム 1](assets/newProgram1.png)

   ![新しいプログラム 2](assets/newProgram2.png)

1. クリック **マイトークン**&#x200B;ドラッグします **電子メールスクリプト** キャンバスに移動します。

   ![電子メールスクリプト](assets/emailScript.png)

1. ファイル名を指定して、「 **クリックして編集**&#x200B;を選択します。

   ![名前を付けて編集](assets/nameAndSave.png)

1. 展開 **[!UICONTROL カスタムオブジェクト]** 右側で、 **[!UICONTROL 契約書]** します。

   検索とドラッグ [!UICONTROL 名前]、契約状況、送信日、現在の署名者の URL がキャンバスに表示されます。

1. これらのトークンを使用して Velocity スクリプトを記述し、1 週間署名されていない契約書の契約書 URL を表示します。 次に、現在の日付と送信日を比較する例を示します。

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

## リマインダーの作成とパーソナライゼーションの追加

パーソナライゼーションの例は次のとおりです。署名者の名前、契約書の名前、契約書へのリンクなど

1. 作成したプログラムを右クリックし、「 **[!UICONTROL 新しいローカルアセット]**&#x200B;を選択し、 **[!UICONTROL 電子メール]**&#x200B;を選択します。

   ![新しい電子メール](assets/createNewEmail.png)

1. 新しいタブで、 **[!UICONTROL 名前]** および **[!UICONTROL 説明]** を入力し、テンプレートピッカーからテンプレートを選択します。

   ![テンプレートピッカー](assets/templatePicker.png)

1. 「**[!UICONTROL 作成]**」をクリックします。

1. 設定 **[!UICONTROL 名前から]** および **[!UICONTROL 差出人住所]**&#x200B;を選択します。

   ![リマインダーメール](assets/reminderEmail.png)

1. メッセージ本文をクリックして、エディタをアクティブにします。

   ツールバーの「 **[!UICONTROL トークンの挿入]** 」ボタンをクリックし、作成したカスタム契約書 URL トークンを見つけて、「 **[!UICONTROL 挿入]**&#x200B;を選択します。 電子メールのカスタマイズを終了し、「 **[!UICONTROL 保存]**&#x200B;を選択します。

   ![トークンの挿入](assets/insertToken.png)

1. 契約書が割り当てられているプロファイルを使用してプレビューします。

   URL へのリンクが表示され、ラベルに契約書名が表示されます。

   ![電子メールリンク](assets/emailLink.png)

## スマートキャンペーンフィルターの設定

1. 作成したプログラムを右クリックし、「 **[!UICONTROL 新しいスマートキャンペーン]**&#x200B;を選択します。

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. 名前を指定して、「 **[!UICONTROL 作成]**&#x200B;を選択します。

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. を検索し、クリック&amp;ドラッグ **[!UICONTROL 契約あり]** をスマート・リストに追加します。

   ![契約あり](assets/hasAgreementDynamics1.png)

   トリガーに公開するフィールドは、 **[!UICONTROL 拘束を追加]**&#x200B;を選択します。

1. 選択 **[!UICONTROL 契約状況]** およびフィルタに使用する他のフィールドを選択します。

   追加するフィールドごとに、フィルタの基準となる値を定義します。 この場合、トリガーされるのは、 **[!UICONTROL 契約状況]** is *署名用に送信* および **[!UICONTROL 送信日]** is *過去 1 週間前に*&#x200B;を選択します。

   ![契約書ステータス](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > 次のように、一意の識別子を拘束に追加します。 **名前**」を選択します。

1. 「スケジュール」タブでキャンペーンのオーディエンスを確認し、対象となるオーディエンスを確認します。

   ![修飾子](assets/qualifiers.png)

## スマート・キャンペーン・フローの設定

キャンペーンフィルター **有効期限までの日数** を使用した場合は、キャンペーンの定期的なスケジュールを使用できます。

1. ツールバーの「 **[!UICONTROL 流量]** タブを [!UICONTROL Smart Campaign]を選択します。

   テキストを検索して **電子メールを送信** カンバスにフローし、前のセクションで作成したリマインダーメールを選択します。

   ![電子メールを送信](assets/sendEmail.png)

1. ツールバーの「 **[!UICONTROL スケジュール]** タブをクリックします。 キャンペーンフローが、 **スマートキャンペーン設定**&#x200B;を選択します。 次に、「 **定期的なスケジュール** タブを選択します。

   ![「スケジュール」タブ](assets/scheduleTab.png)

1. 設定 **スケジュール** を _毎日_&#x200B;を選択します。 必要に応じて、キャンペーンの開始日時と終了日を選択します。

   ![スケジュール設定](assets/scheduleSettings.png)

>[!TIP]
>
>このチュートリアルはコースの一部です [Acrobat Sign for Microsoft Dynamics とMarketoで販売サイクルを加速](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) それは無料で利用できますExperience League!