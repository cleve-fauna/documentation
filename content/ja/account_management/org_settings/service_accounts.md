---
further_reading:
- link: https://docs.datadoghq.com/api/latest/service-accounts/
  tag: ドキュメント
  text: サービスアカウント API リファレンス
title: サービスアカウント
---

## 概要

サービスアカウントは、チーム全体で共有されるアプリケーションキーやその他のリソースを所有するために使用できる非インタラクティブなアカウントです。サービスアカウントのアプリケーションキーは、キーを作成した本人が一度だけ閲覧することができます。

あなたの会社の社員が、個人のアプリケーションキーを使って Datadog API にリクエストを送信する自動スクリプトをセットアップしたとします。その社員が退社すると、その社員の Datadog アカウントを無効化し、そのアプリケーションキーは機能しなくなります。自動化されたスクリプトも、誰かが有効なアプリケーションキーで更新するまで、動作しなくなります。Datadog API への自動リクエストに個人のアプリケーションキーの代わりにサービスアカウントのアプリケーションキーを使用することで、この問題を回避することができます。

## ナビゲーション

サービスアカウントは、[組織の設定][1]に存在します。

UI でサービスアカウントにアクセスするには

1. アカウントメニューから、**Organization Settings** に移動します。
2. **Accounts** の下で、**Service Accounts** を選択します。

[Service Accounts ページ][2]には、組織内のすべてのサービスアカウントのリストが含まれています。Datadog Admin Role を持つユーザーを含む、Service Account Write 権限を持つユーザーは、サービスアカウントを作成することができます。サービス アカウントの書き込み権限を持たないユーザーには、読み取り専用のビューが表示されます。

### サービスアカウントを表示する

デフォルトでは、Service Accounts ページはアクティブなサービスアカウントのみを表示します。無効なサービスアカウントを下のリストに含めるには、**Disabled** を選択します。

ページ上部にある検索ボックスを使用して、サービスアカウントをフィルターします。フィルターは、名前、メール、ロールのフィールドを検索します。

アカウントをクリックすると、以下の情報を含む詳細なサイドパネルビューにアクセスできます。

- ステータス (有効または無効)
- 作成日および最終修正日
- ロール
- アプリケーションキー
- アクセス許可

### サービスアカウントを作成する

サービスアカウントを作成するには、次の手順を実行します。

1. **New Service Account** をクリックします。ダイアログボックスが表示されます。
2. サービスアカウントの名前とメールアドレスを入力します。
3. **Assign Roles** ドロップダウンメニューを使用して、サービスアカウントに 1 つ以上のロールを選択します。
4. 保存するには、**Create Service Account** をクリックします。

Datadog ユーザーのメールアドレスとは異なり、サービスアカウントのメールアドレスは、組織全体で一意である必要はありません。

### サービスアカウントを編集する

サービスアカウントを変更するには、サービスアカウント一覧でクリックします。

1. サイドパネルで、サービスアカウント名の横にある **Edit** をクリックします。ダイアログボックスが表示されます。
2. 変更したいフィールドを更新します。名前、メールアドレス、ステータス、ロールを編集することができます。
3. **保存**をクリックします。

サービスアカウントを無効にするには、上記の手順でサービスアカウントを編集し、ステータスを **Disabled** に設定します。

### アプリケーションキーの作成・失効

サービスアカウントのアプリケーションキーを作成または失効させるには、サービスアカウント一覧からアカウントを選択します。サービスアカウントのサイドパネルが表示されます。

アプリケーションキーを新規に作成する場合は、以下の手順で行います。

- **New Key** をクリックします。ダイアログボックスが表示されます。
- キーにわかりやすい名前をつけます。
- **Create Key** をクリックします。

ダイアログボックスが更新され、キーが表示されます。キーをコピーして、任意の場所に貼り付けます。ダイアログボックスを閉じた後、キーの値を取得することはできません。

アプリケーションキーを失効させるには、サービスアカウント詳細表示のサイドパネルでキーを探し、キーにカーソルを合わせます。右側に鉛筆とゴミ箱のアイコンが表示されます。ゴミ箱をクリックすると、キーが失効されます。キーを失効させたら、**Confirm** をクリックします。

### API

Datadog API でサービスアカウントを利用する場合は、[サービスアカウント API リファレンス][3]を参照してください。

## サービスアカウントのアプリケーションキー

サービスアカウントのアプリケーションキーは、作成直後に一度だけ閲覧することができます。アプリケーションキーへのアクセスを制限することで、他のユーザーがそのキーにアクセスしたときに発生する可能性のある問題を防ぐことができます。サービスアカウントのキーを紛失したり、忘れたりした場合は、キーを失効させて新しいキーを作成してください。

## アクセス許可

サービスアカウントを作成することで、自分に代わって Datadog と対話するアクターが作成されます。サービスアカウントページでの機能は、Datadog のロールと権限によって異なります。

サービスアカウントを作成するには、サービスアカウント書き込み権限が必要です。Datadog Admin ロールは、Service Account Write を含むので、Datadog Admin ロールを持つ人は誰でもサービスアカウントを作成することができます。

サービスアカウントを作成するとき、自分が持っているロールと権限の任意のサブセットを与えることができます。ただし、User Access Manage 権限を持っている場合は例外で、事実上、Datadog で何でもできる管理者権限が付与されます。User Access Manage 権限を持つ Datadog アカウントは、サービスアカウントに割り当てることができるロールと権限に制限がありません。


## 通知

Datadog は、以下のアクションが発生すると、サービスアカウントに関連付けられたメールアドレスに通知を送信します。
- アプリケーションキーの作成
- アプリケーションキーの失効
- サービスアカウントの無効化


## その他の参考資料

{{< partial name="whats-next/whats-next.html" >}}

[1]: /ja/account_management/org_settings/
[2]: https://app.datadoghq.com/organization-settings/service-accounts
[3]: /ja/api/latest/service-accounts/