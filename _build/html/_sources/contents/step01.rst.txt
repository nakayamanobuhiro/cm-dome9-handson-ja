AWSアカウントの追加
========================================

この章では、Dome9で評価するリソースの作成とAWSアカウントをDome9に登録する手順を説明します。

.. contents::
  :local:


評価対象のリソースを作成
----------------------------------------

Dome9で評価するリソースを作成します。
（最初に作成するのは、Dome9ではリソースを作成してから評価できるようになるまでに時間がかかるためです）

リソースの作成はCloudFormationを利用して行います。

作成される環境は以下のとおりです。

.. figure:: /contents/images/env_diag.png
  :align: center


1. 【AWS】AWS コンソールにログインします。ログイン後、リージョンとして **東京リージョン** が選択されていることを確認します。

.. figure:: /contents/images/dome9_1_006.png
  :align: center


.. figure:: /contents/images/dome9_2_001.png
  :align: center


2. 【AWS】CloudFormationでリソースを作成します。[サービスを検索する]のテキストボックスに[CloudFormation]と入力します。

.. figure:: /contents/images/dome9_2_002.png
  :align: center


3. 【AWS】[スタックの作成] - [新しいリソースを使用(標準)]をクリックします。

.. figure:: /contents/images/dome9_2_003.png
  :align: center


4. 【AWS】[前提条件]として[テンプレートの準備完了]を選択します。 併せて、[テンプレートの指定]として[テンプレートファイルのアップロード]を選択します。以下のリンクからダウンロードしたCloudFormationテンプレートをアップロードし、[次へ]をクリックします。

https://dome9-handson-cfn-template-2020-02.s3-ap-northeast-1.amazonaws.com/handson.yml

.. figure:: /contents/images/dome9_2_004.png
  :align: center


5. 【AWS】スタック名を入力し、[次へ]をクリックします。

.. figure:: /contents/images/dome9_2_005.png
  :align: center


6. 【AWS】[次へ]をクリックします。


7. 【AWS】[スタックの作成]をクリックします。


8. 【AWS】スタックの作成が成功したことを確認します。

.. figure:: /contents/images/dome9_2_008.png
  :align: center



9. 【AWS】[リソース]のタブを選択し、作成されたVPCのIDをメモします。（評価を実行する際に利用します）

.. figure:: /contents/images/dome9_2_009.png
  :align: center


AWSリソースの作成は以上です。
ただし、AWSのマネージメントコンソールを閉じないでください。
Dome9の設定を行うために引き続きAWSのマネージメントコンソールを操作します。


AWSアカウントの追加
----------------------------------------

Dome9にAWSアカウントを登録します。

Dome9のアカウントを作成していない場合には、サインアップを行ってください。
なお、サインアップを行う際のメールアドレスは業務で利用しているものを利用してください。
"@gmail.com"などのメールアドレスではサインアップできません。

https://secure.dome9.com/v2/register/invite


1. 【Dome9】Dome9のアカウントにログインします。

https://secure.dome9.com/v2/login

.. figure:: /contents/images/dome9_1_001.png
  :align: center

.. figure:: /contents/images/dome9_1_001_1.png
  :align: center


2. 【Dome9】表示言語を変更します。[(ログインユーザー名)] - [Language] - [日本語]をクリックします。これ以降、日本語表示になっていることを前提に説明します。

.. figure:: /contents/images/dome9_1_002.png
  :align: center


3. 【Dome9】AWSアカウントの追加を開始します。[ASSET MANAGEMENT] - [On-Boarding] - [Get started with AWS]を選択します。

.. figure:: /contents/images/dome9_1_003.png
  :align: center


4. 【Dome9】オペレーションモードを選択します。Dome9には2つのモードが存在します。AWSアカウントの設定を読み取って評価する[モニターモード]と、不適切な設定を自動で修正可能な[完全保護モード]です。 **このハンズオンでは[完全保護モード]を選択してください。**

.. figure:: /contents/images/dome9_1_004.png
  :align: center


5. 【Dome9】Dome9用のポリシーの作成を開始します。以降、ブラウザに表示されている手順に従って作業を進めます。

.. figure:: /contents/images/dome9_1_005.png
  :align: center


