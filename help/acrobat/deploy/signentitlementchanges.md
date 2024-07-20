---
title: ETLA版のお客様向けのAcrobat DC製品の重要なアップデート
description: 2020年8月から2020年11月20日までのETLA（エンタープライズタームライセンス契約）オファーに含まれる、Acrobat DCの使用権限の重要な変更点について説明します
feature: Deploy
role: Admin
level: Intermediate
jira: KT-7269
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 4e6fbf91e96d26f9ee8f1105ad68738b9450a32d
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 2%

---

# ETLA版のお客様向けのAcrobat DC製品の重要なアップデート

[!DNL Adobe Sign Individual] (Adobe Sign Proとしても知られる)は、ETLA（エンタープライズタームライセンス契約）の提供に含まれるすべてのAcrobat DC使用権限のプロビジョニングが2020年8月に解除され、2020年11月20日まで継続されます。 [!DNL Adobe Sign Individual]はエンタープライズグレードの機能を提供していないため、Adobe Sign Enterprise for enterpriseのお客様に置き換える必要があります。 これには、スタンドアロンアプリとしてライセンス認証されたAcrobat DCと、エンタープライズ版Creative Cloudコンプリートプランの一部としてライセンス認証されたAcrobat DCが含まれます。

[!DNL Adobe Sign Individual]へのアクセスは、**Adobe Sign**&#x200B;ツールまたは&#x200B;**Fill &amp; Sign**&#x200B;ツール（[署名を依頼](https://www.adobe.com/jp/acrobat/online/request-signature.html){target="_blank"}）を介してAcrobatで利用できます。

Acrobat DCでの![[!DNL Adobe Sign Individual]アクセス](../assets/Deploy_SignEntitle1.png)

Acrobat DCを最新バージョンにアップデートしていない場合は、「Send for Signature」というラベルが付いている場合があります。

## プロビジョニング解除する理由

[2018年10月、まったく新しいAcrobat DCをリリースしました](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC)。 この最新リリースには、モバイルデバイス、web、デスクトップでのPDFとの連携を強化する新しいツールと機能、およびすべての新しい共同作業ツールが含まれています。 Acrobat DCに登録しているお客様は、すでにこれらの優れた機能を利用できます。 また、電子サインソリューションのAdobe Signに関する重要なアップデートもリリースされました。

2018年10月のリリース以前では、Acrobat DCユーザーは、[!DNL Adobe Sign Individual]の使用権限でプロビジョニングされたAcrobatの「Fill &amp; Sign」(または「Adobe Sign」または「Send for Signature」)というラベルのツールを使用して、電子サイン用に文書を送信できました。

このオプションを使用すると、電子サインを取得するための優れた方法が提供されますが、[!DNL Adobe Sign Individual]のプロビジョニングは解除されます。これは、次のようなAdobe Sign Enterpriseで使用できるEnterprise Gradeの機能が提供されないためです。

* 契約書の送信や署名を行う権限を持つユーザーを一元管理できる
* 組織全体で送信および使用される契約書を管理者が管理できるようにする
* 組織全体で電子サインを管理するための詳細なコントロールを提供

さらに、Adobe Sign Enterpriseは、[!DNL Adobe Sign Individual]の使用権限で使用可能なものと比較して、次のような多くの機能を提供します（ただし、これらに限定されません）。

* 管理
   * シングルサインオン
   * アカウントの委任
* 統合
   * Dropbox、Salesforce、Workdayなどとの事前定義済みのEnterprise Integrations
   * Adobe Signは、Office 365、SharePoint、Dynamics、Teams、Flowを含む[Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html)エンタープライズポートフォリオで推奨される電子サインソリューションです
* カスタマイズと最適化
   * 強化された電子サイン認証、高度なIDベースの署名者ID確認、ワークフローデザイナー、高度な言語サポートなど。

Adobe Signは、法的に準拠した署名を取得するための、業界をリードする世界的に認められたソリューションです。 Adobe Signは、組織の電子サインに関するあらゆるニーズに対応するために一から構築されており、お客様やお客様のユーザーが電子サインに関する様々な地域や業界の規制に完全に準拠した電子サインを使用していることを保証するIT管理者フレンドリーなツールを備えています。 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html)を介したSignの管理について詳しくは、[ここ](https://helpx.adobe.com/enterprise/using/adobe-sign-for-enterprise.html)を参照してください。

Acrobat DCおよびAdobe Sign Enterpriseを含む広範なデジタルドキュメントプラットフォームを通じて引き続きAdobeの電子サイン機能を提供する方法については、組織の連絡先にお問い合わせください。

## 既存の契約書へのアクセス

ユーザーは、このアクションの前に送信された契約書にAdobe Document Cloudを介して引き続きアクセスできます。そのためには、Adobe IDでhttps://documentcloud.adobe.comにログインします。 このユーザーがSign Enterpriseへの移行をスケジュールされている場合、ユーザーは次の[手順](https://helpx.adobe.com/jp/sign/kb/how-to-download-signed-documents---adobe-sign.html)に従う必要があります。

## [!DNL Sign Individual]の使用権限がないAcrobat DCエクスペリエンス

Adobe Sign Enterpriseの使用権限を持つユーザーは、Adobe Signまたは[!UICONTROL Fill &amp; Sign] （署名を依頼）ツールを使用して、Acrobat内で契約書を送信できます。
Adobe Sign Enterpriseの使用権限を持たないユーザーは、新しい契約書を送信できず、エラーメッセージが表示されます。 次の図は、考えられる結果の概要を示しています。

![Acrobat DCエクスペリエンスのエラーメッセージ](../assets/Deploy_SignEntitle2.png)

## Sign個人版の使用権限のないAdobe Document Cloud Webエクスペリエンス

ユーザーはhttps://documentcloud.adobe.com/にログインして、Adobe Sign個人版の使用権限のプロビジョニングを解除する前に送信された、すべての契約書にアクセスしてダウンロードできます。

![Document CloudのWebエクスペリエンスに関するエラーメッセージ](../assets/Deploy_SignEntitle3.png)

## 詳しくは、以下のページを参照してください。

* [Adobe Document Cloud にサインイン](https://helpx.adobe.com/document-cloud/help/sign-in.html)
* [ファイルの管理（ファイルはどこにありますか？）](https://helpx.adobe.com/document-cloud/help/manage-files.html)
* [構成に[!UICONTROL Acrobat Customization Wizard]を使用](https://www.adobe.com/jp/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [[!UICONTROL Admin Console]](https://helpx.adobe.com/jp/enterprise/using/admin-console.html)の概要
* [[!UICONTROL Admin Console]でのAdobe Signの管理](https://helpx.adobe.com/enterprise/using/adobe-sign-for-enterprise.html)

**リビジョン** 2020年5月20日、元の投稿 – 2019年8月
