Network Security
========================================

Network Securityでは、多数のクラウドアカウントにおいてネットワークアクセス制御の設定を効率的に管理することができます。

具体的には、意図しない変更の予防や時限的なアクセス許可を容易に実現できます。


ネットワークの可視化*
--------------------------------------------------------------------------------

* Clarityの機能は2020/1/1以降、Asset Management機能へ移行されました。

AWSアカウント上に作成されたネットワークポリシーを可視化します。
ネットワーク自体を可視化するのではなく、ポリシーを可視化する機能であることに留意してください。


1. [ASSET MANAGEMENT] - [Clarity]をクリックします。

.. figure:: /contents/images/dome9_8_001.png
  :align: center
  :scale: 80%
  

2. AWSアカウントをクリックします。

.. figure:: /contents/images/dome9_8_002.png
  :align: center


3. リージョンを選択します。続けてポリシーを可視化したいVPCをクリックし、[SECURITY GROUP]をクリックします。

.. figure:: /contents/images/dome9_8_003.png
  :align: center


4. [DMZ]のSecurity Groupをクリックします。

DMZ上にSecurity Groupが存在するということは、任意のIPアドレス (0.0.0.0/0) からアクセス可能であることを意味します。
そのSecurity Groupにどのようなリソースが関連付けられているか・どのようなポートが開放されているかを右側の詳細画面で確認できます。

.. figure:: /contents/images/dome9_8_004_1.png
  :align: center

.. figure:: /contents/images/dome9_8_004_2.png
  :align: center

Security Groupへのリンクをクリックすると、詳細を表示する画面に遷移します。

.. figure:: /contents/images/dome9_8_005.png
  :align: center


5. [Internal]のSecurity Groupをクリックします。（dome9-instanceではじまるリソースを選択します）

[Internal]にSecurity Groupが存在するということは、VPC内のリソースからアクセス可能であることを意味します。

.. figure:: /contents/images/dome9_8_006_1.png
  :align: center

.. figure:: /contents/images/dome9_8_006_2.png
  :align: center

Security Groupへのリンクをクリックすると、詳細を表示する画面に遷移します。

.. figure:: /contents/images/dome9_8_006_3.png
  :align: center

さらにEC2インスタンスへのリンクをクリックすると、特定のインスタンスの設定や関連するアラートをまとめて確認することができます（AWSのマネージメントコンソールは各サービス毎に画面が分かれています）。

[NETWORK SECURITY POLICIES]は、ENI、Security Group、NACLの情報が表示されます。

.. figure:: /contents/images/dome9_8_007_1.png
  :align: center

[IAM POLICIES]は、インスタンスにアタッチされたIAMロールの情報が表示されます。

.. figure:: /contents/images/dome9_8_007_2.png
  :align: center

[EVENTS ACTIVITY]は、Log.icを有効化して利用できます。CloudTrailに基づいてイベントが表示されます。

.. figure:: /contents/images/dome9_8_007_3.png
  :align: center

[TRAFIC ACTIVITY]は、Log.icを有効化して利用できます。VPC Flow Logsに基づいてネットワークログが表示されます。

.. figure:: /contents/images/dome9_8_007_4.png
  :align: center

[ENTITY VIEWER]は、インスタンスに関するメタデータが表示されます。

.. figure:: /contents/images/dome9_8_007_5.png
  :align: center

[ALERTS & FINDINGS]は、Comliance Rules、Log.ic、Inspector、GuardDutyから発せられたALERTやFINDINGSが表示されます。

.. figure:: /contents/images/dome9_8_007_6.png
  :align: center

[PROPERTIES]は、インスタンスのプロパティが表示されます。

.. figure:: /contents/images/dome9_8_007_7.png
  :align: center


Security Groupで利用するIPアドレスの管理
--------------------------------------------------------------------------------

Dome9ではSecurity Groupで設定するIPアドレス・ネットワークアドレスをIP Listというオブジェクトとして管理することができます。
これにより、アドレスのコンテキストを把握しやすくなります。
また、IP Listを変更することでそのIP Listを利用して設定されたSecurity Groupを一括で変更することも可能です。


1. [NETWORK SECURITY] - [IP Lists] - [追加]をクリックします。

.. figure:: /contents/images/ip_1_001.png
  :align: center


2. [Name]および[説明]を入力し、[作成]をクリックします。

.. figure:: /contents/images/ip_1_003.png
  :align: center


3. IPアドレスを入力し、[ADD]をクリックします。

以下の画面では、RFCで定義されているドキュメンテーション用のネットワークアドレスを設定しています。

.. figure:: /contents/images/ip_1_004.png
  :align: center


4. IP ListにIPアドレスが追加されたことを確認し、[SAVE]をクリックします。

.. figure:: /contents/images/ip_1_005.png
  :align: center


5. 作成したIP Listを利用してSecurity Groupを設定します。[NETWORK SECURITY] - [Security Groups]をクリックします。

.. figure:: /contents/images/ip_1_006.png
  :align: center
  :scale: 80%


6. 最初に作成したVPCのIDでフィルタリングし、EC2用のセキュリティグループ（Security Groupの名前に"Instance"を含む）をクリックします。

.. figure:: /contents/images/ip_1_007.png
  :align: center


