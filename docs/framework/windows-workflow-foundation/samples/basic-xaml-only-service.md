---
title: "基本的な XAML 専用サービス | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c106feb0-0245-43b5-aefe-93ce0e4d38eb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 基本的な XAML 専用サービス
このサンプルでは、XAML 専用サービスを作成する方法を示します。このシナリオは自動車関連の問題に対する診断サービスです。このサービスは、顧客に一連の質問をして問題を診断するワークフローとして実装されます。このサービスで診断できる問題は 2 種類です \(車のエンジンがかからない、または空調装置が動作しない\)。ワークフローでは、デザイナーの要求\/応答テンプレートを使用して、3 つの簡単なサービス操作を公開します。サービスは、 IIS に仮想ディレクトリを作成し、service1.xamlx ファイルおよび Web.config ファイルをその仮想ディレクトリにコピーすることによって IIS でホストされます。コンパイルされたコードは必要ありません。既定では、このサンプルでは、Visual Studi 2010 でのビルト時に、WCF および WF のサンプルのセットアップ手順 \([Windows Communication Foundation サンプルの 1 回限りのセットアップの手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)\) に従って作成する仮想ディレクトリに、必要なファイルが自動的にコピーされます:。  
  
#### このサンプルを使用するには  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] でプロジェクト ソリューションを読み込み、プロジェクトをビルドします。  
  
2.  \[ソリューションの基本ディレクトリ\]\\Client\\bin\\debug に生成されたクライアント アプリケーションを実行します。  
  
3.  オプションが出力されるので、オプションを選択します。質問が表示されたら、はいかいいえで \(Y キーまたは N キーを使用して\) 回答します。サービスによる問題の診断が完了すると、診断結果が出力されます。  
  
4.  オプションが再度表示されます。もう一度問題を診断することも、アプリケーションを終了することもできます。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Services\XAMLService`  
  
## 参照