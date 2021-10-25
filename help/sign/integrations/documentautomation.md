---
title: Microsoft Power Platform のAdobe Signによる文書の自動化
description: Microsoft Power Apps 用のAdobe SignおよびAdobe PDF Tools コネクタをアクティブにして使用する方法について説明します。 ビジネスの承認と署名のプロセスを、コードを使用することなくすばやく安全に自動化するワークフローを構築できます
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 0%

---

# Adobe Sign for Microsoft Power Platform による文書の自動化

Microsoft Power Apps 用のAdobe SignおよびAdobe PDF Tools コネクタをアクティブにして使用する方法について説明します。 ビジネスの承認および署名プロセスを迅速かつ安全に、コードを入力することなく自動化するワークフローを構築できます。 この実践チュートリアルは、以下のリンク先から 4 つのパートで構成されています。

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="パート 1:署名済み契約書をAdobe SignとSharePointに保存" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>パート 1:署名済み契約書をAdobe SignとSharePointに保存</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="パート 2:Adobe Signによる電子サインの自動承認プロセス" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>パート 2:Adobe Signによる電子サインの自動承認プロセス</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="パート 3:Adobe PDF Tools による自動ドキュメント OCR" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>パート 3:Adobe PDF Tools による自動ドキュメント OCR</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="パート 4:Adobe PDF Tools による自動文書組み立て" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>パート 4:Adobe PDF Tools による自動文書組み立て</strong></a>
    </div>
  </td>
</tr>
</table>

## 前提条件

* Microsoft 365 と Power Automate の互換性
* Adobe Sign知識
* SharePointおよび Power Automate へのアクセス権を持つMicrosoft 365 アカウント (Basic for Adobe Sign、Premium for Adobe PDF Tools)
* Adobe Signエンタープライズ版またはAdobe Signデベロッパーアカウント

**演習 1 および 2**

* API にアクセスできるAdobe Signアカウント。 開発者アカウントまたはエンタープライズアカウント。
* 編集権限を持つ Power Automate がアクセスできるSharePointサイト。 完全な管理者アクセスを推奨します。
* 署名承認リクエストおよび署名用のサンプル文書。

**演習 3 および 4**

