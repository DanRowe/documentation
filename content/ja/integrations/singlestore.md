---
app_id: singlestore
app_uuid: 5e8c3b5f-278f-4423-90d9-969c06a478eb
assets:
  dashboards:
    Singlestore Overview: assets/dashboards/overview.json
  integration:
    configuration:
      spec: assets/configuration/spec.yaml
    events:
      creates_events: false
    metrics:
      check: singlestore.bytes_received
      metadata_path: metadata.csv
      prefix: singlestore.
    process_signatures:
    - memsqld
    service_checks:
      metadata_path: assets/service_checks.json
    source_type_name: SingleStore
  logs:
    source: singlestore
  monitors:
    '[SingleStore] License expiration': assets/monitors/license_expiration.json
    '[SingleStore] Read failures rate': assets/monitors/read_failures.json
    '[SingleStore] Write failures rate': assets/monitors/write_failures.json
author:
  homepage: https://www.datadoghq.com
  name: Datadog
  sales_email: info@datadoghq.com (日本語対応)
  support_email: help@datadoghq.com
categories:
- data store
- ログの収集
dependencies:
- https://github.com/DataDog/integrations-core/blob/master/singlestore/README.md
display_on_public_website: true
draft: false
git_integration_title: singlestore
integration_id: singlestore
integration_title: SingleStore
integration_version: 1.3.1
is_public: true
kind: integration
manifest_version: 2.0.0
name: singlestore
oauth: {}
public_title: SingleStore
short_description: リーフやアグリゲーターから SingleStore のメトリクスを収集します。
supported_os:
- linux
- macos
- windows
tile:
  changelog: CHANGELOG.md
  classifier_tags:
  - Supported OS::Linux
  - Supported OS::macOS
  - Supported OS::Windows
  - Category::Data Store
  - Category::Log Collection
  configuration: README.md#Setup
  description: リーフやアグリゲーターから SingleStore のメトリクスを収集します。
  media: []
  overview: README.md#Overview
  support: README.md#Support
  title: SingleStore
---



## 概要

このチェックでは、Datadog Agent を通じて [SingleStore][1] を監視します。SingleStore は、保存されたデータのトランザクション処理と分析処理を提供します。Datadog-SingleStoreDB インテグレーションを有効にすると、以下が可能になります。

- メトリクスとイベントにより、クラスターとノードの健全性を把握する。
- ストレージ容量の低下に対応する。
- リソースの利用効率を高める。


## セットアップ

ホストで実行されている Agent 用にこのチェックをインストールおよび構成する場合は、以下の手順に従ってください。コンテナ環境の場合は、[オートディスカバリーのインテグレーションテンプレート][2]のガイドを参照してこの手順を行ってください。

### インストール

SingleStore チェックは [Datadog Agent][3] パッケージに含まれています。
サーバーに追加でインストールする必要はありません。

### コンフィギュレーション

#### ホスト

##### メトリクスの収集
1. SingleStore のパフォーマンスデータを収集するには、Agent のコンフィギュレーションディレクトリのルートにある `conf.d/` フォルダーの `singlestore.d/conf.yaml` ファイルを編集します。使用可能なすべてのコンフィギュレーションオプションについては、[サンプル singlestore.d/conf.yaml][4] を参照してください。

2. [Agent を再起動します][5]。

**注**: デフォルトでは、SingleStore インテグレーションは `MV_GLOBAL_STATUS`、`AGGREGATORS`、`LEAVES` テーブルからしかメトリクスを収集しません。システムレベルのメトリクス (CPU、ディスク、ネットワーク IO、メモリ) を追加で収集するには、`singlestore.d/conf.yaml` ファイルで `collect_system_metrics: true` を設定します。

##### ログの収集

{{< site-region region="us3" >}}
**ログ収集は、このサイトではサポートされていません。**
{{< /site-region >}}

1. Datadog Agent で、ログの収集はデフォルトで無効になっています。以下のように、`datadog.yaml` ファイルでこれを有効にします。

   ```yaml
   logs_enabled: true
   ```

2. SingleStore のログの収集を開始するには、該当のログファイルを `singlestore.d/conf.yaml` ファイルに追加します。

   ```yaml
     logs:
       - type: file
         path: /var/lib/memsql/<NODE_ID>/tracelogs/memsql.log
         source: singlestore
         service: "<SERVICE_NAME>"
   ```

    `path` パラメーターと `service` パラメーターの値を変更し、環境に合わせて構成してください。使用可能なすべてのコンフィギュレーションオプションの詳細については、[サンプル singlestore.d/conf.yaml][4] を参照してください。

3. [Agent を再起動します][5]。

#### コンテナ化

コンテナ環境の場合は、[オートディスカバリーのインテグレーションテンプレート][2]のガイドを参照して、次のパラメーターを適用してください。

#### メトリクスの収集

| パラメーター            | 値                                                      |
|----------------------|------------------------------------------------------------|
| `<インテグレーション名>` | `singlestore`                                                   |
| `<初期コンフィギュレーション>`      | 空白または `{}`                                              |
| `<インスタンスコンフィギュレーション>`  | `{"host": "%%host%%", "port": "%%port%%", "username": "<ユーザー>", "password": "<パスワード>"}`       |

##### ログの収集

{{< site-region region="us3" >}}
**ログ収集は、このサイトではサポートされていません。**
{{< /site-region >}}

Datadog Agent で、ログの収集はデフォルトで無効になっています。有効にする方法については、[Kubernetes ログ収集][6]を参照してください。

| パラメーター      | 値                                     |
|----------------|-------------------------------------------|
| `<LOG_CONFIG>` | `{"source": "singlestore", "service": "<SERVICE_NAME>"}` |


### 検証

[Agent の status サブコマンドを実行][7]し、Checks セクションで `singlestore` を探します。

## 収集データ

### メトリクス
{{< get-metrics-from-git "singlestore" >}}



### イベント

SingleStore インテグレーションには、イベントは含まれません。

### サービスのチェック
{{< get-service-checks-from-git "singlestore" >}}


## トラブルシューティング

ご不明な点は、[Datadog のサポートチーム][10]までお問合せください。


[1]: https://www.singlestore.com/
[2]: https://docs.datadoghq.com/ja/getting_started/agent/autodiscovery#integration-templates
[3]: https://app.datadoghq.com/account/settings#agent
[4]: https://github.com/DataDog/integrations-core/blob/master/singlestore/datadog_checks/singlestore/data/conf.yaml.example
[5]: https://docs.datadoghq.com/ja/agent/guide/agent-commands/#start-stop-and-restart-the-agent
[6]: https://docs.datadoghq.com/ja/agent/kubernetes/log/
[7]: https://docs.datadoghq.com/ja/agent/guide/agent-commands/#agent-status-and-information
[8]: https://github.com/DataDog/integrations-core/blob/master/singlestore/metadata.csv
[9]: https://github.com/DataDog/integrations-core/blob/master/singlestore/assets/service_checks.json
[10]: https://docs.datadoghq.com/ja/help/