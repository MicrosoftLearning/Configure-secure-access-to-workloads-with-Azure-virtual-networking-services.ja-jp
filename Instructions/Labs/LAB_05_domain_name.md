---
lab:
  title: '演習 05: DNS ゾーンを作成して DNS 設定を構成する'
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# 演習 05: DNS ゾーンを作成して DNS 設定を構成する

## シナリオ

組織では、内部通信に IP アドレスの代わりにドメイン名を使用するワークロードが必要です。  組織では、カスタム DNS ソリューションを追加したくありません。 これらの要件を特定します。
+ contoso.com には単一の**プライベート DNS ゾーン**が必要です。
+ DNS では、app-vnet への**仮想ネットワーク リンク**が使用されます。 
+ バックエンド サブネットには、新しい **DNS レコード** が必要です。 

## スキルアップ タスク

+ プライベート DNS ゾーンを作成および構成する。
+ DNS レコードを作成して構成する。
+ 仮想ネットワークで DNS 設定を構成する。
  
## アーキテクチャの図

![仮想ネットワークにリンクされた Azure DNS の図。](../Media/task-5.png)



## 演習の手順

**注:** この演習では、ラボ 01 の仮想ネットワークとサブネットをインストールする必要があります。 これらのリソースをデプロイする必要がある場合は、[テンプレート](https://github.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/blob/main/Allfiles/Labs/All-Labs/create-vnet-subnets-template.json)が提供されます。

### プライベート DNS ゾーンの作成

[Azure プライベート DNS](https://learn.microsoft.com/azure/dns/private-dns-overview) は、信頼性が高くセキュリティで保護された DNS サービスを提供し、カスタムの DNS ソリューションの追加を必要とせずに、仮想ネットワークでドメイン名を管理および解決します。 プライベート DNS ゾーンを使用することにより、Azure で提供される名前ではなく、独自のカスタム ドメイン名を使用できます。

1. Azure portal で、`Private dns zones` を検索して選択します。

1. **[+ 作成]** を選択して DNS ゾーンを構成します。 

    | プロパティ       | 値                        |
    | :------------- | :--------------------------- |
    | サブスクリプション   | **サブスクリプションを選択します** |
    | リソース グループ | **RG1**                      |
    | Name           | `private.contoso.com`              |
    | リージョン         | **米国東部**                  |

1. **[確認と作成]**、**[作成]** の順に選択します。

1. DNS ゾーンのデプロイを待ってから、**[リソースに移動]** を選択します。 

### プライベート DNS ゾーンへの仮想ネットワーク リンクを作成する

プライベート DNS ゾーンの DNS レコードを解決するには、リソースをプライベート ゾーンにリンクする必要があります。 [仮想ネットワーク リンク](https://learn.microsoft.com/azure/dns/private-dns-virtual-network-links)は、仮想ネットワークをプライベート ゾーンに関連付けます。

1. ポータルで、**private.contoso.com** DNS ゾーンでの作業を続行します。 

1. **[DNS 管理]** ブレードで、**[+ 仮想ネットワーク リンク]** を選択します。

1. **[+ 追加]** を選択し、仮想ネットワーク リンクを構成します。 

    | プロパティ                 | 値             |
    | :----------------------- | :---------------- |
    | リンク名                | `app-vnet-link` |
    | 仮想ネットワーク          | **app-vnet**      |
    | 自動登録を有効にする | **Enabled**       |

1. **[作成]** を選択し、デプロイが完了するまで待ちます。 必要に応じて、ページを**更新**してください。 

### DNS レコード セットを作成する

[DNS レコード](https://learn.microsoft.com/en-us/azure/dns/dns-zones-records#dns-records)は、DNS ゾーンに関する情報を提供します。 

1. ポータルで、**private.contoso.com** DNS ゾーンでの作業を続行します。 

1. **[DNS 管理]** ブレードで、**[+ レコードセット]** を選択します。

1. 仮想マシンごとに 2 つの A レコードが自動的に作成されていることがわかります。 

1. **[+ 追加]** を選択し、レコード セットを構成します。 完了したら、**[追加]** を選択します。 
   
    | プロパティ   | 値        |
    | :--------- | :----------- |
    | 名前       | `backend`    |
    | Type       | **A**        |
    | TTL        | **1**        |
    | IP アドレス (IP address) | **10.1.1.5** |

**注:** このレコード セットは、プライベート IP アドレスが 10.1.1.5 の app-vnet に仮想マシンが存在します。

### オンライン トレーニングでさらに学習する

+ [Azure DNS の概要](https://learn.microsoft.com/training/modules/intro-to-azure-dns/)。 このモジュールでは、Azure DNS の機能、そのしくみ、および組織のニーズを満たすソリューションとして Azure DNS を使用することを選択すべきタイミングについて説明します。
+ [Azure DNS でドメインをホストする](https://learn.microsoft.com/training/modules/host-domain-azure-dns/)。 このモジュールでは、DNS ゾーンと DNS レコードを作成する方法について説明します。

### 要点

以上でこの演習は完了です。 重要なポイントを以下に示します。

+ Azure DNS は、ドメイン ネーム システム (DNS) ドメイン (DNS ゾーンともいう) をホストおよび管理できるクラウド サービスです。 
+ Azure DNS パブリック ゾーンでは、インターネット上のホストによって解決されるようにするレコードのドメイン ネーム ゾーン データをホストします。
+ Azure プライベート DNS ゾーンを使用すると、プライベート Azure リソースのプライベート DNS ゾーン名前空間を構成できます。
+ DNS ゾーンは、DNS レコードのコレクションです。 DNS レコードは、ドメインに関する情報を提供します。
