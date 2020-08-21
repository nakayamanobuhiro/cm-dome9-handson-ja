IAM Safety
========================================

IAM Safetyを利用することで平常時は特権が制限された状態にしつつ必要な時だけ動的に特権を付与することができます。

これにより、平常時のオペレーションミスの予防や不正行為の抑止を最小限度の手間で実現することができます。


IAM Safetyの有効化
----------------------------------------

IAM Safetyの仕組みを解説します。

IAM Safetyを利用するにあたり、IAM Groupと特権操作を明示的に拒否するIAM Policyを作成します。
IAM Safetyで保護されるIAM Userは、普段はこのIAM Groupのメンバーとなっており特権操作が制限されます。
Dome9で昇格したユーザーは一時的にグループのメンバーから削除され、特権操作が可能になります。
ただし、IAM Userに当初から特権が付与されている場合に限ります。
Dome9は明示的に特権操作を禁止することが可能ですが特権操作を付与することはありません。

.. figure:: /contents/images/IAM_Safety_Diag.png
  :align: center


1. [IAM PROTECTION] - [Accounts & IAM Users]を選択します。

.. figure:: /contents/images/iam_safety_1_001.png
  :align: center
  :scale: 80%


2. [開始]をクリックします。

.. figure:: /contents/images/iam_safety_1_002.png
  :align: center


3. Dome9で制限したいアクションを定義します。今回はコンピューティングリソース（EC2やそれに関連が深いサービス群）への操作を制限します。
[テンプレート]から[Compute]を選択し、[次へ]をクリックします。

.. figure:: /contents/images/iam_safety_1_003.png
  :align: center


4. IAM SafetyのためのIAM GroupおよびIAM Policyを作成します。
表示されているIAM Policyはあとで利用します。

.. figure:: /contents/images/iam_safety_1_004.png
  :align: center


5. AWSのマネージメントコンソールにログインし、[サービス] - [IAM]を選択します。


6. [ポリシー] - [ポリシーの作成]をクリックします。

.. figure:: /contents/images/iam_safety_1_005.png
  :align: center


7. [JSON]のタブをクリックし、Dome9のコンソールで表示されているIAM Policyをコピーして貼り付けます。

.. figure:: /contents/images/iam_safety_1_006.png
  :align: center


8. ポリシー名に[CloudGuard-Restricted-Policy]と入力し、[ポリシーの作成]をクリックします。

.. figure:: /contents/images/iam_safety_1_007.png
  :align: center


9. 次にIAM Groupを作成します。[グループ] - [新しいグループの作成]をクリックします。

.. figure:: /contents/images/iam_safety_1_008.png
  :align: center


10. グループ名に[CloudGuard-Restricted-Group]と入力し、次に進みます。


.. figure:: /contents/images/iam_safety_1_009.png
  :align: center


11. 作成したIAM Policyを選択し、次に進みます。

.. figure:: /contents/images/iam_safety_1_010.png
  :align: center


12. 内容を確認し、IAM Groupの作成を完了します。

.. figure:: /contents/images/iam_safety_1_011.png
  :align: center


13. Dome9に設定するIAM PolicyおよびIAM GroupのARNを確認します。[ポリシー]を選択し、[CloudGuard-Restricted-Policy]をクリックします。

.. figure:: /contents/images/iam_safety_1_012.png
  :align: center


14. [ポリシーARN]をコピーします。

.. figure:: /contents/images/iam_safety_1_013.png
  :align: center


15. Dome9のコンソールに戻り、[ポリシーARN]にコピーしたARNを貼り付けます。

.. figure:: /contents/images/iam_safety_1_014.png
  :align: center


16. [グループ]を選択し、[CloudGuard-Restricted-Group]をクリックします。

.. figure:: /contents/images/iam_safety_1_015.png
  :align: center


17. [グループのARN]をコピーします

.. figure:: /contents/images/iam_safety_1_016.png
  :align: center


18. Dome9のコンソールに戻り、[グループARN]にコピーしたARNを貼り付けます。次に進みます。

.. figure:: /contents/images/iam_safety_1_017.png
  :align: center


19. IAM Safetyを利用するAWSアカウントを選択し、次に進みます。

.. figure:: /contents/images/iam_safety_1_018.png
  :align: center


20. Dome9に対してIAM UserやIAM Group等への操作を許可するためにIAM Policyの作成およびIAM Roleへアタッチを行います。

.. figure:: /contents/images/iam_safety_1_019.png
  :align: center


21. [ポリシー] - [ポリシーの作成]をクリックします。

.. figure:: /contents/images/iam_safety_1_020.png
  :align: center


22. [JSON]のタブをクリックし、Dome9のコンソールで表示されているIAM Policyをコピーして貼り付けます。

.. figure:: /contents/images/iam_safety_1_021.png
  :align: center


23. ポリシー名に[CloudGuard-IAM-Policy]と入力し、[ポリシーの作成]をクリックします。

.. figure:: /contents/images/iam_safety_1_022.png
  :align: center


24. [ロール]を選択し、[CloudGuard-Connect]をクリックします。

.. figure:: /contents/images/iam_safety_1_023.png
  :align: center


