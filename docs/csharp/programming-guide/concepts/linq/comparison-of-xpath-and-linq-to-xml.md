---
title: "XPath と LINQ to XML の比較 | Microsoft Docs"
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
ms.assetid: 87d361b1-daa9-4fd4-a53a-cbfa40111ad3
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d60000605a42faa22841cc7b76b878a77bc53b7f
ms.lasthandoff: 03/13/2017


---
# <a name="comparison-of-xpath-and-linq-to-xml"></a>XPath と LINQ to XML の比較
XPath と [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] の機能はある程度似ています。 どちらも XML ツリーに対してクエリを実行するために使用され、結果として、要素のコレクション、属性のコレクション、ノードのコレクション、要素や属性の値などを返します。 ただし、相違点もいくつかあります。  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a>XPath と LINQ to XML の違い  
 XPath では、新しい型を射影できません。 XPath では、ツリーからノードのコレクションが返されるだけですが、[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] では、クエリを実行し、オブジェクト グラフまたは XML ツリーを新しい構造に射影できます。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] クエリは、XPath 式と比べて、はるかに多機能かつ強力です。  
  
 XPath 式は、文字列内に独立して存在します。 C# コンパイラは、コンパイル時に XPath 式を解析できません。 一方 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] クエリは、C# コンパイラによって解析され、コンパイルされます。 コンパイラを使用することにより、多くのクエリ エラーを検出できます。  
  
 XPath の結果は厳密に型指定されません。 多くの場合、XPath 式を評価した結果はオブジェクトであり、開発者が適切な型を決定し、必要に応じて結果をキャストする必要があります。 一方、[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] クエリからの射影は厳密に型指定されます。  
  
## <a name="result-ordering"></a>結果の順序付け  
 XPath 1.0 勧告には、XPath 式の評価結果であるコレクションは順序付けされないことが記載されています。  
  
 ただし、[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] の XPath 軸メソッドから返されるコレクションを反復処理すると、コレクション内のノードがドキュメント順に返されます。 これは、ドキュメントの逆順として述語が表現されている `preceding` や `preceding-sibling` などの XPath 軸にアクセスする場合でも同様です。  
  
 一方、[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 軸のほとんどはコレクションをドキュメント順に返しますが、<xref:System.Xml.Linq.XNode.Ancestors%2A> と <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A> の 2 つは、コレクションをドキュメントの逆順に返します。 次の表では、軸を列挙し、それぞれのコレクションの順序を示します。  
  
|LINQ to XML 軸|並べ替え|  
|----------------------|--------------|  
|XContainer.DescendantNodes|ドキュメント順|  
|XContainer.Descendants|ドキュメント順|  
|XContainer.Elements|ドキュメント順|  
|XContainer.Nodes|ドキュメント順|  
|XContainer.NodesAfterSelf|ドキュメント順|  
|XContainer.NodesBeforeSelf|ドキュメント順|  
|XElement.AncestorsAndSelf|ドキュメントの逆順|  
|XElement.Attributes|ドキュメント順|  
|XElement.DescendantNodesAndSelf|ドキュメント順|  
|XElement.DescendantsAndSelf|ドキュメント順|  
|XNode.Ancestors|ドキュメントの逆順|  
|XNode.ElementsAfterSelf|ドキュメント順|  
|XNode.ElementsBeforeSelf|ドキュメント順|  
|XNode.NodesAfterSelf|ドキュメント順|  
|XNode.NodesBeforeSelf|ドキュメント順|  
  
## <a name="positional-predicates"></a>位置述語  
 XPath 式では、多くの軸で位置述語がドキュメント順として表現されますが、逆方向軸つまり `preceding`、`preceding-sibling`、`ancestor`、および `ancestor-or-self` の場合は、ドキュメントの逆順で表現されます。 たとえば、XPath 式 `preceding-sibling::*[1]` は、直前の兄弟を返します。 これは、最終的な結果セットがドキュメント順で表される場合も同様です。  
  
 一方、LINQ to XML の位置述語は、常に軸の順序として表現されます。 たとえば、`anElement.ElementsBeforeSelf().ToList()[0]` は、直前の兄弟ではなく、クエリされる要素の親の最初の子要素を返します。 別の例として、`anElement.Ancestors().ToList()[0]` は親要素を返します。  
  
 上記の方法では、コレクション全体が具体化されます。 これは、このクエリを記述する方法としては、最も効率的な方法とはいえません。 このように記述されているのは、位置述語の動作を明らかにするためです。 同じクエリをより適切に記述するには、<xref:System.Linq.Enumerable.First%2A> メソッドを、`anElement.ElementsBeforeSelf().First()` のように使用します。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] で直前の要素を検索する場合は、次の式を記述します。  
  
 `ElementsBeforeSelf().Last()`  
  
## <a name="performance-differences"></a>パフォーマンスの違い  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] の XPath 機能を使用する XPath クエリのパフォーマンスは、[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] クエリよりも低くなります。  
  
## <a name="comparison-of-composition"></a>構成の比較  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] クエリの構成は、XPath 式の構成に似ている部分がありますが、構文はかなり異なります。  
  
 たとえば、`customers` という変数に要素があり、`CompanyName` というすべての子要素の下で `Customer` という孫要素を検索する場合は、次のように XPath 式を記述します。  
  
```csharp  
customers.XPathSelectElements("./Customer/CompanyName");  
```  
  
 これと同等の [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] クエリは次のとおりです。  
  
```csharp  
customers.Element("Customer").Elements("CompanyName");  
```  
  
 同様の対応関係が XPath 軸ごとに存在します。  
  
|XPath 軸|LINQ to XML 軸|  
|----------------|----------------------|  
|child (既定の軸)|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>|  
|Parent (..)|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName>|  
|attribute 軸 (@)|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName><br /><br /> または<br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName>|  
|ancestor 軸|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName>|  
|ancestor-or-self 軸|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName>|  
|descendant 軸 (//)|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName><br /><br /> または<br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName>|  
|descendant-or-self|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName><br /><br /> または<br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName>|  
|following-sibling|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName><br /><br /> または<br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName>|  
|preceding-sibling|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName><br /><br /> または<br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName>|  
|following|同等の軸はありません。|  
|preceding|同等の軸はありません。|  
  
## <a name="see-also"></a>関連項目  
 [XPath ユーザー向けの LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
