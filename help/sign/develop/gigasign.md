---
title: GigaSign を使用した大量の文書の収集
description: Gigasign を使用すると、署名が必要な文書を送信、収集、追跡して、数千人に同時に送信できます
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: ad54f7afa78b0fbb31eccf455723a8890cb92355
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%

---

# GigaSign を使用した大量の文書の収集

Gigasign を使用すると、署名が必要な文書を送信、収集、追跡して、数千人に同時に送信できます。 従業員やお客様との大量のコミュニケーションに対応するように設計されており、一括送信ごとに最大 2,500 人の受信者をサポートします。 GigaSign は、Acrobat Sign API を使用して MegaSign と同じ機能を提供し、複数の署名者、受信者グループ、受信者の役割、契約書名、カーボンコピーなどをサポートします。

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## GigaSign アプリをダウンロードしてインストールします。

[GigaSign Zip ファイルのダウンロード](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Java 1.8 ダウンロードリンク（必要な場合のみ）](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[ホワイトリストへの IP アドレス（必要な場合のみ）](https://helpx.adobe.com/jp/sign/system-requirements.html#IPs){target="_blank"}

## 基本的な設定手順

1. Acrobat Sign アカウントにログインする.

1. クリック **[!UICONTROL グループ]** または **[!UICONTROL アカウント]**&#x200B;一番上に見えるほうが

1. 画面左側の検索フィールドに「アクセストークン」と入力します。

1. 右側の「+」アイコンを押します。

1. 必要なスコープ (User_Read、Agreement_Read、Agreement_Write、Agreement_Send、Library_Read) を持つキーを作成します。

1. 作成したキーをダブルクリックして、全文をコピーします（画面の右側に移動するため、すべて取得していることを確認します）。

1. GigaSign を開きます。

1. ツールバーの「 **[!UICONTROL 設定]** アイコンをタップします。

1. 統合キーを最初の行に貼り付けます。

1. 2 行目に、キーの作成に使用したアカウントの電子メールアドレスを入力します。

1. 「**[!UICONTROL 送信]**」をクリックします。