25. [ポリシーをアタッチします]をクリックします。

.. figure:: /contents/images/iam_safety_1_024.png
  :align: center


26. [CloudGuard-IAM-Policy]を選択し、[ポリシーのアタッチ]をクリックします。

.. figure:: /contents/images/iam_safety_1_025.png
  :align: center


27. Dome9のコンソールに戻り設定を完了します。接続に成功すると以下の画面が表示されます。

.. figure:: /contents/images/iam_safety_1_026.png
  :align: center


保護するIAM Entityの作成
----------------------------------------

今回は、IAM Userを作成し、そのIAM UserをIAM Safetyで管理します。



1. [ユーザー] - [ユーザーを追加]をクリックします。

.. figure:: /contents/images/iam_safety_1_027.png
  :align: center


2. 以下の通り設定を実施します。設定したら、[次のステップ:アクセス権限]をクリックします。

- 任意のユーザー名を入力
- [AWSマネジメントコンソールへのアクセス]をチェック
- [パスワードリセットが必要]のチェックを外す（作業手順を減らすためにチェックを外します）

.. figure:: /contents/images/iam_safety_1_028.png
  :align: center


3. [既存のポリシーを直接アタッチ]を選択し、[AdministratorAccess]を選択して[次のステップ:タグ]をクリックします。

.. figure:: /contents/images/iam_safety_1_029.png
  :align: center


4. タグを設定せず次に進みます。

5. [ユーザーの作成]をクリックします。

.. figure:: /contents/images/iam_safety_1_030.png
  :align: center


6. 以下の情報をメモします。メモ帳などにコピーしてください。もしくは、[.csvのダウンロード]をクリックします。ダウンロードできるファイルに以下の情報が含まれます。

- サインインURL
- ユーザー
- パスワード

.. figure:: /contents/images/iam_safety_1_031.png
  :align: center


7. 作成したIAM UserでAWSのマネージメントコンソールにログインします。別のIAM Userでログインしている場合には一度ログアウトし、先ほどメモしたサインインURLにアクセスします。

.. figure:: /contents/images/iam_safety_1_032.png
  :align: center


8. 最初に作成したEC2インスタンスを利用して動作を確認します。[サービス] - [EC2]をクリックします。

.. figure:: /contents/images/iam_safety_1_033.png
  :align: center


9. [インスタンス]を選択し、起動しているEC2インスタンスを選択して[アクション] - [インスタンスの状態] - [停止]をクリックします。

.. figure:: /contents/images/iam_safety_1_034.png
  :align: center

10．停止したことを確認したら、起動します。[アクション] - [インスタンスの状態] - [開始]をクリックします。

.. figure:: /contents/images/iam_safety_1_034_2.png
  :align: center


IAM Userの保護（権限を制限）
----------------------------------------

作成したIAM Safetyで管理し、特権の行使を制限します。


1. [IAM PROTECTION] - [Accounts & IAM Users]を選択します。

.. figure:: /contents/images/iam_safety_1_001.png
  :align: center
  :scale: 80%

2. 作成したIAM Userを選択し、[すべて保護]をクリックします。

.. figure:: /contents/images/iam_safety_1_035.png
  :align: center


.. figure:: /contents/images/iam_safety_1_035_1.png
  :align: center


.. figure:: /contents/images/iam_safety_1_035_2.png
  :align: center


3. ステータスが[Protected]になったことを確認します。


.. figure:: /contents/images/iam_safety_1_036.png
  :align: center


4. 動作を確認します。[インスタンス]を選択し、起動しているEC2インスタンスを選択して[アクション] - [インスタンスの状態] - [停止]をクリックします。

.. figure:: /contents/images/iam_safety_1_037.png
  :align: center


5. [停止する]をクリックします。

.. figure:: /contents/images/iam_safety_1_038.png
  :align: center


6. 権限を制限されているためインスタンスができません（期待する動作です）。[キャンセル]をクリックします。

.. figure:: /contents/images/iam_safety_1_039.png
  :align: center


IAM Userの特権昇格
----------------------------------------

一時的に制限を緩和して特権へ昇格させます。


1. 保護したIAM Userに対して[ELEVATE]をクリックします。成功した場合、その旨が記載されたメッセージが上部に表示されます。

.. figure:: /contents/images/iam_safety_1_040.png
  :align: center


2. 特権に昇格できたことを確認します。[Active elevations]を開きます。

.. figure:: /contents/images/iam_safety_1_041.png
  :align: center


3. 昇格したIAM Userが存在することを確認します。[ELEVATE]をクリックした場合には昇格の期間が15分間であることが確認できます。[Expiration]を確認してください。

.. figure:: /contents/images/iam_safety_1_042.png
  :align: center


4. 動作を確認します。[インスタンス]を選択し、起動しているEC2インスタンスを選択して[アクション] - [インスタンスの状態] - [停止]をクリックします。

.. figure:: /contents/images/iam_safety_1_043.png
  :align: center

5. [停止する]をクリックします。

.. figure:: /contents/images/iam_safety_1_044.png
  :align: center


6. インスタンスの停止処理が開始されたことを確認します。

.. figure:: /contents/images/iam_safety_1_045.png
  :align: center

