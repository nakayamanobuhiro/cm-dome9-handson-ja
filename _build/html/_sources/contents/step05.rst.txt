リソースの削除
========================================

ハンズオンが終了したら、作成したAWSリソースの削除を行います。


CloudFormationで作成したVPCやEC2インスタンス等は費用が発生する場合がありますので削除をお願いします。


Dome9上のAWSアカウントの登録およびDome9を利用する為に作成したIAMのリソースは、評価を継続する場合には削除する必要はありません。
ただし、CloudTrailを有効にしているAWSアカウントではDome9によるAPIの呼び出しによって費用が発生する場合があります。


AWSリソースの削除作業を実施する際、削除に必要な権限を持ったIAM UserでAWSのマネージメントコンソールにログインしてください。


CloudFormation Stackの削除
----------------------------------------

CloudFormation Stackを削除します。
削除は以下の手順に従って行ってください。


https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/cfn-console-delete-stack.html


(Optional)IAM Safetyの無効化
----------------------------------------

IAM Safetyを無効化します。


1. [UAM Safety] - [Accounts & IAM Users]を選択します。


.. figure:: /contents/images/delete_001.png
  :align: center


2. IAM Safetyを有効化したAWSアカウントに対して、[アカウント保護の解除]をクリックします。


.. figure:: /contents/images/delete_002.png
  :align: center


3. [Unprotect]をクリックします。なお、この時点ではAWSアカウントの関連付けの解除までは完了していません。


.. figure:: /contents/images/delete_003.png
  :align: center


4. [アカウントの関連付けを解除]をクリックします。


.. figure:: /contents/images/delete_004.png
  :align: center


5. [Disassociate]をクリックします。


.. figure:: /contents/images/delete_005.png
  :align: center


以上でIAM Safetyの無効化は完了です。


(Optional)AWSアカウントの登録解除
----------------------------------------

Dome9からAWSアカウントを削除します。


1. [ASSET Management] - [Cloud Accounts]を選択します。


.. figure:: /contents/images/delete_006.png
  :align: center


2. 登録したAWSアカウントをクリックします。


.. figure:: /contents/images/delete_007.png
  :align: center


3. [削除]をクリックします。


.. figure:: /contents/images/delete_008.png
  :align: center


4. [削除]をクリックします。


.. figure:: /contents/images/delete_009.png
  :align: center


以上でAWSアカウントの登録解除は完了です。


(Optional)IAM Userの削除
----------------------------------------

IAM Safetyの動作確認用に作成したIAM Userを削除します。
削除は以下の手順に従って行ってください。


https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_users_manage.html#id_users_deleting


.. figure:: /contents/images/delete_010.png
  :align: center


(Optional)IAM Groupの削除
----------------------------------------

IAM Safetyのために作成したIAM Groupを削除します。
削除は以下の手順に従って行ってください。


https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_groups_manage_delete.html


.. figure:: /contents/images/delete_011.png
  :align: center


(Optional)IAM Roleの削除
----------------------------------------

AWSアカウントをDome9に登録するために作成したIAM Roleを削除します。
削除は以下の手順に従って行ってください。


https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_roles_manage_delete.html


.. figure:: /contents/images/delete_012.png
  :align: center


(Optional)IAM Policyの削除
----------------------------------------

IAM RoleおよびIAM Groupのために作成したIAM Policyを削除します。
削除は以下の手順に従って行ってください。

https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/access_policies_manage-delete.html


.. figure:: /contents/images/delete_013.png
  :align: center
