Posture Management
========================================

Posture Managementでは、クラウドプラットフォーム上の状態・設定を走査およびリスクの検出を行うことができます。
また、継続的に検出を行うことも可能です。

リソースの評価
----------------------------------------

最初に作成したリソースを評価します。
今回は、[AWS Dome9 CheckUp]のRulesetを利用します。


1. [Posture Management] - [Compliance Rulesets]を選択します。


.. figure:: /contents/images/dome9_3_001.png
  :align: center


2. [AWS Dome9 CheckUp] - [評価を実行]をクリックします。見つけられない場合にはRuleset名をフィルターのテキストボックスに入力して絞り込んでください。


.. figure:: /contents/images/dome9_3_002.png
  :align: center


3. 評価対象を選択し、[RUN]をクリックします。見つけられない場合にはRuleset名をフィルターのテキストボックスに入力して絞り込んでください。

- [Cloud Account]: Dome9に追加したAWSアカウント
- [Region]: Tokyo（評価用のリソースを作成したリージョン）
- [VPC]: CloudFormationで作成したVPC


.. figure:: /contents/images/dome9_3_003.png
  :align: center



4. 評価結果を確認します。


.. figure:: /contents/images/dome9_3_004.png
  :align: center



評価対象のリソースの修正
----------------------------------------

修正の対象を特定し、修正と再評価を行います。


1. 以下の条件で絞り込みを行います。

- Rules passed/failed: failed
- Types: Instance


.. figure:: /contents/images/dome9_4_001.png
  :align: center


.. figure:: /contents/images/dome9_4_002.png
  :align: center


.. figure:: /contents/images/dome9_4_003.png
  :align: center


.. figure:: /contents/images/dome9_4_004.png
  :align: center


フィルタリングした結果、以下の2件のルールが検出されます。

.. figure:: /contents/images/dome9_4_005.png
  :align: center


評価ルールの詳細は以下のドキュメントを参照してください。


- Instance with administrative service: SSH (TCP:22) is too exposed to the public internet

  - https://gsl.dome9.com/D9.AWS.NET.AG4.Instance.22.TCP.html

- Instance with administrative service: SSH (TCP:22) is exposed to a wide network scope

  - https://gsl.dome9.com/D9.AWS.NET.AG5.Instance.22.TCP.html


----------------------------------------------------------------------------------------------------------------------------------------------------------------
"Instance with administrative service: SSH (TCP:22) is too exposed to the public internet"
----------------------------------------------------------------------------------------------------------------------------------------------------------------

ルール"Instance with administrative service: SSH (TCP:22) is too exposed to the public internet"による評価結果を確認し、問題点を是正します。


1.　評価結果を展開し、内容を確認します。

.. figure:: /contents/images/dome9_5_001.png
  :align: center


このルールによって、SSHでのアクセスをインターネット上の多くのホストに許可しているEC2インスタンスが不合格とされます。

不合格とされたEC2インスタンスのIDをクリックします。

.. figure:: /contents/images/dome9_5_002.png
  :align: center


2. 問題のあるインスタンスの設定を確認します。

Dome9のAsset Management機能を用いることで、保護されたリソースの設定を参照することができます。
以下の画面(Network Security Policies)では、ネットワークアクセス制御に関する設定（Security GroupのInbound/OutboundおよびNACLのInbound/Outbound）を1つの画面で確認することができます。
この画面から、任意のIPアドレスからSSHでのアクセスを許可しているSecurity Groupが存在していることが分かります。

Security Groupの名前をクリックします。

.. figure:: /contents/images/dome9_5_003.png
  :align: center


3. 任意のIPアドレスからSSHでのアクセスを許可しているルールを削除します。

.. figure:: /contents/images/dome9_5_004.png
  :align: center


.. figure:: /contents/images/dome9_5_005.png
  :align: center



----------------------------------------------------------------------------------------------------------------------------------------------------------------
"Instance with administrative service: SSH (TCP:22) is exposed to a wide network scope"
----------------------------------------------------------------------------------------------------------------------------------------------------------------

ルール"Instance with administrative service: SSH (TCP:22) is exposed to a wide network scope"による評価結果を確認し、問題点を是正します。

このルールによって、SSHでのアクセスを多数のホストに許可しているEC2インスタンスが不合格とされます。

