---
kind: ガイド
title: グラフに適した色の選択
---

Datadog のグラフにおいて、色はデータの系列を区別するための主要な方法です。グラフに適切な色を選択することで、チームメイトはグラフのデータをパースし、洞察を得て、効果的にトラブルシューティングを行うことができるようになります。

{{< img src="dashboards/guide/colors/colors_top.png" alt="'Graph your data' の見出しで、ユーザーはカラーパレットのリストから選択している。" style="width:90%;" >}}

## カラーパレットの種類

### Categorical パレット

Categorical パレットは、差別化が必要でありながら、自然な順序に従わないデータ (たとえば、アベイラビリティゾーンなど) に使用するのが最適です。

{{< img src="dashboards/guide/colors/2_alphabet.png" alt="A B C D E F G の文字が表示されたパレットで、それぞれの文字が異なる色相で表示されています。" style="width:40%;" >}}

#### Classic

デフォルトの Classic パレットは、読みやすさを重視した 6 色のセットを使用しています。系列の数が 6 を超えると、系列に割り当てられた色が繰り返されます。隣り合う系列には、それぞれ異なる色が設定されています。

Classic カラーパレットは、視覚的なアクセシビリティをサポートしています。

{{< img src="dashboards/guide/colors/3_classic_palette.png" alt="ドーナツグラフと積み上げ棒グラフの Classic パレットがどのようなものかを説明する概要。" style="width:80%;" >}}

#### Consistent/Semantic

Consistent パレットは、データ系列に一貫して同じ色を割り当てることができ、チャート間のデータの相関を容易にすることができます。Classic パレットと異なり、Consistent パレットは隣接するデータ系列が同じ色を使用することを保証するものではなく、またアクセシビリティにも対応していません。


{{< img src="dashboards/guide/colors/4_consistent_palette.png" alt="Consistent/Semantic パレットのカラーパレット。" style="width:70%;" >}}

{{< img src="dashboards/guide/colors/5_consistent_interface.png" alt="Consistent パレットの棒グラフ。" style="width:90%;" >}}

互換性のあるタグの小さなサブセットについては、Datadog は自動的にデータの各系列の背後にある意味を認識します。この場合、Consistent カラーパレットは Semantic カラーパレットとして表示され、色で意味を表現します。例えば、赤色はエラーを表す場合があります。

{{< img src="dashboards/guide/colors/6_semantic_interface.png" alt="Semantic パレットの棒グラフ。" style="width:90%;" >}}

### Diverging パレット

データセット内の値の差を強調する必要がある場合は、Diverging パレットを使用します。Diverging パレットは、自然な順序と自然な中間点を持つデータに最も適しています。例: メモリ使用率の変化量、-100% から +100% まで、自然な中点は 0%

Diverging パレットには、Cool (緑と青)、Warm (黄色とオレンジの中間) の 2 種類があります。

{{< img src="dashboards/guide/colors/7_divergent_palette.png" alt="3 -2 -1 0 1 2 3 を示すパレットで、両端に異なる色のグラデーションがある。" style="width:40%;" >}}
{{< img src="dashboards/guide/colors/8_divergent_graphs.png" alt="Diverging パレットのグラフ。" style="width:80%;" >}}

### Sequential パレット

Sequential パレットは、データセット内の異なる系列に共通点があることを強調する必要がある場合に使用します。このパレットは、ホスト群の CPU 使用率 (0％ から 100％ まで) のような自然な順序を持つデータに適しています。

カラーバリエーションは、パープル、オレンジ、グレー、レッド、グリーン、ブルーの 5 色です。

[カラーオーバーライド](#color-overrides)と組み合わせると、Sequential パレットは、1 つのグラフで複数のクエリを実行した結果を区別するために役立ちます。

{{< img src="dashboards/guide/colors/9_sequential_palette.png" alt="1 2 3 4 5 6 7 を示すパレットで、色はグラデーションになっている。" style="width:r0%;" >}}
{{< img src="dashboards/guide/colors/10_sequential_graphs.png" alt="Sequential パレットのグラフ。" style="width:80%;" >}}

## カラーオーバーライド

カラーオーバーライドを使うと、各クエリに好きな色を 1 つずつ割り当てることができます。これは、1 つのグラフで複数のクエリを実行した結果を区別する場合に特に有効です。

{{< img src="dashboards/guide/colors/11_overrides.png" alt="カラーオーバーライドを構成するためのパネル。" style="width:80%;" >}}

## アクセシビリティの設定

Datadog では、色覚異常、視力低下、コントラスト感度などの視覚的ニーズに対応するため、グラフにアクセシブルカラーモードを提供しています。アクセシブルカラーモードを選択すると、Classic パレットを使用しているすべてのグラフが、特定の視覚的ニーズに対応したアクセシブルな色でレンダリングされます。アクセシブルカラーモードは、[User Preferences ページ][1]で設定することができます。

{{< img src="dashboards/guide/colors/visual_accessibility.png" alt="利用可能な視覚的アクセシビリティオプション: デフォルト、プロタノピア (緑と赤の区別がつきにくい)、デュータノピア (赤、緑、黄の区別がつきにくい)、トリタノピア (青と緑の区別がつきにくい)、ハイコントラスト (低視力用に色の区切りを増やす)、低彩度 (視覚化するためにコントラストを下げる)。" style="width:90%;" >}}

[1]: https://app.datadoghq.com/personal-settings/preferences