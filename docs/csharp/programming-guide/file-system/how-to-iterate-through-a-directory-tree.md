---
title: "方法: ディレクトリ ツリーを反復処理する (C# プログラミング ガイド) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- iterating through folders [C#]
- file iteration [C#]
ms.assetid: c4be4a75-6b1b-46a7-9d38-bab353091ed7
caps.latest.revision: 10
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c63e18bc7e23a9fda4a005745174bdd6c85b3f08
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-iterate-through-a-directory-tree-c-programming-guide"></a>方法 : ディレクトリ ツリーを反復処理する (C# プログラミング ガイド)
"ディレクトリ ツリーを反復処理する" とは、指定したルート フォルダー以下の入れ子になっている各サブディレクトリ内の各ファイルにアクセスすることです。 必ずしもファイルを 1 つ 1 つ開く必要はありません。 ファイルまたはサブディレクトリの名前だけを `string` として取得することも、その他の情報を <xref:System.IO.FileInfo?displayProperty=fullName> オブジェクトまたは <xref:System.IO.DirectoryInfo?displayProperty=fullName> オブジェクトの形式で取得することもできます。  
  
> [!NOTE]
>  Windows では、"ディレクトリ" と "フォルダー" という用語は同義です。 多くのドキュメントおよびユーザー インターフェイスのテキストでは、"フォルダー" という用語が使用されていますが、[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] クラス ライブラリでは、"ディレクトリ" という用語が使用されています。  
  
 最も容易なケース、つまり、指定したルート以下のすべてのディレクトリのアクセス許可があることが確実にわかっている場合は、`System.IO.SearchOption.AllDirectories` フラグを使用できます。 このフラグは、指定したパターンと一致する、入れ子にされたすべてのサブディレクトリを返します。 このフラグを使用する方法を次の例に示します。  
  
```csharp  
root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories);  
```  
  
 この方法の弱点は、指定したルート以下のサブディレクトリの 1 つが <xref:System.IO.DirectoryNotFoundException> または <xref:System.UnauthorizedAccessException> を発生させた場合、メソッド全体が失敗し、ディレクトリが返されないという点です。 <xref:System.IO.DirectoryInfo.GetFiles%2A> メソッドを使用する場合も同様です。 特定のサブフォルダーに関するこのような例外を処理する必要がある場合は、次の例のように、ディレクトリ ツリーを手動で移動する必要があります。  
  
 ディレクトリ ツリーを手動で移動するときは、最初にサブディレクトリを処理 ("*先行順走査*") するか、最初にファイルを処理 ("*後順走査*") できます。 先行順走査を実行する場合、現在のフォルダー以下のツリー全体を移動してから、そのフォルダー自体に直接格納されているファイルを反復処理していきます。 このドキュメントで後述する例は、後順走査を実行しますが、先行順走査を実行するように簡単に変更できます。  
  
 また、再帰とスタック ベース走査のどちらを使用するかを選択できます。 このドキュメント内の後の例では、両方の方法を示しています。  
  
 ファイルおよびフォルダーに対してさまざまな操作を実行する必要がある場合は、単一のデリゲートを使用して呼び出すことができる個別の関数に操作をリファクタリングすることで、これらの例をモジュール化できます。  
  
> [!NOTE]
>  NTFS ファイル システムには、"*接合ポイント*"、"*シンボリック リンク*"、および "*ハード リンク*" の形式で "*リパース ポイント*" を含めることができます。 <xref:System.IO.DirectoryInfo.GetFiles%2A>、<xref:System.IO.DirectoryInfo.GetDirectories%2A> などの .NET Framework メソッドは、リパース ポイント以下のサブディレクトリを返しません。 この動作により、リパース ポイントが相互参照している場合に、無限ループに入るのが回避されます。 通常、ファイルを誤って変更または削除しないようにリパース ポイントを処理する場合は、十分な注意が必要です。 リパース ポイントを詳細に制御する必要がある場合は、プラットフォーム呼び出しまたはネイティブ コードを使用して、適切な Win32 ファイル システム メソッドを直接呼び出します。  
  
## <a name="example"></a>例  
 再帰を使用してディレクトリ ツリーを移動する方法を次の例に示します。 この再帰の方法は洗練されていますが、ディレクトリ ツリーが大きく、入れ子の階層が深いと、スタック オーバーフロー例外が発生する可能性があります。  
  
 ここで処理される例外や、各ファイルまたは各フォルダーに対して実行される操作は、あくまで例として用意したものです。 実際の要件を満たす際には、このコードを修正する必要があります。 詳細については、コード内のコメントを参照してください。  
  
 [!code-cs[csFilesandFolders#1](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-iterate-through-a-directory-tree_1.cs)]  
  
## <a name="example"></a>例  
 再帰を使用せずにディレクトリ ツリー内のファイルおよびフォルダーを反復処理する方法を、次の例に示します。 この方法では、後入れ先出し (LIFO: Last In First Out) スタックである、一般的な <xref:System.Collections.Generic.Stack%601> コレクション型を使用します。  
  
 ここで処理される例外や、各ファイルまたは各フォルダーに対して実行される操作は、あくまで例として用意したものです。 実際の要件を満たす際には、このコードを修正する必要があります。 詳細については、コード内のコメントを参照してください。  
  
 [!code-cs[csFilesandFolders#2](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-iterate-through-a-directory-tree_2.cs)]  
  
 通常、すべてのフォルダーをテストして、アプリケーションにフォルダーを開くアクセス許可があるかどうかを確認する作業には時間がかかります。 そのため、このコード例には、`try/catch` ブロック内の操作の該当部分のみが含まれています。 フォルダーへのアクセスが拒否されたときにアクセス許可を昇格して再びアクセスを試行するように、`catch` ブロックを修正できます。 原則として、アプリケーションが不明の状態にならずに処理できる例外のみをキャッチしてください。  
  
 ディレクトリ ツリーの内容をメモリまたはディスクに保存する必要がある場合、各ファイルの (`string` 型の) <xref:System.IO.FileSystemInfo.FullName%2A> プロパティのみを保存するのが最適な選択肢です。 その後、必要に応じて、この文字列を使用して新しい <xref:System.IO.FileInfo> オブジェクトまたは <xref:System.IO.DirectoryInfo> オブジェクトを作成するか、追加処理が必要なファイルを開くことができます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 堅牢性の高いファイル反復処理コードでは、ファイル システムの数多くの複雑な部分を考慮する必要があります。 詳細については、「[NTFS Technical Reference (NTFS テクニカル リファレンス)](http://go.microsoft.com/fwlink/?LinkId=79488)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.IO>   
 [LINQ とファイル ディレクトリ](http://msdn.microsoft.com/library/5a5d516c-0279-4a84-ac84-b87f54caa808)   
 [ファイル システムとレジストリ (C# プログラミング ガイド)](../../../csharp/programming-guide/file-system/index.md)