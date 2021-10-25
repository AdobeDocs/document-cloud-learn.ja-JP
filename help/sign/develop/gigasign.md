---
title: GigaSign を使用した大量の文書の収集
description: Gigasign を使用すると、署名を依頼する文書を送信、収集、追跡して、同時に数千人に送信できます
role: User, Admin
product: adobe sign
level: Intermediate
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: 7d82422e442cbbed9420050c30ca70821e9a2cdd
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 4%

---

# GigaSign を使用した大量の文書の収集

Gigasign を使用すると、署名を依頼する文書を送信、収集、追跡して、同時に数千人に送信できます。 従業員やお客様との大量のコミュニケーションに対応し、一括送信ごとに最大 2,500 人の受信者をサポートします。 GigaSign は、Adobe Sign API を使用して MegaSign と同じ機能を提供し、複数の署名者、受信者グループ、受信者の役割、契約書名、カーボンコピーなどをサポートします。

>[!VIDEO](https://video.tv.adobe.com/v/328113?hidetitle=true)

## GigaSign アプリをダウンロードしてインストールする

[GigaSign Zip ファイルのダウンロード](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Java 1.8 ダウンロードリンク（必要な場合のみ）](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target=&quot;_blank&quot;}

[ホワイトリストへの IP アドレス（必要な場合のみ）](https://helpx.adobe.com/jp/sign/system-requirements.html#IPs){target=&quot;_blank&quot;}

## 基本的な設定手順

1. Adobe Sign アカウントにログインします。

1. クリック **[!UICONTROL グループ]** または **[!UICONTROL アカウント]**&#x200B;上の方を見てください

1. 画面左側の検索フィールドに「アクセストークン」と入力します。

1. 右側の「+」アイコンを押します。

1. 必要なスコープ (User_Read、Agreement_Read、Agreement_Write、Agreement_Send、Library_Read) を持つキーを作成します。

1. 作成したキーをダブルクリックして、全文をコピーします（画面の右側に消えるので、すべてを取得していることを確認します）。

1. GigaSign を開きます。

1. 次の **[!UICONTROL 設定]** アイコンをクリックします。

1. 最初の行に統合キーを貼り付けます。

1. 2 行目に、キーの作成に使用したアカウントの電子メールアドレスを入力します。

1. クリック **[!UICONTROL 送信]**&#x200B;を選択します。
