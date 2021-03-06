---
title: "#error (C# リファレンス) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#error"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#error ディレクティブ [C#]"
ms.assetid: f2a7f3af-4cf9-4111-b369-70204d24b26b
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# #error (C# リファレンス)
`#error` を使用すると、コードの特定の位置でエラーを表示できます。  次に例を示します。  
  
```  
#error Deprecated code in this method.  
```  
  
## 解説  
 `#error`は一般的に、条件付きディレクティブ内で使用します。  
  
 また、[\#warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-warning.md) でユーザー定義の警告を生成することもできます。  
  
## 使用例  
  
```  
// preprocessor_error.cs  
// CS1029 expected  
#define DEBUG  
class MainClass   
{  
    static void Main()   
    {  
#if DEBUG  
#error DEBUG is defined  
#endif  
    }  
}  
```  
  
## 参照  
 [C\# リファレンス](../../../csharp/language-reference/index.md)   
 [C\# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [C\# プリプロセッサ ディレクティブ](../../../csharp/language-reference/preprocessor-directives/index.md)