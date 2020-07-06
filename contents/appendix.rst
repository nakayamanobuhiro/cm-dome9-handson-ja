ハンズオンに含まれないDome9の機能
========================================

Dome9には上記の機能以外に以下のような機能を提供しています。

- Asset Management

  - Azure / GCP / Kubernetes

- Posture Management

  - Remediation
  - Compliance Policies

- Network Security

  - Flow Logs

- Log.ic

- IAM Protection

  - IAM Report


Asset Management
----------------------------------------

----------------------------------------
Azure / GCP / Kubernetes
----------------------------------------

AWS以外にも、Azure / GCP / k8sもDome9で保護することができます。
ただし、利用できる機能はクラウドサービスによって異なります。

Posture Management
----------------------------------------

----------------------------------------
Remediation
----------------------------------------

Compliance Rulesetでリスクがあると評価されたリソースに対してその是正を自動的に行うことが可能です。

https://dev.classmethod.jp/etc/dome9-remediation/

----------------------------------------
Compliance Policies
----------------------------------------

登録したクラウドサービスに対して指定したCompliance Rulesetによる評価を自動的に実行することができます。
また、評価結果を利用者に通知することができます。

https://dev.classmethod.jp/cloud/dome9-continuous-compliance/

この継続的な評価は特定のクラウドサービスのアカウントに対して実行することもできますし、アカウントをグループ化したOrganization Unitの単位で適用することも可能です。

Network Security
----------------------------------------

----------------------------------------
Flow Logs
----------------------------------------

VPC FlowLogsをDome9で集約し、フィルタリング等を行うことができます。

この機能はインシデント調査などに利用することができます。


Log.ic
----------------------------------------

クラウドサービスに対する管理アクティビティ（CloudTrail）およびネットワークアクティビティ（VPC FlowLogs）の可視化と分析を行うことができます。
Log.icはCheckpointの提供する脅威インテリジェンスを連携し、問題のあるアクティビティを検出することができます。
また、事前定義されたRuleSetを利用して継続的にアクティビティを評価することも可能です。

https://dev.classmethod.jp/cloud/aws/dome9-log-ic-introduction/

IAM Protection
----------------------------------------

----------------------------------------
IAM Report
----------------------------------------

IAM UserやIAM Roleに対して付与されている権限の分析や認証情報に関するレポートを提供します。
IAM Reportを利用することで、特定のアクションが許可されたIAMのEntityを特定したり、不適切な認証設定のIAM Entityを特定することが可能です。

https://dev.classmethod.jp/cloud/aws/dome9-iam-report/
