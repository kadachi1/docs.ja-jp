---
title: "DataSets、DataTables、および DataViews | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d4c4b69-8919-4224-8a65-6cca1c61b48f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataSets、DataTables、および DataViews
ADO.NET <xref:System.Data.DataSet> はメモリ常駐型のデータ表現であり、含まれているデータ ソースとは関係なく、一貫性のあるリレーショナル プログラミング モデルを提供します。  <xref:System.Data.DataSet> とは、テーブル間のリレーションシップだけでなく、包括するテーブル、整列するテーブル、およびデータを制約するテーブルを含むデータのセットを表します。  
  
 <xref:System.Data.DataSet> にはさまざまな使用方法があり、単独または組み合わせで使用できます。  次の操作を行うことができます。  
  
-   プログラムを使用して <xref:System.Data.DataSet> 内に <xref:System.Data.DataTable>、<xref:System.Data.DataRelation>、および <xref:System.Data.Constraint> を作成し、テーブルにデータを設定できます。  
  
-   `DataAdapter` を使用して、既存のリレーショナル データ ソースから取得したデータのテーブルで <xref:System.Data.DataSet> を作成できます。  
  
-   XML を使用して、<xref:System.Data.DataSet> の内容を読み込んだり、永続化したりできます。  詳細については、「[DataSet での XML の使用](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)」を参照してください。  
  
 厳密に型指定された <xref:System.Data.DataSet> も XML Web サービスを使用して転送できます。  <xref:System.Data.DataSet> は、XML Web サービスを使用してデータの転送が理想的に行えるように設計されています。  XML Web サービスの概要については、「[XML Web Services Overview](http://msdn.microsoft.com/ja-jp/9db0c7b8-bca6-462b-9be5-f5f9a7f05a4d)」を参照してください。  XML Web サービスから <xref:System.Data.DataSet> を使用する例については、「[XML Web サービスからの DataSet の使用](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/consuming-a-dataset-from-an-xml-web-service.md)」を参照してください。  
  
## このセクションの内容  
 [DataSet の作成](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-dataset.md)  
 <xref:System.Data.DataSet> のインスタンス作成に使用する構文について説明します。  
  
 [DataSet への DataTable の追加](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-a-datatable-to-a-dataset.md)  
 テーブルと列の作成方法および <xref:System.Data.DataSet> への追加方法について説明します。  
  
 [DataRelation の追加](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md)  
 <xref:System.Data.DataSet> のテーブル間のリレーションを作成する方法について説明します。  
  
 [DataRelation の移動](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations.md)  
 <xref:System.Data.DataSet> のテーブル間のリレーションを使用して、親子のリレーションシップに基づく子または親の行を返す方法について説明します。  
  
 [DataSet の内容のマージ](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/merging-dataset-contents.md)  
 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> の各配列の内容を別の <xref:System.Data.DataSet> にマージする方法について説明します。  
  
 [DataSet の内容のコピー](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/copying-dataset-contents.md)  
 指定されたデータだけでなく、スキーマを持つことができる <xref:System.Data.DataSet> のコピーを作成する方法について説明します。  
  
 [DataSet のイベント処理](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataset-events.md)  
 <xref:System.Data.DataSet> のイベントおよびその使用方法について説明します。  
  
 [型指定された DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)  
 型指定された <xref:System.Data.DataSet> の概要と、その作成および使用方法について説明します。  
  
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)  
 <xref:System.Data.DataTable> の作成方法、スキーマの定義方法、およびデータの操作方法について説明します。  
  
 [DataTableReaders](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatablereaders.md)  
 <xref:System.Data.DataTableReader> の作成方法および使用方法について説明します。  
  
 [DataViews](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)  
 `DataViews` の作成方法および操作方法、および <xref:System.Data.DataView> イベントの操作方法について説明します。  
  
 [DataSet での XML の使用](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 <xref:System.Data.DataSet> がデータ ソースとして XML と対話する方法を、<xref:System.Data.DataSet> の内容を XML データとして読み込んで永続化する方法と共に説明します。  
  
 [XML Web サービスからの DataSet の使用](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/consuming-a-dataset-from-an-xml-web-service.md)  
 <xref:System.Data.DataSet> を使用してデータを転送する XML Web サービスを作成する方法について説明します。  
  
## 関連項目  
 [ADO.NET の新機能](../../../../../docs/framework/data/adonet/whats-new.md)  
 ADO.NET の新機能について説明します。  
  
 [ADO.NET の概要](../../../../../docs/framework/data/adonet/ado-net-overview.md)  
 ADO.NET のデザインとコンポーネントを紹介します。  
  
 [DataAdapter からの DataSet の読み込み](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md)  
 **DataSet** にデータ ソースのデータを読み込む方法について説明します。  
  
 [DataAdapter によるデータ ソースの更新](../../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)  
 **DataSet** のデータに加えた変更をデータ ソースに反映する方法について説明します。  
  
 [DataSet への既存の制約の追加](../../../../../docs/framework/data/adonet/adding-existing-constraints-to-a-dataset.md)  
 **DataSet** にデータ ソースの主キー情報を設定する方法について説明します。  
  
## 参照  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)   
 [ADO.NET Managed Providers and DataSet Developer Center \(ADO.NET マネージ プロバイダーと DataSet デベロッパー センター\)](http://go.microsoft.com/fwlink/?LinkId=217917)