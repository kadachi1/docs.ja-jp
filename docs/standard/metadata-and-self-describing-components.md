---
title: "メタデータと自己言及的なコンポーネント | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "共通言語ランタイム, メタデータ"
  - "コンポーネント [.NET Framework], メタデータ"
  - "言語, 相互運用性"
  - "メタデータ, メタデータの概要"
  - "PE ファイル, メタデータ"
  - "移植可能な実行可能 (PE) ファイル, メタデータ"
  - "ランタイム, メタデータ"
  - "自己言及的なファイル"
ms.assetid: 3dd13c5d-a508-455b-8dce-0a852882a5a7
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# メタデータと自己言及的なコンポーネント
以前は、ある 1 つの言語で記述されたソフトウェア コンポーネント \(.exe または .dll\) で、別の言語で記述されたコンポーネントを使用するのは簡単ではありませんでした。  COM により、この問題が解決するための手段が提供されるようになりました。  .NET Framework では、コンパイラからすべてのモジュールやアセンブリに追加の宣言情報を挿入できるようになり、コンポーネントの相互運用性が大幅に強化されています。  メタデータと呼ばれるこの情報により、コンポーネント間のシームレスな相互作用がサポートされます。  
  
 メタデータはプログラムを説明するバイナリ情報であり、共通言語ランタイムのポータブル実行可能 \(PE\) ファイルまたはメモリのいずれかに格納されます。  コードを PE ファイルとしてコンパイルすると、PE ファイルの特定の部分にメタデータが挿入され、コードは Microsoft Intermediate Language \(MSIL\) に変換されて PE ファイル内の別の部分に挿入されます。  モジュール内またはアセンブリ内で定義され、参照されているすべての型およびメンバーは、メタデータ内部に記述されます。  コードを実行すると、ランタイムはメタデータをメモリに読み込み、コードのクラス、メンバー、継承などの情報を検索するためにメタデータを参照します。  
  
 メタデータには、コードに定義されているすべての型およびメンバーが言語に中立的な形で記述されています。  メタデータには、次の情報が格納されいてます。  
  
-   アセンブリに関する記述  
  
    -   ID \(名前、バージョン、カルチャ、公開キー\)  
  
    -   エクスポートされる型  
  
    -   そのアセンブリが依存している他のアセンブリ  
  
    -   実行のために必要なセキュリティ アクセス許可  
  
-   型に関する説明  
  
    -   名前、参照可能範囲、基底クラス、および実装されているインターフェイス  
  
    -   メンバー \(メソッド、フィールド、プロパティ、イベント、入れ子になった型\)  
  
-   属性。  
  
    -   型やメンバーを修飾する追加の記述要素  
  
## メタデータの利点  
 メタデータは、プログラミング モデルを簡素化するうえで重要な役割を果たします。これにより、インターフェイス定義言語 \(IDL: Interface Definition Language\) ファイル、ヘッダー ファイル、およびその他のコンポーネント参照の外部メソッドは一切不要になります。  メタデータを使用すると、.NET Framework の各言語は、開発者やユーザーからは見えない、言語に依存しない形式で自動的に記述されるようになります。  また、属性を使用することにより、メタデータを拡張することもできます。  メタデータの主な利点は、次のとおりです。  
  
-   自己言及的なファイル  
  
     共通言語ランタイム モジュールおよびアセンブリは、自己言及的なファイルです。  モジュールのメタデータには、他のモジュールと相互作用するのに必要なすべての情報が含まれています。  メタデータは自動的に COM の IDL の機能を提供するため、ユーザーは 1 つのファイルを定義と実装の両方に使用できます。  また、ランタイム モジュールやアセンブリをオペレーティング システムに登録する必要もありません。  これにより、ランタイムが使用する記述は常にコンパイル済みファイル内の実際のコードに反映されるため、アプリケーションの信頼性が高くなります。  
  
-   言語の相互運用性と簡単なコンポーネント ベースのデザイン  
  
     メタデータは、他の言語で記述されている PE ファイルからクラスを継承するのに必要な、コンパイル済みコードについてのすべての情報を提供します。  明示的なマーシャリングや相互運用可能なカスタム コードの使用を考慮せずに、マネージ言語 \(共通言語ランタイムに変換される言語\) で記述された任意のクラスのインスタンスを作成できます。  
  
-   属性。  
  
     .NET Framework を使用すると、コンパイル済みファイル内で "属性" と呼ばれる特定の種類のメタデータを宣言できます。  属性は、.NET Framework 全体で使用され、実行時のプログラムの動作を詳細に制御します。  また、ユーザー定義のカスタム属性によって、独自に作成したメタデータを .NET Framework のファイルに挿入できます。  詳細については、「[属性](../../docs/standard/attributes/index.md)」を参照してください。  
  
