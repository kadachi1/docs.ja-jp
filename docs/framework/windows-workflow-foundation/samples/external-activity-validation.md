---
title: "外部アクティビティの検証 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49619f59-9819-484a-bcd8-5596308e8551
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 外部アクティビティの検証
このサンプルでは、ユーザーが作成するものではないビルトイン アクティビティに検証ロジックを追加する方法を示します。検証ロジックでは、ワークフロー内に存在するすべての <xref:System.Activities.Statements.If> アクティビティに <xref:System.Activities.Statements.If.Then%2A> または <xref:System.Activities.Statements.If.Else%2A> のいずれかのプロパティが強制的に設定されます。また、ワークフロー内に存在するすべての <xref:System.Activities.Statements.Pick> アクティビティに複数の分岐が含まれているかどうかが確認され、分岐が含まれていない場合は警告が生成されます。  
  
## サンプルの詳細  
 このサンプルでは、検証する各アクティビティ \(<xref:System.Activities.Statements.If> アクティビティと <xref:System.Activities.Statements.Pick> アクティビティ\) のインスタンスを含むワークフローを作成します。検証動作ごとに <xref:System.Activities.Validation.Constraint> を作成します。このサンプルで作成される制約は `ConstraintError_IfShouldHaveThenOrElse` と `ConstraintWarning_PickHasOneBranch` です。次に、これらの制約を <xref:System.Activities.Validation.ValidationSettings> インスタンスの `AdditionalConstraints` コレクションに追加します。最後に、<xref:System.Activities.Validation.ActivityValidationServices> の `static`<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> メソッドを呼び出してワークフロー内のアクティビティを検証し、検証結果をコンソールに出力します。  
  
> [!NOTE]
>  ポリシー制約は、任意のアクティビティに追加できます。たとえば、<xref:System.Activities.Statements.Sequence> または <xref:System.Activities.Statements.Parallel> アクティビティにポリシー制約を追加できます。  
  
#### このサンプルを使用するには  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] を使用して、ExternalActivityValidation.sln ファイルを開きます。  
  
2.  ソリューションをビルドするには、Ctrl キーと Shift キーを押しながら B キーを押します。  
  
3.  ソリューションを実行するには、Ctrl キーを押しながら F5 キーを押します。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Validation\ExternalActivityValidation`  
  
## 参照