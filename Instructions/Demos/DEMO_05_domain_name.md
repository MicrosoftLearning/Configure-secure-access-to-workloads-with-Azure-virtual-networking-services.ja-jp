---
demo:
  title: 'デモ: Azure DNS の作成と構成'
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---
## デモ – Azure DNS の作成と構成

このデモでは、Azure DNS について説明します。

[チュートリアル: ドメインとサブドメインをホストする - Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns)


**プライベート DNS ゾーンを作成する**

1. Azure portal にアクセスします。

1.  **DNS ゾーン** サービスを検索します。

1. **DNS ゾーン**を作成し、そのゾーンの目的を説明します。 名前には、contoso.internal.com を使用できます。

1.  DNS ゾーンが作成されるのを待ちます。 ページを **更新**する必要がある場合があります。 

**DNS レコード セットを追加する**


[チュートリアル: ゾーン内のリソース レコードを参照するエイリアス レコードを作成する](https://learn.microsoft.com/azure/dns/tutorial-alias-rr)

1. ゾーンが作成されたら、 **[+ レコード セット]** を選択します。

1.  **[種類]**   ドロップダウンを使用して、さまざまな種類のレコードを表示します。 さまざまなレコードの種類の使用方法を確認します。 選択するレコードの種類によって、レコードの情報がどのように変わるかに注目してください。

1. 例として **A** レコードを作成します。 

**自動登録用の VNet をリンクする**

1.  DNS ゾーンがデプロイされたら、受講者と一緒に概要ページを確認します。
1.  プライベート DNS ゾーンを仮想ネットワークにリンクするには、仮想ネットワーク リンクを作成します。
1.  左側のウィンドウで、[Virtual network links](仮想ネットワーク リンク) を選択します。
1.  [追加] を選択します。
1.  [リンク名]に「myLink」と入力します。
1.  [仮想ネットワーク] で [myAzureVNet] を選択します。
1.  [Enable auto registration](自動登録を有効にする) チェック ボックスをオンにします。
1.  [OK] を選択します。

>**注**: 受講者は LAB_05 を完了できるようになりました