6. 【AWS】AWS コンソールにログインします。

.. figure:: /contents/images/dome9_1_006.png
  :align: center



7. 【AWS】[サービス]をクリックし、[IAM]を選択します。 

.. figure:: /contents/images/dome9_1_007.png
  :align: center



8. 【AWS】[ポリシー]を選択し、[ポリシーを作成]ボタンをクリックします。 

.. figure:: /contents/images/dome9_1_008.png
  :align: center



9. 【AWS】[JSON]タブを選択します。 


.. figure:: /contents/images/dome9_1_009.png
  :align: center



10. 【Dome9】ポリシーをコピーし、ペーストします。

.. figure:: /contents/images/dome9_1_010_1.png
  :align: center


.. figure:: /contents/images/dome9_1_010_2.png
  :align: center




11. 【AWS】[ポリシーの確認]をクリックします。

.. figure:: /contents/images/dome9_1_011.png
  :align: center




12. 【AWS】ポリシーに[dome9-readonly-policy]という名前をつけ、[ポリシーの作成]をクリックします。 

.. figure:: /contents/images/dome9_1_012.png
  :align: center


13. 【AWS】[ポリシーを作成]ボタンをもう一度クリックします。 

.. figure:: /contents/images/dome9_1_008.png
  :align: center



14. 【AWS】[JSON]タブを選択します。 

.. figure:: /contents/images/dome9_1_009.png
  :align: center


15. 【Dome9】ポリシーをコピーし、ペーストします。 コピー  


.. figure:: /contents/images/dome9_1_015_1.png
  :align: center

.. figure:: /contents/images/dome9_1_015_2.png
  :align: center

.. figure:: /contents/images/dome9_1_015_3.png
  :align: center


16. 【AWS】ポリシーに[dome9-write-policy]という名前をつけ、[ポリシーの作成]をクリックします。 

.. figure:: /contents/images/dome9_1_016.png
  :align: center


17. 【Dome9】[次へ]をクリックします。


18. 【AWS】[ロール] - [ロールの作成]をクリックします。 

.. figure:: /contents/images/dome9_1_018.png
  :align: center




19. 【AWS/Dome9】ロールタイプを選択し、[別のAWS アカウント]をクリックます。併せて、[外部IDが必要]のチェックボックスにチェックします。以下の値を入力します。[次のステップ:アクセス権限]をクリックします。

- アカウントID : (Dome9のコンソールに表示されている12桁の数字)
- 外部ID : (Dome9のコンソールに表示されている文字列)
- MFAが必要 : チェックしない

.. figure:: /contents/images/dome9_1_019_1.png
  :align: center

.. figure:: /contents/images/dome9_1_019_2.png
  :align: center



20. 【AWS】以下のポリシーを選択し、[次のステップ:タグ]をクリックします。

- [SecurityAudit] (AWS管理ポリシー)
- [AmazonInspectorReadOnlyAccess] (AWS管理ポリシー)
- [dome9-readonly-policy] (フィルタで「dome9」と検索します。)
- [dome9-write-policy]

.. figure:: /contents/images/dome9_1_020.png
  :align: center


21. 【AWS】[次のステップ:確認]をクリックします。



22. 【AWS】ロール名に[Dome9-Connect]という名前を付け、［ロールの作成］をクリックします。

.. figure:: /contents/images/dome9_1_022.png
  :align: center


23. 【AWS】検索ボックスを使用して、前のステップで作成したロール名を探しクリックします。

.. figure:: /contents/images/dome9_1_023.png
  :align: center



24. 【AWS/Dome9】ロールARNをコピーし、右の[ロールARN]フィールドにペーストします。

.. figure:: /contents/images/dome9_1_024_1.png
  :align: center

.. figure:: /contents/images/dome9_1_024_2.png
  :align: center


25. 【Dome9】[NEXT]をクリックします。 


26. 【Dome9】[終了]をクリックします。（Organizational Unitに関する設定は行いません。）


27. 【Dome9】AWSアカウントがDome9に接続できたことを確認します。

.. figure:: /contents/images/dome9_1_027.png
  :align: center



AWSアカウントの追加は以上です。





