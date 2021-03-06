---
title: "関数型変換の適用範囲 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c78107bd-b006-4574-a3d4-bbf808388ff3
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0f79ec1e5975a1197464785182a7e6d4af4ba61c
ms.contentlocale: ja-jp
ms.lasthandoff: 05/22/2017


---
# <a name="applicability-of-functional-transformation-c"></a>関数型変換の適用範囲 (C#)
純粋関数型変換は、さまざまな状況で適用できます。  
  
 関数型変換の方法は、構造化されたデータのクエリと操作に適しているため、LINQ テクノロジに適切に対応できます。 ただし、関数型変換の適用範囲は、LINQ で使用する場合に比べてはるかに広範です。 データ形式の変換を中心とする処理はすべて、関数型変換の適用対象と考えることができます。  
  
 この方法は、一見して適用対象とは思われない数多くの問題に適用できます。 次に示す適用対象では、関数型変換を LINQ と組み合わせて、または切り離して使用することを検討する必要があります。  
  
-   XML ベースのドキュメント。 XML 言語の整形式データは、関数型変換を通じて容易に操作できます。 詳細については、「[XML の関数型変換 (C#)](../../../../csharp/programming-guide/concepts/linq/functional-transformation-of-xml.md)」を参照してください。  
  
-   その他の構造化されたファイル形式。 Windows.ini ファイルからプレーンテキストのドキュメントに至るほとんどのファイルは、分析や変換に適した構造を備えています。  
  
-   データ ストリーミング プロトコル。 通信プロトコルへのデータのエンコードおよび通信プロトコルからのデータのデコードは、単純な関数型変換で表せる場合がほとんどです。  
  
-   RDBMS データと OODBMS データ。 リレーショナル データベースおよびオブジェクト指向データベースは、構造化されたデータ ソースとして XML と同様に広く使用されています。  
  
-   数学的、統計的、および科学的なソリューション。 これらの分野では、視覚化、予測、重要な問題の解決などを支援する際に、大きなデータ セットが操作される傾向があります。  
  
 「[純粋関数へのリファクタリング (C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md)」で説明しているように、純粋関数の使用は関数型プログラミングの一例です。 純粋関数は、その直接的な利点に加えて、関数型変換の観点から問題について考える場合に役立ちます。 この方法は、プログラムおよびクラスの設計にも大きな影響を与えます。 上に示したように、問題がデータ変換ソリューションに関連している場合は、特に影響を受けます。  
  
 このチュートリアルでは扱いませんが、関数型変換の観点から影響を受ける設計は、アクターとしてオブジェクトよりもプロセスに重点を置く傾向があり、その結果であるソリューションは、個別のオブジェクト状態変更ではなく一連の大規模な変換として実装される傾向にあります。  
  
 繰り返しになりますが、C# は命令型の方法と関数型の方法の両方をサポートしているため、両方の要素を組み込むことがアプリケーションにとって最善の設計であることを覚えておいてください。  
  
## <a name="see-also"></a>関連項目  
 [純粋関数型変換の概要 (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [XML の関数型変換 (C#) ](../../../../csharp/programming-guide/concepts/linq/functional-transformation-of-xml.md)   
 [純粋関数へのリファクタリング (C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md)
