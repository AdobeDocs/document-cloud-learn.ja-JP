---
title: Acrobat Signテキストタグ付け
description: テキストタグ付けによってAcrobat Signフォームフィールドを構築する方法について説明します。
feature: Workflow, Sign
role: User, Admin
level: Experienced
jira: KT-6059
thumbnail: KT-6402.jpg
exl-id: 3a54925d-b713-487b-92b7-ec7160513696,c981c640-e50a-4952-ac39-2f90d6d0cf08
source-git-commit: 656c87201aca58de947cb835f610f6c82a814d57
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Acrobat Signテキストタグ付け

テキストタグ付きのAcrobat Signフォームフィールドを作成する方法について説明します。 テキストタグは、Microsoft Word、Adobe InDesignなどのオーサリングツールに直接追加できます。また、AcrobatのPDFを使用している場合にも追加できます。 これにより、Acrobat Signで使用する文書を作成する手間が大幅に軽減されます。 Acrobat Signでタグ付き文書をアップロードした後、テンプレートとして設定できます。これにより、誰もが文書にフィールドを追加する必要がなくなります。

## はじめに

テキストタグとは、文書内の任意の場所に配置された一意に書式設定されたテキストの断片であり、Acrobat Signにアップロードするとフィールドとして自動的に認識されます。

![テキストタグの構文](../assets/syntax.png)

テキストタグは、Microsoft Word、Adobe InDesignなどのオーサリングツールに直接追加できます。また、AcrobatなどのPDFを使用している場合にも追加できます。 テキストタグを使用すると、Acrobat Signで使用する文書を作成する手間が大幅に軽減されます。

### Microsoft Wordでのタグの追加

Microsoft Word文書にテキストタグを追加するには、この[ビデオチュートリアル](text-tagging-word.md)を参照してください。

### Acrobatでのタグの追加

Adobe Acrobatには、堅牢なドラッグ&amp;ドロップフォームオーサリング環境が用意されています。 Acrobatでテキストタグを適用すると、Acrobat Signで利用できる機能を利用できるようになります。

1. Acrobatでフォームを開きます。

1. **[!UICONTROL すべてのツール]**&#x200B;パネルから&#x200B;**[!UICONTROL フォームを準備]**&#x200B;を選択します。

1. **[!UICONTROL [フォームの作成]]**&#x200B;を選択します。

1. **[!UICONTROL オプション]**&#x200B;パネルのドロップダウンから「**[!UICONTROL フォームを電子サイン用に準備]**」を選択します。

   ![電子サイン用のフォームを準備](../assets/tag-prepare-e-signing.png)

1. 「**[!UICONTROL 次へ]**」を選択して確定します。

   ![フィールドの変換を確認](../assets/tag-confirm.png)

1. フィールドをダブルクリックして、**[!UICONTROL プロパティ]**&#x200B;ダイアログを表示します。

   [Acrobat Signテキストタグガイド](https://helpx.adobe.com/jp/sign/using/text-tag.html)で説明されている構文を使用して、フォームフィールド名を変更します。

1. 例えば、フィールド名に&#x200B;*OInt_es_:signer1:optinitials*&#x200B;と入力すると、最初のフィールドを省略可能にすることができます。

   ![フィールド名の変更](../assets/tag-opt-initials.png)

   テキストタグはフォームフィールド名に追加されます。Microsoft Word（またはその他のオーサリングツール）で使用する構文とは異なり、中括弧は含まれません。

   テキストタグは、フォームフィールドの名前を変更するだけで、フィールドパネルに追加することもできます。

   ![フィールドパネルで名前を変更](../assets/tag-rename.png)

1. ファイルを保存して閉じます。

1. Acrobat Signでファイルをアップロードし、次のセクションで説明する再利用可能なテンプレートを作成します。

### 再利用可能なテンプレートを作成

タグ付き文書を作成した後、それを再利用可能なテンプレートとして設定することで、誰もが文書にフィールドを追加する必要がなくなります。

再利用可能なテンプレートを作成するには、この[ビデオチュートリアル](../sign-advanced-users/create-a-template.md)を参照してください。
