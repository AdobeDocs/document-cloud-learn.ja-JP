---
title: ETLA版のお客様向けのAcrobat DC製品の重要なアップデート
description: 2020 年 8 月から 2020 年 11 月 20 日までのETLA（エンタープライズタームライセンス契約）の特典に含まれるAcrobat DCの使用権限に関する重要な変更について説明します。
role: Admin
product: adobe acrobat
level: Intermediate
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 3%

---

# Important Acrobat DC product updates for ETLA customers

[!DNL Adobe Sign Individual] (Adobe Sign Pro とも呼ばれます ) は、2020 年 8 月以降にETLA（包括ライセンス契約）の提供に含まれるすべてのAcrobat DCエンタイトルメントからプロビジョニング解除され、2020 年 11 月 20 日まで継続されます。 [!DNL Adobe Sign Individual] does not provide enterprise-grade functionality and should be replaced with Adobe Sign Enterprise for enterprise customers. これには、スタンドアロンアプリケーションとしてライセンスされたAcrobat DCと、エンタープライズ版コンプリートプランのCreative Cloudの一部としてライセンスされたAcrobat DCが含まれます。

Access to [!DNL Adobe Sign Individual] is available in Acrobat via the **Adobe Sign** tool or the **Fill &amp; Sign** tool (Request signatures).

![[!DNL Adobe Sign Individual] Acrobat DCでのアクセス](../assets/Deploy_SignEntitle1.png)

Acrobat DCを最新バージョンにアップデートしていない場合、ツールのラベルが「Send for Signature」と表示されます。

## プロビジョニング解除の理由

[2018 年 10 月には、まったく新しいAcrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC)を選択します。 この最新リリースには、モバイルデバイス、Web およびデスクトップでPDFを使用する際に役立つ新しいツールと機能に加え、まったく新しい共同作業ツールが含まれています。 Acrobat DCのサブスクリプションをご利用のお客様は、これらの優れた機能を既にご利用いただいている必要があります。 リリースされたもう 1 つの主要なアップデートは、電子サインソリューションのAdobe Signです。

Prior to the October 2018 release, Acrobat DC users have been able to send documents out for e-signature using tools in Acrobat labelled “Fill &amp; Sign” (or “Adobe Sign” or “Send for Signature”) which were provisioned with [!DNL Adobe Sign Individual] entitlement.

このオプションを使用すると、電子サインを取得するための優れた方法が提供されますが、プロビジョニング解除を行っています [!DNL Adobe Sign Individual] これは、Adobe Sign Enterprise を通じて使用できる次のようなエンタープライズグレードの機能を提供しないためです。

* 契約書の送信または署名の権限を持つユーザーを一元管理する機能
* Allowing admins to manage agreements that are sent and used across the organization
* Providing granular controls to manage electronic signatures across the organization

また、Adobe Sign Enterprise は、 [!DNL Adobe Sign Individual] 以下を含む（ただし、これらに限定されない）。

* 管理
   * シングルサインオン
   * アカウントの委任
* 統合
   * Dropbox、Salesforce、Workdayなどとの事前統合
   * Adobe Signは、 [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html) office 365、SharePoint、Dynamics、Teams、Flow を含むエンタープライズポートフォリオ
* カスタマイズと最適化
   * Enhanced e-signature authentication, Advanced ID-based signer identity verification, workflow designer, advanced language support, etc.

Adobe Signは、法的に準拠した署名を取得するための、業界をリードする世界的に認められたソリューションです。 Adobe Signは、お客様の組織の電子サインに関するあらゆるニーズに対応するためにゼロから構築されています。IT 管理者が利用しやすいツールによって、お客様やお客様のユーザーが、電子サインに関するさまざまな地域や業界の規制に準拠した電子サインを使用していることを確認できます。 詳しくは、 [ここ](https://helpx.adobe.com/enterprise/using/adobe-sign-for-enterprise.html) サインスルーの管理の詳細 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html)を選択します。

Acrobat DCやAdobe Sign Enterprise など、アドビの広範なデジタル文書プラットフォームを通じて電子サイン機能を引き続き提供する方法については、Adobeの担当者にお問い合わせください。

## 既存の契約書へのアクセス

ユーザーは、Adobe ID(https://documentcloud.adobe.com) でログインすることで、このアクションの前にAdobe Document Cloudを介して送信された契約書に引き続きアクセスできます。 If this user is scheduled for migration to Sign Enterprise, they will need to follow these [instructions](https://helpx.adobe.com/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Acrobat DCの [!DNL Sign Individual] 使用権限

Users who have Adobe Sign Enterprise entitlements will be able to send agreements within Acrobat using either the Adobe Sign or [!UICONTROL Fill &amp; Sign] (Request signatures) tool.
Adobe Sign Enterprise の使用権限がないユーザーは、新しい契約書を送信できず、エラーメッセージが表示されます。 次の図は、考えられる結果の概要を示しています。

![Acrobat DC Experience のエラーメッセージ](../assets/Deploy_SignEntitle2.png)

## Sign 個人版の使用権限のないAdobe Document Cloud Web エクスペリエンス

ユーザーはhttps://documentcloud.adobe.com/にログインして、Adobe Sign Individual の使用権限のプロビジョニングを解除する前に送信された契約書にアクセスしてダウンロードできます。

![Document CloudWeb エクスペリエンスのエラーメッセージ](../assets/Deploy_SignEntitle3.png)

## 詳しくは、以下のページを参照してください。

* [Adobe Document Cloud にサインイン](https://helpx.adobe.com/document-cloud/help/sign-in.html)
* [Managing files (Where are my files?)](https://helpx.adobe.com/document-cloud/help/manage-files.html)
* [使用方法 [!UICONTROL AcrobatCustomization Wizard] 設定](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [概要 [!UICONTROL Admin Console]](https://helpx.adobe.com/enterprise/using/admin-console.html)
* [Adobe Signを [!UICONTROL Admin Console]](https://helpx.adobe.com/enterprise/using/adobe-sign-for-enterprise.html)

**改訂** 2020 年 5 月 20 日；元の投稿 — 2019 年 8 月
