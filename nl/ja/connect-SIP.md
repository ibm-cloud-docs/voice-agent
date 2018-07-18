---

copyright:
  years: 2018
lastupdated: "2018-06-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# SIP トランクの接続
{: #connect}

以下のリストから、{{site.data.keyword.iva_full}} との統合に使用する SIP トランク・プロバイダーを選択できます。
{: #shortdesc}

* [NetFoundry](#NetFoundry-setup)
* [Twilio](#twilio-setup)
* [AT&T やその他のプロバイダー](#att-other)
* [{{site.data.keyword.iva_short}} とのピアリング](#peering)
* [要補助セットアップの要求](#request-setup)

## NetFoundry SIP トランクと電話番号の作成
{: #NetFoundry-setup}

**注:** アカウントを作成するには、クレジット・カードが必要です。使用量に基づいて定期的にこのカードに課金されます。 既に NetFoundry アカウントを持っている場合は、既存のアカウントを使用することができます。

1. [NetFoundry ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson.netfoundry.io/watson-login){: new_window} の Web サイトでアカウントを作成します。

1. _Watson アカウント_のメインページに移動します。

1. 番号を取得する地域を選択します。

  **注:** Netfoundry Web サイトで、使用可能な地域を確認してください。 常に新しい地域が追加されています。

1. **「購入」**をクリックし、画面の説明に従って購入を実行します。

1. 支払いが正常に処理されると、SIP トランク電話番号がアカウントに表示されます。

この電話番号 (国コードと地域コードを含む) がボイス・エージェントのセットアップおよび通話中転送の構成に必要になります。 [ボイス・エージェントの作成と接続](getting-started.html#step3)を参照してください。


## Twilio SIP トランクの作成
{: #twilio-setup}

**注:** [Twilio アカウント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.twilio.com/try-twilio){: new_window} を作成するにはクレジット・カードが必要です。構成する SIP トランクの使用量に応じてこのカードに定期的に課金されます。 すでに Twilio アカウントを持っている場合は、既存のアカウントを使用することができます。

  1. [Twilio Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.twilio.com/try-twilio){: new_window} で Twilio アカウントを作成します。

  1. Twilio アカウントを使用して SIP トランクを作成します。

  1. Twilio Web サイトから、「弾力的な SIP トランクの接続 (Elastic SIP Trunking)」ダッシュボードに移動します。

  1. ナビゲーション・バーから**「Trunks (トランク)」**を選択して、SIP トランクを作成します。 すでに SIP トランクがある場合は、**「+」**アイコンをクリックします。 それによって表示されるダイアログ・ボックスに
SIP トランクの名前を入力し、**「Create (作成)」**をクリックします。

  1. 「Elastic SIP Trunks (エラスティック SIP トランク)」ページから、使用する SIP トランクを選択します。

  1. SIP トランクのナビゲーション・バーから**「Origination (起点)」**を選択して、起点の SIP URI を構成します。 サービス障害を未然に防ぐために、**「+」**アイコンを選択して複数のホスト名を指定することができます。

  ここで指定する IP アドレスまたはホスト名は、{{site.data.keyword.iva_short}} サービス・インスタンスの_「開始 (Getting started)」_ダッシュボードでメモした値です。 起点 URI を構成する場合、その URI は SIP URI 形式 (例、`sip:us-south.voiceagent.cloud.ibm.com/`) でなければなりません。 複数のホスト名または IP アドレスを指定しておくと、最初のホスト・エンドポイントで障害が発生したり、サービス休止になったりした場合、SIP トランク・プロバイダーはリストの次のホスト名に通話を切り替えます。

  1. SIP トランクのナビゲーション・バーから**「Numbers (番号)」**を選択します。 その後、電話番号を作成し、使用する SIP トランクにその番号を割り当てます。

  「Numbers (番号)」ページで、**「Buy a Number (番号の購入)」**をクリックするか、またはすでに番号を持っている場合は**「+」**アイコンをクリックします。 パネルが表示されるので、そのパネルで自分の地域内の新しい電話番号をプロビジョンすることができます。 SIP トランクに戻って「Number (番号)」アイコンをクリックし、作成した SIP トランクにその番号を割り当てます。

  この電話番号は、国コードおよび地域コードとともに、ボイス・エージェントのセットアップに必要です。 [ボイス・エージェントの作成と接続](getting-started.html#step3)を参照してください。


## AT&T やその他のプロバイダーとの接続
{: #att-other}

{{site.data.keyword.iva_short}} では、AT&T&reg; やその他の SIP トランキング・プロバイダーとの接続がサポートされています。 ただし、それらの接続はセルフサービスのセットアップではなく、特別な支援が必要になります。 [要補助セットアップの要求](#request-setup)を参照してください。

## {{site.data.keyword.iva_short}} とのピアリング
{: #peering}

{{site.data.keyword.iva_short}} では、IPSec トンネルなどのピア接続がサポートされています。 ただし、それらの接続はセルフサービスのセットアップではなく、特別な支援が必要になります。 [要補助セットアップの要求](#request-setup)を参照してください。

## 要補助セットアップの要求
{: #request-setup}

AT&T やその他の SIP トランキング・プロバイダーと接続したり、{{site.data.keyword.iva_short}} とピア接続したり、あるいは 50 より多くの同時接続を要求したりするには、以下の手順で要補助ネットワーク・セットアップを要求します。

1. 新しい [{{site.data.keyword.Bluemix_notm}} サポート・チケット](https://console.bluemix.net/unifiedsupport/tickets/add)を開きます。

1. **「チケット・タイプ」**は**「技術的」**を選択します。

1. **「リソース・コンテキストを選択します」**は**「Cloud Foundry」**を選択します。

1. **「サポートの技術的領域」**は**「アプリケーション・サービス」**を選択します。

1. {{site.data.keyword.iva_short}} インスタンスの**「地域」**、**「組織」**、および**「スペース」**を選択します。

1. **「関連するリソース」**にはご使用の {{site.data.keyword.iva_short}} サービス・インスタンスを選択します。

1. **「重大度」**は**「重大度 4 - 最小の影響」**を選択します。

1. **「件名」**には、「`{{site.data.keyword.iva_short}} 要補助ネットワーク・セットアップ`」と入力します。

1. **「要旨」**セクションで、{{site.data.keyword.iva_short}} サービスに接続したいこと、または、ボイス・エージェントのために 50 より多い同時接続を要求したいことを説明します。 SIP トランキング・プロバイダーか、IPSec トンネルのようなピア接続のいずれかを使用して接続できます。 チケットに、ネットワーク・トポロジーを説明する PDF か画像形式のネットワーク図を添付することができます。 また、希望のサービス機能を詳しく説明するホワイト・ペーパーを添付することもできます。