このルールで指摘されている問題は、"Instance with administrative service: SSH (TCP:22) is too exposed to the public internet"に対する修正によって同時に解消されるため、追加作業は不要です。


リソースの再評価
----------------------------------------

修正完了後、同じRulesetで評価を実行します。

修正が評価結果に反映されるために10-20分程度必要とする場合があります。
期待する結果にならなかった場合、しばらく待ってから評価を再実行してください。

.. figure:: /contents/images/dome9_5_006.png
  :align: center


AWSリソースの評価と修正は以上です。


【参考】その他のルール
----------------------------------------

これ以外に[AWS Dome9 CheckUp]に含まれるルールの一部を紹介します。


--------------------------------------------------------------------------------
"Ensure IAM password policy require at least one symbol"
--------------------------------------------------------------------------------


- Ensure IAM password policy require at least one symbol

  - https://gsl.dome9.com/D9.AWS.IAM.10.html

--------------------------------------------------------------------------------
"Ensure IAM password policy expires passwords within 90 days or less"
--------------------------------------------------------------------------------



- Ensure IAM password policy expires passwords within 90 days or less

  - https://gsl.dome9.com/D9.AWS.IAM.15.html

--------------------------------------------------------------------------------
"Use Encrypted RDS storage"
--------------------------------------------------------------------------------


- Use Encrypted RDS storage

  - https://gsl.dome9.com/D9.AWS.CRY.05.html


--------------------------------------------------------------------------------
"Ensure a log metric filter and alarm exist for unauthorized API calls"
--------------------------------------------------------------------------------


- Ensure a log metric filter and alarm exist for unauthorized API calls

  - https://gsl.dome9.com/D9.AWS.MON.01.html


--------------------------------------------------------------------------------
"Ensure VPC flow logging is enabled in all VPCs"
--------------------------------------------------------------------------------


- Ensure VPC flow logging is enabled in all VPCs

  - https://gsl.dome9.com/D9.AWS.NET.03.html



評価の除外
----------------------------------------

Rulesetで定義した基準を全てのリソースが準拠していることが一般的には望ましいですが、業務上の要件等で満たせない・満たす必要がないケースがあります。
Dome9ではそのようなケースを例外として登録し評価対象から除外することができます。


1. [Posture Management] - [Assesment History]を選択します。

.. figure:: /contents/images/exclude_001.png
  :align: center


2．Ruleset [AWS Dome9 Checkup] で評価した最新の評価結果を開きます。

.. figure:: /contents/images/exclude_002.png
  :align: center


3. "Ensure IAM password policy expires passwords within 90 days or less"の評価結果を確認します。
ルール名で検索します。
新規作成したばかりのAWSアカウントの場合、不合格になっているはずです。
今回はこのルールによる評価を除外します。
評価結果を[展開]します。

.. figure:: /contents/images/exclude_003.png
  :align: center


4. [Actions]から、旗のアイコンをクリックします。


.. figure:: /contents/images/exclude_004.png
  :align: center


5. 新しい除外設定を作成します。
評価結果から画面遷移した場合、除外の対象となるAWSアカウントおよびエンティティは設定済です。
どのルールを除外するか（Exclude by Rule）は設定されていないので、この設定を追加します。

.. figure:: /contents/images/exclude_005.png
  :align: center


6. 除外するルールを選択およびコメントを入力し、[SAVE]をクリックします。


.. figure:: /contents/images/exclude_006.png
  :align: center


7. 除外設定が作成されたことを確認します。
[Posture Management] - [Exclusions]を選択します。


.. figure:: /contents/images/exclude_007.png
  :align: center


8. 実際に評価から除外されたか確認します。
[Posture Management] - [Complient Rulesets]を選択し、[AWS Dome9 Checkup]で[評価を実行]します。


.. figure:: /contents/images/exclude_008.png
  :align: center

.. figure:: /contents/images/exclude_009.png
  :align: center


9. ルール名で検索すると、合格として表示されます。
[SHOW EXCLUSIONS]を有効にすると、評価が除外されていることが確認できます。

.. figure:: /contents/images/exclude_010.png
  :align: center


.. figure:: /contents/images/exclude_011.png
  :align: center