## メタデータと PE ファイルの構造  
 メタデータと Microsoft Intermediate Language \(MSIL\) は、それぞれ、.NET Framework のポータブル実行可能 \(PE\) ファイルの別のセクションに格納されます。  ファイルのメタデータ部分には、一連のテーブルとヒープ データの構造が格納されています。  MSIL 部分には、PE ファイルのメタデータ部分を参照する MSIL とメタデータ トークンが格納されています。  コードの MSIL を表示する [MSIL 逆アセンブラー \(Ildasm.exe\)](../../docs/framework/tools/ildasm-exe-il-disassembler.md) のようなツールを使用すると、メタデータ トークンが表示される場合があります。  
  
### メタデータのテーブルおよびヒープ  
 各メタデータ テーブルには、プログラムの要素に関する情報が保持されています。  たとえば、1 つのメタデータ テーブルにはコード内のクラスが記述されており、別のテーブルにはフィールドが記述されています。  コードに 10 個のクラスが存在する場合、クラス テーブルには、各クラスごとに 1 行、つまり 10 行が存在します。  メタデータ テーブルは、他のテーブルおよびヒープを参照します。  たとえば、クラスのメタデータ テーブルは、メソッドのテーブルを参照します。  
  
 また、メタデータは、4 つのヒープ構造 \(文字列、BLOB、ユーザー文字列、および GUID\) に情報を格納します。  型やメンバーに名前を付けるために使用する文字列はすべて、文字列ヒープに格納されています。  たとえば、特定のメソッドの名前はメソッド テーブルに直接は格納されず、メソッド テーブルから文字列ヒープ内に格納されているメソッドの名前を参照します。  
  
### メタデータ トークン  
 各メタデータ テーブルのそれぞれの行は、メタデータ トークンによって、PE ファイルの MSIL 部分内で一意に識別されます。  メタデータ トークンは、概念上、ポインターに類似しており、特定のメタデータ テーブルを参照します。  
  
 メタデータ トークンは、4 バイトで構成される数値です。  最上位バイトは、特定のトークンの参照先であるメタデータ テーブル \(メソッド、型など\) を表します。  残り 3 バイトは、記述されているプログラミング要素と対応する、メタデータ テーブル内の行を指定します。  たとえば、C\# 言語でメソッドを定義し、そのメソッドを PE ファイルとしてコンパイルすると、PE ファイルの MSIL 部分に次のようなメタデータ トークンが格納されます。  
  
```  
0x06000004  
```  
  
 最上位バイト \(`0x06`\) は、**MethodDef** トークンであることを示します。  下位 3 バイト \(`000004`\) は、**MethodDef** テーブル内の、このメソッドの定義を記述する情報に対応する 4 行目を参照するように、共通言語ランタイムに指示します。  
  
### PE ファイル内のメタデータ  
 プログラムを共通言語ランタイムとしてコンパイルすると、プログラムは 3 つの部分で構成される PE ファイルに変換されます。  各部分の内容を説明する表を次に示します。  
  
|PE セクション|PE セクションの内容|  
|--------------|-----------------|  
|PE ヘッダー|PE ファイルの主要なセクションのインデックスとエントリ ポイントのアドレス。<br /><br /> ランタイムはこの情報に基づいてファイルを PE ファイルとして識別し、実行開始位置と、メモリにプログラムをいつ読み込むかを判断します。|  
|MSIL の命令|コードを構成する Microsoft Intermediate Language \(MSIL\) の命令。  ほとんどの MSIL 命令には、メタデータ トークンが付いています。|  
|メタデータ|メタデータ テーブルおよびヒープ。  ランタイムはこのセクションを使用してコード内のすべての型およびメンバーに関する情報を記録します。  また、このセクションには、カスタム属性やセキュリティ情報も格納されています。|  
  
## 実行時のメタデータの使用  
 メタデータと、共通言語ランタイムでのメタデータの役割をより深く理解するために、簡単なプログラムを作成し、メタデータがその有効期間中にどのように機能するかを示します。  `MyApp` と呼ばれるクラス内の 2 つのメソッドを表すコードの例を次に示します。  `Main` メソッドは、プログラムのエントリ ポイントです。`Add` メソッドは、2 つの整数引数の合計値を返します。  
  
```vb  
Public Class MyApp  
   Public Shared Sub Main()  
      Dim ValueOne As Integer = 10  
      Dim ValueTwo As Integer = 20  
      Console.WriteLine("The Value is: {0}", Add(ValueOne, ValueTwo))  
   End Sub  
  
   Public Shared Function Add(One As Integer, Two As Integer) As Integer  
      Return (One + Two)  
   End Function  
End Class  
```  
  
