---
title: GigaSignを使用して大量のドキュメントを収集
description: Gigasignを使用すると、数千人のユーザーに対して同時に署名用のドキュメントを送信、収集、追跡できます
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

# GigaSignを使用して大量のドキュメントを収集

Gigasignを使用すると、数千人のユーザーに対して同時に署名用のドキュメントを送信、収集、追跡できます。 従業員やお客様との大量のコミュニケーションを目的として設計されており、1回のバルク送信で最大2,500人の受信者をサポートします。 GigaSignは、Adobe Sign APIを使用してMegaSignと同じ機能を提供し、複数の署名者、受信者グループ、受信者の役割、契約名、カーボンコピーなどをサポートします。

>[!VIDEO](https://video.tv.adobe.com/v/328113?hidetitle=true)

## GigaSignアプリをダウンロードしてインストールする

[GigaSign ZIPファイルのダウンロード](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Java 1.8ダウンロードリンク（必要な場合のみ）](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target=&quot;_blank&quot;}

[ホワイトリストにIPアドレスを追加（必要な場合のみ）](https://helpx.adobe.com/jp/sign/system-requirements.html#IPs){target=&quot;_blank&quot;}

## 基本的な設定手順

1. Adobe Sign アカウントにログインします。

1. [**[!UICONTROL グループ]**]または[**[!UICONTROL アカウント]**]をクリックします。

1. 画面の左側の検索フィールドに「Access tokens」と入力します。

1. 右側の「+」アイコンを押します。

1. 必要な範囲(User_Read、Agreement_Read、Agreement_Write、Agreement_Send、Library_Read)でキーを作成します。

1. 作成したキーをダブルクリックし、全文をコピーします（画面の右側に表示されるので、必ず全文を入手してください）。

1. GigaSignを開きます。

1. 右上の&#x200B;**[!UICONTROL 設定]**&#x200B;アイコンをクリックします。

1. 統合キーを最初の行に貼り付けます。

1. 2行目に、そのキーの作成に使用したアカウントの電子メールアドレスを入力します。

1. [**[!UICONTROL 送信]**]をクリックします。
