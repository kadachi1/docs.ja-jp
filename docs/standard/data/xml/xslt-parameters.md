---
title: "XSLT パラメーター | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: fe60aaa0-ae43-4b1c-9be1-426af66ba757
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XSLT パラメーター
XSLT パラメーターを <xref:System.Xml.Xsl.XsltArgumentList> に追加するには、<xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> メソッドを使用します。  その時点で、修飾名と名前空間 URI がそのパラメーター オブジェクトに関連付けられます。  
  
### XSLT パラメーターを使用するために必要な処理  
  
1.  <xref:System.Xml.Xsl.XsltArgumentList> オブジェクトを作成し、<xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> メソッドを使用してパラメーターを追加します。  
  
2.  スタイル シートからパラメーターを呼び出します。  
  
3.  <xref:System.Xml.Xsl.XsltArgumentList> オブジェクトを <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> メソッドに渡します。  
  
## パラメーターの型  
 このパラメーター オブジェクトは、W3C 型に対応している必要があります。  対応する W3C 型、これと同等の Microsoft .NET のクラス \(型\)、および W3C 型が XPath 型か XSLT 型であるかを次の表に示します。  
  
|W3C 型|対応する .NET クラス \(型\)|XPath 型または XSLT 型|  
|-----------|-------------------------|-----------------------|  
|`String`|<xref:System.String?displayProperty=fullName>|XPath|  
|`Boolean`|<xref:System.Boolean?displayProperty=fullName>|XPath|  
|`Number`|<xref:System.Double?displayProperty=fullName>|XPath|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XSLT|  
|`Node*`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XPath|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator><br /><br /> **XPathNavigator\[\]**|XPath|  
  
 \* これは単一のノードを含むノード セットに相当します。  
  
 パラメーター オブジェクトが上記のクラスのいずれでもない場合、次の規則に従って型が変換されます。  共通言語ランタイム \(CLR\) の数値型は、<xref:System.Double> に変換されます。  <xref:System.DateTime> 型は <xref:System.String> に変換されます。  <xref:System.Xml.XPath.IXPathNavigable> 型は <xref:System.Xml.XPath.XPathNavigator> に変換されます。  **XPathNavigator\[\]** は <xref:System.Xml.XPath.XPathNodeIterator> に変換されます。  
  
 その他の型はエラーになります。  
  
## 例  
 算出された割引日を保持するパラメーターを <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> メソッドを使用して作成する例を次に示します。  割引日は、発注日から 20 日後として算出されます。  
  
 [!code-csharp[XSLT_Param#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Param/CS/xsltparam.cs#1)]
 [!code-vb[XSLT_Param#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Param/VB/xsltparam.vb#1)]  
  
### 入力  
  
##### order.xml  
 [!code-xml[XSLT_Param#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/order.xml#2)]  
  
##### discount.xsl  
 [!code-xml[XSLT_Param#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/discount.xsl#3)]  
  
### 出力  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<order>  
  <total>36.9</total>  
     15% discount if paid by: 2/4/2004 12:00:00 AM  
</order>  
```  
  
## 参照  
 [XSLT 変換](../../../../docs/standard/data/xml/xslt-transformations.md)