7. さきほど作成したIP ListからSSHでアクセスすることを許可します。[+]をクリックします。

.. figure:: /contents/images/ip_1_008.png
  :align: center


8. [Service Type]を[SSH]に変更します。[Port Behavior]が[Limited]に変更されることを確認します。併せて、[ADD SOURCE]をクリックします。

.. figure:: /contents/images/ip_1_009.png
  :align: center


9. [IP LIST (CUSTOMER MANAGED)] - [（作成したIP List名）]を選択します。併せて、[CREATE SERVICE]をクリックします。

.. figure:: /contents/images/ip_1_009_2.png
  :align: center


10. Inbound ServiceにSSHの許可ルールが追加されていることを確認します。

.. figure:: /contents/images/ip_1_010.png
  :align: center


11. 併せて、AWSのマネージメントコンソール上でも設定が追加されていることを確認します。

.. figure:: /contents/images/ip_1_011.png
  :align: center


Dynamic Accessによる一時的なアクセス許可
----------------------------------------

Dynamic Accessは、一定時間のみ特定のIPアドレスからのアクセスを許可することができる機能です。
設定した時間を経過すると、Dome9によって許可設定が自動で削除されます。


1. [NETWORK SECURITY] - [Dynamic Access]をクリックします。

.. figure:: /contents/images/dynamic_access_1_001.png
  :align: center
  :scale: 80%


2. 最初に作成したVPCのIDでフィルタリングし、EC2インスタンスに割り当てられたSecurity GroupのSSHアクセスを許可するルールに対して[GET ACCESS]をクリックします。

これで、Dome9のコンソールにアクセスししている環境からのアクセスが許可されました。
今のネットワーク環境（グローバルIPアドレス）は以下から確認できます。

http://checkip.amazonaws.com/

.. figure:: /contents/images/dynamic_access_1_002.png
  :align: center


3. 一時的な許可が完了していることを確認します。[Active Leases]をクリックします。

.. figure:: /contents/images/dynamic_access_1_003.png
  :align: center


4. http://checkip.amazonaws.com/ で確認したIPアドレスからのアクセスが許可されていることを確認します。

.. figure:: /contents/images/dynamic_access_1_004.png
  :align: center


5. 併せて、AWSのマネージメントコンソール上でも設定が追加されていることを確認します。

.. figure:: /contents/images/dynamic_access_1_005.png
  :align: center


6. 次は、アクセスを許可するIPアドレスを明示的に指定します。[Custom Lease]をクリックします。

.. figure:: /contents/images/dynamic_access_1_006.png
  :align: center


7. アクセスを許可するIPアドレスを入力し、[SAVE]をクリックします。

.. figure:: /contents/images/dynamic_access_1_007.png
  :align: center


8. 併せて、AWSのマネージメントコンソール上でも設定が追加されていることを確認します。

.. figure:: /contents/images/dynamic_access_1_008.png
  :align: center


Full ProtectionによるSecurity Groupの保護
--------------------------------------------------------------------------------

Full Protectionが有効なSecurity Groupは、Dome9を経由しない変更を検知するとDome9によって元の設定に戻されます。


1. Security Groupの設定を確認します。
[NETWORK SECURITY] - [Security Groups]をクリックします。併せて、作成したVPCでフィルタリングを行います。
今回は、[default]で動作を確認します。
[default]をクリックします。

.. figure:: /contents/images/full_protection_1_001.png
  :align: center


2．[FULL PROTECTION]が有効になっていることを確認します。
有効になっていない場合には有効化します。
併せて、現在のSeurity Groupの設定を確認します。
[Inbound Services]では、[default]から任意のポートでアクセスできます。
今回は、任意のIPアドレスから任意のポートにアクセスできるような変更を加え、それが検知されて元に戻ることを確認します。

.. figure:: /contents/images/full_protection_1_002.png
  :align: center


3. AWSのマネージメントコンソールにログインし、VPCのコンソールを開きます。
[セキュリティグループ]を選択し、[default]のSecurity Groupを選択します。
[インバウンドのルール]のタブを選択し、[ルールの編集]をクリックします。

.. figure:: /contents/images/full_protection_1_003.png
  :align: center


4. 既存のインバウンドのルールを[ソース : カスタム, "0.0.0.0/0"]に変更し、[ルールの保存]をクリックします。

.. figure:: /contents/images/full_protection_1_004.png
  :align: center


5. インバウンドのルールが変更されたことを確認します。
Dome9によって設定が戻されるまでしばらく（10分～15分）待ちます。
マネージメントコンソール上でインバウンドのルールがロールバックされたことを確認したらDome9のコンソールに戻ります。

ロールバック前の状態がこちらです。

.. figure:: /contents/images/full_protection_1_005_1.png
  :align: center

ロールバック後の状態がこちらです。

.. figure:: /contents/images/full_protection_1_005_2.png
  :align: center


6. 操作したSeurity Groupを開き、[History]の直近のイベントを開きます。

.. figure:: /contents/images/full_protection_1_006.png
  :align: center


7. [Dome9 Audit - Security Group Tamper Detected And Handled]というメッセージがあることを確認します。これはDome9がDome9を経由しない変更を検出し設定を元に戻したことを示す記録です。

.. figure:: /contents/images/full_protection_1_007.png
  :align: center