```csharp  
using System;    
public class MyApp  
{  
   public static int Main()  
   {  
      int ValueOne = 10;  
      int ValueTwo = 20;           
      Console.WriteLine("The Value is: {0}", Add(ValueOne, ValueTwo));  
      return 0;  
   }  
   public static int Add(int One, int Two)  
   {  
      return (One + Two);  
   }  
}  
```  
  
 このコードを実行すると、ランタイムがモジュールをメモリに読み込み、このクラスのメタデータを調べます。  モジュールを読み込んだ後、ランタイムはメソッドの Microsoft Intermediate Language \(MSIL\) ストリームを詳細に分析して、そのストリームを高速のネイティブ機械語命令に変換します。  ランタイムはジャスト イン タイム \(JIT\) コンパイラを使用して、それぞれのメソッドを必要なときに 1 つずつ、MSIL 命令からネイティブ マシン語コードに変換します。  
  
 上記のコードの `Main` 関数によって生成された MSIL の一部の例を次に示します。  MSIL とメタデータは、[MSIL 逆アセンブラー \(Ildasm.exe\)](../../docs/framework/tools/ildasm-exe-il-disassembler.md) を使用することにより、任意の .NET Framework アプリケーションから表示できます。  
  
```  
.entrypoint  
.maxstack  3  
.locals ([0] int32 ValueOne,  
         [1] int32 ValueTwo,  
         [2] int32 V_2,  
         [3] int32 V_3)  
IL_0000:  ldc.i4.s   10  
IL_0002:  stloc.0  
IL_0003:  ldc.i4.s   20  
IL_0005:  stloc.1  
IL_0006:  ldstr      "The Value is: {0}"  
IL_000b:  ldloc.0  
IL_000c:  ldloc.1  
IL_000d:  call int32 ConsoleApplication.MyApp::Add(int32,int32) /* 06000003 */  
```  
  
 JIT コンパイラはこのメソッド全体の MSIL を読み取って詳細に分析し、このメソッドの効率的なネイティブ命令を生成します。  `IL_000d`で、`Add` メソッドのメタデータ トークン \(`/*` `06000003 */`\) が検出されます。ランタイムは、このトークンを使用して **MethodDef** テーブルの 3 行目を調べます。  
  
 **メソッドが記述されているメタデータ トークンによって参照される、`Add`MethodDef** テーブルの一部の例を次の表に示します。  このアセンブリにはほかにもメタデータ テーブルが存在し、それぞれ独自の値を持っていますが、ここでは、このテーブルだけを参照します。  
  
|行|Relative Virtual Address \(RVA\)|ImplFlags|フラグ|名前<br /><br /> \(文字列ヒープを指す\)|Signature \(BLOB ヒープを指す\)|  
|-------|--------------------------------------|---------------|---------|--------------------------|-------------------------------|  
|1|0x00002050|IL<br /><br /> マネージ|パブリック<br /><br /> ReuseSlot<br /><br /> SpecialName<br /><br /> RTSpecialName<br /><br /> .ctor|.ctor \(コンストラクター\)||  
|2|0x00002058|IL<br /><br /> マネージ|パブリック<br /><br /> スタティック<br /><br /> ReuseSlot|Main|文字列|  
|3|0x0000208c|IL<br /><br /> マネージ|パブリック<br /><br /> スタティック<br /><br /> ReuseSlot|追加|int, int, int|  
  
 このテーブルの各列には、コードについての重要な情報が格納されています。  ランタイムは **RVA**列を使用して、このメソッドを定義する MSIL の開始メモリ アドレスを計算します。  **ImplFlags** および **Flags** 列には、このメソッドを記述するビットマスク \(たとえば、メソッドがパブリックかプライベートかを記述するビットマスク\) が格納されています。  **Name** 列は、文字列ヒープからメソッドの名前へのインデックスとなります。  **Signature** 列は、BLOB ヒープ内のメソッドのシグネチャ定義へのインデックスとなります。  
  
 ランタイムは 3 行目の **RVA** 列から必要なオフセット アドレスを計算し、計算したオフセット アドレスを JIT コンパイラに返します。JIT コンパイラは計算された新しいアドレスに移動します。  JIT コンパイラは、新しいアドレスから、別のメタデータ トークンを検出するまで MSIL の処理を続行し、処理を繰り返します。  
  
 ランタイムは、メタデータを使用することにより、コードを読み込み、ネイティブ機械語命令に変換するのに必要なすべての情報にアクセスできます。  このように、メタデータによって自己言及的なファイルが使用可能になり、メタデータと共通型システムを組み合わせて使用することで、言語間で継承が可能になります。  
  
## 関連トピック  
  
|タイトル|説明|  
|----------|--------|  
|[属性](../../docs/standard/attributes/index.md)|属性の適用方法、カスタム属性の記述方法、および属性に格納されている情報の取得方法を説明します。|