資料のダウンロード [ここ](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## パート 1:署名済み契約書をAdobe SignとSharePointに保存 {#part1}

パート 1 では、Power Automate のフローテンプレートを使用して、すべての署名済み契約書をSharePointサイトに保存する自動化ワークフローを設定します。

1. Power Automate に移動します。
1. Search for Adobe Sign.

   ![Power Automate への移動のスクリーンショット](assets/documentautomation/automation_1.png)

1. 選択 **Adobe Signの完了した契約書をSharePointライブラリに保存**&#x200B;を選択します。

   ![「Adobe Signの完了した契約書をSharePointライブラリに保存」アクションのスクリーンショット](assets/documentautomation/automation_2.png)

1. 画面を確認し、必要な接続を構成します。 Adobe Sign接続を有効にします。
1. 青をクリック `+` 記号を使用します。

   ![Adobe SignとSharePointのフロー接続のスクリーンショット](assets/documentautomation/automation_3.png)

1. Adobe Signアカウントの電子メールアドレスを入力し、新しいウィンドウでパスワードフィールドをクリックします。

   ![Adobe Signのログイン画面のスクリーンショット](assets/documentautomation/automation_4.png)

   アカウントを確認するAdobeが表示されるまでお待ちください。

   >[!NOTE]
   >
   >Adobe IDまたはアドビの企業 SSO を使用している場合は、このチェックにより適切なログインにルーティングされます。

1. ログインを完了します。
1. クリック **続行** 」をクリックしてフロー編集画面に移動します。
1. トリガーに名前を付けます。

   ![トリガー名のスクリーンショット](assets/documentautomation/automation_5.png)

1. SharePointの設定

   ![SharePoint設定のスクリーンショット](assets/documentautomation/automation_6.png)

   **サイトアドレス：** SharePoint Site
   **フォルダパス：** 使用する共有ドキュメントへのパス
   **ファイル名：** デフォルトを受け入れる
   **ファイルコンテンツ：** デフォルトを受け入れる

1. フローを保存します.

   ![保存アイコンのスクリーンショット](assets/documentautomation/automation_7.png)

1. 青い戻る矢印でフローの概要画面に移動します。 このフローはパート 2 でテストします。

   ![フローの概要画面のスクリーンショット](assets/documentautomation/automation_8.png)

次のパートでは、このフローをテストします。

## パート 2:Adobe Signによる電子サインの自動承認プロセス {#part2}

パート 2 では、最初のパートをより堅牢なフローで構築し、両方のフローをテストして動作を確認します。

1. 選択 **テンプレート** をクリックします。

   ![テンプレート選択のスクリーンショット](assets/documentautomation/automation_9.png)

1. 「マネージャーの承認」を検索します。
1. 選択 **選択したファイルに対するマネージャーの承認を要求する**&#x200B;を選択します。

   ![選択したファイルに対して「承認をリクエスト」を選択したスクリーンショット](assets/documentautomation/automation_10.png)

   接続を確認し、不足している接続を追加します。

   >[!NOTE]
   >
   >これが承認を使用して実行する最初のフローである場合、フローの実行時に完全に設定されます。

1. クリック **続行** 」をクリックしてフロー編集画面に移動します。

   このフローには、エラーチェックやネストされた条件付きステップなど、事前に設定されたステップが多数含まれます。

1. 設定 **選択したファイル** 次のように入力します。
   **サイトアドレス：** SharePointサイト
   **ライブラリ名：** 文書リポジトリ
1. 次のように入力を追加します。
   **種類**:電子メール
   **名前**:署名者の電子メール

   ![フロー設定のスクリーンショット](assets/documentautomation/automation_11.png)

1. 設定 **ファイルのプロパティを取得：** 次のように入力します。
   **サイトアドレス：** SharePointサイト
   **ライブラリ名：** 文書リポジトリ

1. 下にスクロールして、 **「はい」の場合**&#x200B;を選択します。

   ![「はい」の場合の設定のスクリーンショット](assets/documentautomation/automation_12.png)

1. クリック **アクションの追加** 」を **「はい」の場合** 」ボックスをクリックして、署名用に送信する手順を追加します。

   ![「はい」の場合にアクションを追加するスクリーンショット](assets/documentautomation/automation_13.png)

1. 検索対象 **SharePointファイルコンテンツの取得** を選択し、 **ファイルコンテンツの取得**&#x200B;を選択します。

   ![検索ボックスのスクリーンショット](assets/documentautomation/automation_14.png)

1. 以下を設定します。 **ファイルコンテンツの取得** 次のように入力します。

   ![「ファイルコンテンツを取得」設定のスクリーンショット](assets/documentautomation/automation_15.png)

   **サイトアドレス：** SharePointサイト
   **ファイル識別子：** 「identifier」を検索し、 **ファイルのプロパティの取得** 手順：
1. 「Adobe」を検索し、 **Adobe Sign** を選択して、別のアクションを追加します。

   ![検索メニューのスクリーンショット](assets/documentautomation/automation_16.png)

1. Adobe Signの検索ボックスに「upload」と入力し、「 **文書をアップロードして文書 ID を取得**&#x200B;を選択します。
1. 動的変数の検索 **名前** 」をクリックし、「 **ファイル名**&#x200B;を選択します。
1. クリック **式** 変数アシスタントの **ファイルコンテンツ**&#x200B;を選択します。

   ![「文書をアップロードして文書 ID を取得」画面のスクリーンショット](assets/documentautomation/automation_17.png)

1. アポストロフィを 1 つ追加し、「戻る」をクリックして **動的コンテンツ**&#x200B;を選択し、 **ファイルコンテンツ** を選択し、「 **OK**&#x200B;を選択します。

   以下の例のように、アポストロフィが追加されていないことを確認します。

   ![動的コンテンツ画面の外観のスクリーンショット](assets/documentautomation/automation_18.png)

1. Adobe Signの検索領域で「create」を検索して、別のAdobe Signアクションを追加します。
1. 選択 **アップロードされた文書から契約書を作成して署名用に送信**&#x200B;を選択します。

   ![「作成」を検索したスクリーンショット](assets/documentautomation/automation_19.png)

1. 必要な情報を設定します。選択 **名前** の動的変数アシスタントから **契約書名**を選択します。
選択 **文書 ID** の動的変数アシスタントから **文書 ID**を選択します。
選択 **署名者の電子メール** の動的変数アシスタントから **参加者の電子メール**を選択します。
「1」を **参加者の順序**を選択します。
選択 **署名者** ドロップダウンから **参加者ロール**&#x200B;を選択します。

   ![必要な情報のスクリーンショット](assets/documentautomation/automation_20.png)

1. **保存** を選択します。

### フローのテスト

SharePointサイトのドキュメントリポジトリに移動してテストします。

1. ドキュメントを選択し、 **自動化** および **流量** 作成されました。

   ![「自動化」メニューとフローを選択したスクリーンショット](assets/documentautomation/automation_21.png)

1. フローを開始して接続を検証します（フローの最初の実行のみ）。
1. 承認者へのわかりやすいメッセージを **メッセージ**&#x200B;を選択します。
1. 文書の署名者の電子メールを **署名者の電子メール**&#x200B;を選択します。
1. クリック **フローの実行**&#x200B;を選択します。

フローを開始するユーザーに対して設定された承認者に、承認要求が送信されます。 電子メールまたは Power Automate のアクションアイテムメニューから承認できます。
承認されたら、文書に署名します。 ユーザーと Sign にログインしている場合は、署名用のウィンドウをプライベートブラウザーウィンドウで開く必要があります。

![プライベートブラウザーウィンドウで開く画面](assets/documentautomation/automation_22.png)

署名を完了し、SharePointフォルダーに戻ります。

![SharePointフォルダーのスクリーンショット](assets/documentautomation/automation_23.png)

## パート 3:Adobe PDF Tools による自動ドキュメント OCR {#part3}

パート 3 では、Microsoft SharePointに読み込まれたPDFの OCR を自動化する方法について学習します。 SharePointで検索できないスキャンされたPDF文書で発生する問題を解決します。

![ブラウザーのPDFドキュメントのスクリーンショット](assets/documentautomation/automation_24.png)

### SharePointでのフォルダーの設定

文書を保存するMicrosoftSharePointに移動します。

1. クリック **+新規** 」をクリックして、「処理済み契約書」という新しいフォルダーを作成します。
1. クリック **+新規** 」をクリックして、「Old Contracts」という新しいフォルダーを作成します。

   ![新しいフォルダーのスクリーンショット](assets/documentautomation/automation_25.png)

これらのフォルダーは、Power Automate フローの一部として参照されるようになりました。

### テンプレートからのフローの作成

1. https://flow.microsoft.comにログインします。
1. クリック **テンプレート** を選択します。

   ![テンプレート選択のスクリーンショット](assets/documentautomation/automation_26.png)

1. 選択 **SharePointで、新しく追加したファイルを検索可能なテキストPDFに変換する**&#x200B;を選択します。
1. 次の **+** 記号をAdobe PDF Tools の横に表示します。

   ![+記号を選択したスクリーンショット](assets/documentautomation/automation_27.png)

1. 新しいタブでhttps://www.adobe.com/go/powerautomate_getstartedに移動します。
1. クリック **今すぐ始める**&#x200B;を選択します。

   ![「開始」ボタンのスクリーンショット](assets/documentautomation/automation_28.png)

1. Adobe IDでログインします。

   ![ログイン画面のスクリーンショット](assets/documentautomation/automation_29.png)

1. 資格情報の名前と説明を入力し、「 **資格情報の作成**&#x200B;を選択します。

   ![資格情報の作成画面のスクリーンショット](assets/documentautomation/automation_30.png)

   資格情報を開いた状態でウィンドウを維持します。 Microsoft Power Automate に入力する必要があります。

   ![開いたままにするためのブラウザータブのスクリーンショット](assets/documentautomation/automation_31.png)

1. 資格情報を入力し、「 **Microsoft Power Automate で作成**&#x200B;を選択します。

   ![インストールツールの資格情報を入力したPDFのスクリーンショット](assets/documentautomation/automation_32.png)

1. 「**続行**」をクリックします。

   ![「続行」をクリックする場所のスクリーンショット](assets/documentautomation/automation_33.png)

   ワークフローのビューが表示されたら、環境に合わせて設定する必要があります。

1. 「サイトアドレス」フィールドを選択し、「 **フォルダーにファイルを作成する場合**&#x200B;を選択します。

   ![「フォルダートリガーでファイルを作成するとき」を選択した場合のスクリーンショット](assets/documentautomation/automation_34.png)

1. フォルダーアイコンをクリックして、「フォルダー ID」にある「古い契約」フォルダーに移動します。

   ![「Old Contracts」フォルダを選択したスクリーンショット](assets/documentautomation/automation_35.png)

1. エレメントを **ファイルの作成** アクションをフローの下部で実行します。

   変更 **サイトアドレス** をサイトアドレスに追加します。
「フォルダ・パス」で、処理済契約フォルダの場所を指定します。

1. クリック **保存** をクリックします。
1. クリック **テスト**&#x200B;を選択します。
1. 選択 **手動**&#x200B;を選択します。
1. クリック **テスト**&#x200B;を選択します。

   ![テストフローのスクリーンショット](assets/documentautomation/automation_36.png)

### 新しいフローを試す

1. SharePointの Old Contracts フォルダーに移動します。
1. ダウンロードしたエクササイズファイルで E03/Old Contracts に移動します。
1. ReleaseFormXX.pdf ファイルをSharePointの Old Contracts フォルダーにコピーします。

   ![ファイルのコピーのスクリーンショット](assets/documentautomation/automation_37.png)

処理済み契約フォルダーに移動すると、フローの実行に少し時間がかかった後に、PDFを確認できます。 PDFを開くと、テキストが選択可能であることがわかります。
さらに、SharePointでは文書のインデックスが作成されるので、SharePointの検索バーから文書のコンテンツを検索できます。

## パート 4:Adobe PDF Tools による自動文書組み立て {#part4}

パート 4 では、Microsoft SharePointからフローを選択して開始するときに提供される情報に基づいて、多数の文書を結合する方法について学習します。 このシナリオでは、フローは次のようになります。

* お客様のパッケージに含めるものを選択するための情報を求めます。
* 提供された情報に基づいて、多くの文書を結合します。 これらの文書には、表紙とオプションのホワイトペーパーが含まれています。
* 結合されたドキュメントがSharePointに保存されます。

### エクササイズファイルのSharePointへの読み込み

1. 練習用ファイルの E04 フォルダーを開きます。
1. Proposal、Templates および Generated Docs フォルダーをSharePointに読み込みます。

   ![フォルダーの読み込みのスクリーンショット](assets/documentautomation/automation_38.png)

これらのフォルダは参照に使用されます。 特に、提案書には Proposal.docx ファイルを使用します。

Templates フォルダには、さまざまな都市の表紙デザインを含む Cobes フォルダがあります。 また、オプションで追加のホワイトペーパーを含むホワイトペーパーフォルダーも用意されています。このフォルダーを選択すると、最後に追加のホワイトペーパーが追加されます。

### フローをMicrosoft Power Automate に読み込む

1. Microsoft Power Automate(https://flow.microsoft.com) にログインします。
1. クリック **マイフロー**&#x200B;を選択します。

   ![「マイフロー」を選択する場所のスクリーンショット](assets/documentautomation/automation_39.png)

1. クリック **読み込み**&#x200B;を選択します。

   ![読み込み画面のスクリーンショット](assets/documentautomation/automation_40.png)

1. クリック **アップロード** E04/Flows/にある GenerateProposal_20210311231623.zip フォルダーを選択します。

   ![フォルダー選択のスクリーンショット](assets/documentautomation/automation_41.png)

1. クリック **読み込み**&#x200B;を選択します。

1. [ アクション ] の下の [ レンチ ] アイコンをクリックします。 **お客様に提案を送信**&#x200B;を選択します。

   ![レンチアイコンのスクリーンショット](assets/documentautomation/automation_42.png)

1. 選択 **新規として作成** 」をクリックします。
1. 「リソース名」でフローの名前を設定します。
1. 「**保存**」をクリックします。

   他の関連リソースに対してこの手順を繰り返し、接続を選択します。

   ![ファイル保存のスクリーンショット](assets/documentautomation/automation_43.png)

1. クリック **読み込み** すべての接続を確立した後

### 選択したファイル用に設定

フローが作成されたら、次の操作を行います。

1. クリック **編集**&#x200B;を選択します。

   ![編集の選択場所のスクリーンショット](assets/documentautomation/automation_44.png)

1. トリガーを選択 **選択したファイル**&#x200B;を選択します。

   サイトアドレスにSharePointサイトを追加します。
ライブラリをライブラリに追加します。

   ![完了したトリガーのスクリーンショット](assets/documentautomation/automation_45.png)

### templateFolderPath の設定

1. templateFolderPath 変数をクリックします。
1. インポートしたSharePointサイト内の Templates フォルダーのパスを設定します。

### 表紙を設定/ファイルの内容を取得

1. クリック **表紙** 」アクションをクリックします。
1. 拡張 **表紙：ファイルコンテンツを取得**&#x200B;を選択します。

   「サイトアドレス」をSharePointサイトに設定します。

   ![拡張カバーのスクリーンショット](assets/documentautomation/automation_46.png)



### 選択したファイルを設定

1. を展開します。 **選択したファイル** スコープアクション。

   「サイトアドレス」と「ライブラリ名」を、それぞれ「 **ファイルのプロパティの取得**を選択します。
「サイトアドレス」を「 **ファイルコンテンツの取得**&#x200B;を選択します。

   ![展開された「選択したファイル」アクションのスクリーンショット](assets/documentautomation/automation_47.png)

### ホワイトペーパーの設定

1. クリック **ホワイトペーパー** 」をクリックします。
1. 拡張 **条件：ホワイトペーパーを追加**&#x200B;を選択します。

   ![展開された「ホワイトペーパーを追加」条件のスクリーンショット](assets/documentautomation/automation_48.png)

1. 拡張 **ホワイトペーパー 1:パスを使用したファイルコンテンツの取得**を選択します。
指定したSharePointサイトにサイトアドレスを編集します。

～に対して同じ手順を繰り返す **条件：ホワイトペーパー 2 を追加**&#x200B;を選択します。

### ファイル作成の設定

1. 拡張 **ファイルを作成**&#x200B;を選択します。

   サイトアドレスとフォルダーパスの編集：SharePointサイトと、Generated Docs フォルダーがあるパスを編集します。

1. 「**保存**」をクリックします。

### フローのテスト

1. SharePointの Proposal フォルダーに移動します。
1. Proposal.docx フォルダーを選択します。

   ![提案フォルダーを選択する際のスクリーンショット](assets/documentautomation/automation_49.png)

1. 「フロー」の下でフローを選択します。 **自動化** を選択します。

   ![「自動化」メニューの選択のスクリーンショット](assets/documentautomation/automation_50.png)

1. クリック **続行** 」をクリックしてフローを開始します。

   ![「続行」ボタンの選択のスクリーンショット](assets/documentautomation/automation_51.png)

1. 表紙と追加するホワイトペーパーを選択します。
1. クリック **フローの実行**&#x200B;を選択します。

   ![「フローを実行」ボタンのスクリーンショット](assets/documentautomation/automation_52.png)

Generate Docs フォルダーに移動します。 生成されたPDFファイル

![新しいディレクトリファイルが追加されたSharePointPDFのスクリーンショット](assets/documentautomation/automation_53.png)

### フローへのProtectおよびその他のアクションの追加

フローが正常に作成されたら、フローを編集して、パスワードを使用してPDF文書を暗号化します。 また、他のアクションの活用方法も説明します。

1. フローの最後に戻ります。
1. 次の **+** 間のシンボル **結合PDF** および **ファイルの作成**&#x200B;を選択します。

   ![+記号の選択場所のスクリーンショット](assets/documentautomation/automation_54.png)

1. 選択 **アクションの追加**&#x200B;を選択します。
1. 「Adobe PDF Tools」を検索します。

   ![Adobe PDF検索のスクリーンショット](assets/documentautomation/automation_55.png)

1. 選択 **ProtectPDFの表示**&#x200B;を選択します。
1. 「動的コンテンツを使用してファイル名」フィールドを **PDFファイル名の結合PDF**&#x200B;を選択します。

   ![動的コンテンツのスクリーンショット](assets/documentautomation/automation_56.png)

   トリガーには、開始フォームの一部である「パスワード」フィールドがあります。 それはここで使えます。

1. 検索対象 **パスワードフィールド** 動的コンテンツを使用して、「パスワード」フィールドに入力します。

   ![パスワード検索のスクリーンショット](assets/documentautomation/automation_57.png)

1. 動的コンテンツを使用して **PDFファイルの内容の結合PDF** 」をクリックします。
1. 変更する **ファイルの作成** を使用して、マージオプションではなくProtectPDFからファイルコンテンツをPDFします。
1. 拡張 **ファイルの作成**&#x200B;を選択します。
1. 「ファイルコンテンツ」フィールドをクリアします。
1. 動的コンテンツを使用した配置 **PDFファイルの内容** から **ProtectPDFの表示**&#x200B;を選択します。

### フローのテスト

1. SharePointの Proposal フォルダーに移動します。
1. Proposal.docx を選択します。

   ![提案フォルダーを選択した場合のスクリーンショット](assets/documentautomation/automation_58.png)

1. 選択 **自動化** をクリックしてフローを選択します。

   ![メニューから「自動処理」を選択したスクリーンショット](assets/documentautomation/automation_59.png)

1. クリック **続行** 」をクリックしてフローを開始します。

   ![「続行」のスクリーンショット](assets/documentautomation/automation_60.png)

1. 追加する表紙とホワイトペーパーを選択します。
1. 「パスワード」フィールドに、設定するパスワードを設定します。
1. クリック **フローの実行**&#x200B;を選択します。

   ![選択したファイルのスクリーンショットと「フローを実行」ボタン](assets/documentautomation/automation_61.png)

1. Generate Docs フォルダーに移動します。
生成されたPDFファイル PDFファイルを開くと、パスワードの入力を求めるプロンプトがPDFされます。

   ![SharePointディレクトリに生成されたPDFのスクリーンショット](assets/documentautomation/automation_62.png)
