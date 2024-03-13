---
title: GigaSignを使用した大量の文書の収集
description: Gigasignを使用すると、何千人もの人に同時に文書を送信、収集、および署名用のトラックできます
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: 636119a247f7d891c6edaa16149fcc8083ccee7e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# GigaSignを使用した大量の文書の収集

Gigasignを使用すると、何千人もの人に同時に文書を送信、収集、および署名用のトラックできます。 これは、従業員や顧客との大量の通信に適しており、一括送信ごとに最大2,500人の受信者をサポートします。 GigaSignは、Acrobat Sign APIを使用してMegaSignと同じ機能を提供します。また、複数の署名者、受信者グループ、受信者の役割、契約書名、カーボンコピーなどのサポートも含まれています。

>[!IMPORTANT]
>
>GigaSignは、JavaまたはAcrobat Signの最新バージョンには更新されず、サポート対象外になります。 GigaSignの機能は、 [一括送信](https://helpx.adobe.com/acrobat/using/send-in-bulk.html) 機能。 GigaSignの使用を明示的に必要としないユースケースには、すべて「一括送信」を使用してください。

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## GigaSignアプリをダウンロードしてインストールします

[GigaSign Zipファイルをダウンロード](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Java 1.8ダウンロードリンク（必要な場合のみ）](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[ホワイトリストへのIPアドレス（必要な場合のみ）](https://helpx.adobe.com/jp/sign/system-requirements.html#IPs){target="_blank"}

## 基本的なセットアップ手順

1. Acrobat Signアカウントにログインします。

1. クリック **[!UICONTROL グループ]** または **[!UICONTROL アカウント]**&#x200B;上に見えるものはどちらでも構いません。

1. 画面の左側にある検索フィールドに「アクセストークン」と入力します。

1. 右側の「+」アイコンを押します。

1. 必要なスコープを持つキーを作成します(User_Read、Agreement_Read、Agreement_Write、Agreement_Send、Library_Read)。

1. 作成したキーをダブルクリックし、全文をコピーします（全文が画面の右側に表示されるため、すべて表示されていることを確認します）。

1. GigaSignを開きます。

1. 「 **[!UICONTROL 設定]** アイコンが表示されます。

1. 最初の行に統合キーを貼り付けます。

1. 2行目にそのキーの作成に使用したアカウントの電子メールアドレスを入力します。

1. 「**[!UICONTROL 送信]**」をクリックします。
