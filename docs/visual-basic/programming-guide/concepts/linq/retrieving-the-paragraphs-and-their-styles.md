---
title: "段落とそのスタイル (Visual Basic) の取得 |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: d9ed2238-d38e-4ad4-b88b-db7859df9bde
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bb6d68296a720a796a319502c4cb2f0319727459
ms.lasthandoff: 03/13/2017


---
# <a name="retrieving-the-paragraphs-and-their-styles-visual-basic"></a>段落とそのスタイル (Visual Basic) の取得
この例では、WordprocessingML ドキュメントから段落ノードを取得するクエリを記述します。 それぞれの段落のスタイルも特定します。  
  
 このクエリの基に前の例では、クエリで[の既定の段落スタイル (Visual Basic) の検索](../../../../visual-basic/programming-guide/concepts/linq/finding-the-default-paragraph-style.md)スタイルの一覧から既定のスタイルを取得します。 スタイルが明示的に設定されていない段落のスタイルをクエリで特定するには、この情報が必要です。 段落のスタイルは、`w:pPr` 要素を通して設定されます。この要素が含まれていない段落は、既定のスタイルを使用して書式設定されます。  
  
 このトピックでは、クエリを構成するいくつかの要素の意味を説明し、完全な作業例の一部分であるクエリを紹介します。  
  
## <a name="example"></a>例  
 ドキュメント内のすべての段落とそのスタイルを取得するクエリのソースは、次のとおりです。  
  
```vb  
xDoc.Root.<w:body>...<w:p>  
```  
  
 この式は、前の例では、クエリのソースのような[(Visual Basic の場合) 既定の段落スタイルの検索](../../../../visual-basic/programming-guide/concepts/linq/finding-the-default-paragraph-style.md)します。 主な違いは、使用するという、<xref:System.Xml.Linq.XContainer.Descendants%2A>軸の代わりに、<xref:System.Xml.Linq.XContainer.Elements%2A>軸</xref:System.Xml.Linq.XContainer.Elements%2A></xref:System.Xml.Linq.XContainer.Descendants%2A>。 クエリを使用して、<xref:System.Xml.Linq.XContainer.Descendants%2A>軸段落が body 要素の直接の子はできませんので、ドキュメント内のセクションがある、; 代わりに、段落は&2; つのレベルがダウンしている階層内</xref:System.Xml.Linq.XContainer.Descendants%2A>。 使用して、<xref:System.Xml.Linq.XContainer.Descendants%2A>軸、ドキュメントでセクションを使用するかどうかのコードを実行します</xref:System.Xml.Linq.XContainer.Descendants%2A>。  
  
## <a name="example"></a>例  
 クエリで `Let` 句を使用して、スタイル ノードが含まれる要素を特定します。 要素がない場合は、`styleNode` が `Nothing` に設定されます。  
  
```vb  
Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault()  
```  
  
 `Let`最初句を使用して、<xref:System.Xml.Linq.XContainer.Elements%2A>というすべての要素を検索する軸`pPr`を使用して、<xref:System.Xml.Linq.Extensions.Elements%2A>という名前のすべての子要素を検索する拡張メソッド`pStyle`、最後に使用して、<xref:System.Linq.Enumerable.FirstOrDefault%2A>標準クエリ演算子のコレクションをシングルトンに変換する</xref:System.Linq.Enumerable.FirstOrDefault%2A></xref:System.Xml.Linq.Extensions.Elements%2A></xref:System.Xml.Linq.XContainer.Elements%2A>。 コレクションが空の場合は、`styleNode` が `Nothing` に設定されます。 これは、`pStyle` 子孫ノードを検索するのに便利な表現形式です。 `pPr` 子ノードが存在しない場合、コードが例外をスローして失敗することはなく、`styleNode` が `Nothing` に設定されます。これは、この `Let` 句で予期された動作です。  
  
 このクエリは、匿名型のコレクションを射影します。このコレクションには、`StyleName` および `ParagraphNode` の&2; つのメンバーがあります。  
  
## <a name="example"></a>例  
 この例では、WordprocessingML ドキュメントを処理して、WordprocessingML ドキュメントから段落ノードを取得します。 それぞれの段落のスタイルも特定します。 この例は、このチュートリアルのこれまでの例に基づいています。 新しいクエリについては、以下のコード内にあるコメントで説明が示されています。  
  
 この例ではのソース ドキュメントを作成するための手順を参照して[ソース Office Open XML ドキュメント (Visual Basic) を作成する](../../../../visual-basic/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md)です。  
  
 この例では、WindowsBase アセンブリに含まれるクラスを使用します。 内の型を使用して、<xref:System.IO.Packaging?displayProperty=fullName>名前空間</xref:System.IO.Packaging?displayProperty=fullName>。  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, ByVal defaultStyle As String) As String  
        If (styleNode Is Nothing) Then  
            Return defaultStyle  
        Else  
            Return styleNode.@w:val  
        End If  
    End Function  
  
    Sub Main()  
        Dim fileName = "SampleDoc.docx"  
  
        Dim documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Dim stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
        Dim wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (styleRelation IsNot Nothing) Then  
                    Dim styleUri As Uri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
                    '  Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
                End If  
            End If  
        End Using  
  
        Dim defaultStyle As String = _  
            ( _  
                From style In styleDoc.Root.<w:style> _  
                Where style.@w:type = "paragraph" And _  
                      style.@w:default = "1" _  
                Select style _  
            ).First().@w:styleId  
  
        ' Following is the new query that finds all paragraphs in the  
        ' document and their styles.  
        Dim paragraphs = _  
            From para In xDoc.Root.<w:body>...<w:p> _  
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault() _  
        Select New With { _  
            .ParagraphNode = para, _  
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _  
        }  
  
        For Each p In paragraphs  
            Console.WriteLine("StyleName:{0}", p.StyleName)  
        Next  
  
    End Sub  
End Module  
```  
  
 この例で、次の出力に示されるドキュメントに適用すると生成[ソース Office Open XML ドキュメント (Visual Basic) を作成する](../../../../visual-basic/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md)です。  
  
```  
StyleName:Heading1  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
```  
  
## <a name="next-steps"></a>次の手順  
 次のトピックで[(Visual Basic) の段落のテキストを取得して](../../../../visual-basic/programming-guide/concepts/linq/retrieving-the-text-of-the-paragraphs.md)段落のテキストを取得するクエリを作成します。  
  
## <a name="see-also"></a>関連項目  
 [チュートリアル: WordprocessingML ドキュメント (Visual Basic) 内のコンテンツの操作](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
