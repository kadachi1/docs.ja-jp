---
title: "コレクションに関するガイドライン | Microsoft Docs"
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
ms.assetid: 297b8f1d-b11f-4dc6-960a-8e990817304e
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# コレクションに関するガイドライン
任意の型が共通の特性を持つオブジェクトのグループを操作する際に、コレクションを見なすことができます。 実装するには、このような型に適したはほぼ必ず <xref:System.Collections.IEnumerable> または <xref:System.Collections.Generic.IEnumerable%601>, 、ここでおのみ考慮されるようにコレクションには、これらのインターフェイスの一方または両方を実装する型。  
  
 **X のしないで** のパブリック Api で弱く型指定されたコレクションを使用します。  
  
 すべての戻り値およびコレクションのアイテムを表すパラメーターの型は、\(これは、コレクションのパブリック メンバーにのみ適用されます\) の基本型の正確な項目の種類にする必要があります。  
  
 **X のしないで** を使用して <xref:System.Collections.ArrayList> または <xref:System.Collections.Generic.List%601> パブリック Api のです。  
  
 これらの型は、パブリック Api ではなく、内部の実装で使用するためのデータ構造です。`List<T>` パフォーマンスと電力消費の Api と柔軟性 cleanness を犠牲に最適です。 たとえば、返された場合 `List<T>`, はこれまでできませんクライアント コードは、コレクションを変更する場合は、通知を受信することです。 また、 `List<T>` など多くのメンバーの公開 <xref:System.Collections.Generic.List%601.BinarySearch%2A>, が役に立たないか多くのシナリオに該当します。 次の 2 つのセクションでは、パブリック Api の使用専用に設計された型 \(抽象化\) について説明します。  
  
 **X のしないで** を使用して `Hashtable` または `Dictionary<TKey,TValue>` パブリック Api のです。  
  
 これらの型は、内部の実装で使用するためのデータ構造です。 パブリック Api を使用する必要があります <xref:System.Collections.IDictionary>, 、`IDictionary <TKey, TValue>`, 、またはいずれかまたは両方のインターフェイスを実装するカスタム型です。  
  
 **X のしないで** を使用して <xref:System.Collections.Generic.IEnumerator%601>, 、<xref:System.Collections.IEnumerator>, 、またはその他の型以外の戻り値の型として実装して、これらのインターフェイスのいずれかを `GetEnumerator` メソッドです。  
  
 型以外の場合、メソッドから列挙子を返す `GetEnumerator` では使用できません、 `foreach` ステートメントです。  
  
 **X のしないで** 両方を実装する `IEnumerator<T>` と `IEnumerable<T>` 同じ型にします。 非ジェネリック インターフェイスにも当てはまります `IEnumerator` と `IEnumerable`です。  
  
## コレクションのパラメーター  
 **✓ は** 型の専門性の最も可能性のあるパラメーターの種類として使用します。 ほとんどのメンバーをコレクションのパラメーターを使用すること、 `IEnumerable<T>` インターフェイスです。  
  
 **X 回避** を使用して <xref:System.Collections.Generic.ICollection%601> または <xref:System.Collections.ICollection> にアクセスするだけのパラメーターとして、 `Count` プロパティです。  
  
 代わりに、 `IEnumerable<T>` または `IEnumerable` して動的にオブジェクトが実装されているかどうかを確認する `ICollection<T>` または `ICollection`です。  
  
## コレクションのプロパティと戻り値  
 **X のしないで** 設定可能なコレクション プロパティを提供します。  
  
 ユーザーは、まずコレクションを消去して、新しい内容を追加し、コレクションの内容を置き換えることができます。 コレクション全体を置き換える一般的なシナリオがある場合は、提供することを検討してください、 `AddRange` コレクション メソッド。  
  
 **✓ は** を使用して `Collection<T>` またはそのサブクラスの `Collection<T>` プロパティまたは戻り値を表す読み取り\/書き込みのコレクション。  
  
 場合 `Collection<T>` いくつかの要件を満たしていません \(など、コレクションは実装する必要があります <xref:System.Collections.IList>\) を実装することによってカスタム コレクションを使用して `IEnumerable<T>`, 、`ICollection<T>`, 、または <xref:System.Collections.Generic.IList%601>です。  
  
 **✓ は** を使用して <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>, のサブクラス `ReadOnlyCollection<T>`, 、まれなケースで、または `IEnumerable<T>` プロパティまたは戻り値を表す読み取り専用コレクション。  
  
 一般に、使用 `ReadOnlyCollection<T>`します。 いくつかの要件を満たしていない場合 \(など、コレクションは実装する必要があります `IList`\) を実装することによってカスタム コレクションを使用して `IEnumerable<T>`, 、`ICollection<T>`, 、または `IList<T>`です。 カスタムの読み取り専用コレクションを実装する場合は、実装 `ICollection<T>.ReadOnly` false を返します。  
  
 あるか、唯一のシナリオをサポートすることが順方向専用のイテレーションであることを確認する場合、単に使用できます `IEnumerable<T>`します。  
  
 **✓ を検討してください** コレクションを直接使用する代わりにジェネリックの基本コレクションのサブクラスを使用します。  
  
 これにより、優れた名前し基本コレクション型ではないヘルパー メンバーを追加するためです。 これは、特に高水準の Api に該当します。  
  
 **✓ を検討してください** のサブクラスを返す `Collection<T>` または `ReadOnlyCollection<T>` から非常に一般的に使用されるメソッドとプロパティ。  
  
 これによりするヘルパー メソッドを追加またはコレクションの実装を将来を変更することが可能です。  
  
 **✓ を検討してください** コレクションに格納された項目が一意キーを持つ場合は、キー付きのコレクションを使用する \(名前、Id などです。\)。 キー付きコレクションは、整数値とキーの両方でインデックスを作成できるとを継承して実装は通常コレクション `KeyedCollection<TKey,TItem>`します。  
  
 通常、キー付きのコレクションは、メモリ フット プリントが大きくし、メモリのオーバーヘッドが、キーの利点を上回る場合使用しないでです。  
  
 **X のしないで** プロパティのコレクションまたはコレクションを返すメソッドから null 値を返します。 代わりに、空のコレクションまたは空の配列を返します。  
  
 一般的な規則は、null および空の \(項目が 0\) コレクション、配列があることと同じ扱われます。  
  
### スナップショットとライブのコレクション  
 時刻である時点の状態を表すコレクションは、スナップショットのコレクションと呼ばれます。 たとえば、データベース クエリから返された行を含むコレクションには、スナップショットがあります。 常に現在の状態を表すコレクションは、ライブのコレクションと呼ばれます。 たとえば、一連の `ComboBox` 項目は、ライブのコレクション。  
  
 **X のしないで** プロパティからのスナップショットのコレクションを返します。 プロパティは、ライブのコレクションを返す必要があります。  
  
 プロパティの getter が非常に軽量な操作をする必要があります。 スナップショットを返すには、o \(n\) 操作の内部コレクションのコピーを作成する必要があります。  
  
 **✓ は** スナップショット コレクションまたはライブのいずれかを使用して `IEnumerable<T>` \(またはそのサブタイプ\) は揮発性のコレクションを表すため \(つまり、変更可能なコレクションを明示的に変更することがなく\)。  
  
 一般に、共有リソース \(ディレクトリ内のファイルなど\) を表すすべてのコレクションは、揮発性です。 このようなコレクションは、非常に困難か不可能実装は、単に前方参照専用の列挙子にしない限り、ライブのコレクションとして実装するにです。  
  
## 配列またはコレクションの選択  
 **✓ は** コレクションを配列よりも優先されます。  
  
 コレクションは、内容を制御するため、時間の経過と共に進化させることができますおよびがより使いやすくします。 さらに、読み取り専用のシナリオの配列の使用はお勧めできません、配列の複製のコストが非常に大きいためです。 使いやすさの調査によると、一部の開発者と感じるユーザー コレクション ベースの Api を使用します。  
  
 ただし、低レベルの Api を開発する場合、読み取り\/書き込みシナリオの配列を使用する方がよい場合があります。 配列である、メモリの使用量、ワーキング セットを軽減して、ランタイムが最適化されるため、配列内の要素へのアクセスが高速化します。  
  
 **✓ を検討してください** 低レベルの Api で配列を使用する、メモリ消費量を最小限に抑え、パフォーマンスを最大化します。  
  
 **✓ は** バイトのコレクションではなくバイト配列を使用します。  
  
 **X のしないで** プロパティをプロパティの getter を呼び出すたびに新しい配列 \(内部配列のコピーなど\) を返す必要がある場合は、プロパティの配列を使用します。  
  
## カスタム コレクションを実装します。  
 **✓ を検討してください** から継承する `Collection<T>`, 、`ReadOnlyCollection<T>`, 、または `KeyedCollection<TKey,TItem>` 新しいコレクションを設計するとき。  
  
 **✓ は** 実装 `IEnumerable<T>` 新しいコレクションを設計するとき。 実装を検討 `ICollection<T>` も `IList<T>` 理にかなっています。  
  
 このようなカスタム コレクションを実装するには場合、によって確立された API パターンに従う `Collection<T>` と `ReadOnlyCollection<T>` 限り近くにします。 つまり、同じメンバーを明示的に実装する、これら 2 つのコレクションの名前となどのように、パラメーターの名前します。  
  
 **✓ を検討してください** 非ジェネリック コレクション インターフェイスを実装する \(`IList` と `ICollection`\) 場合は、コレクションは多くの場合する Api に渡される入力としてこれらのインターフェイスを取得します。  
  
 **X 回避** 型に、コレクションの概念に関係のない複雑な Api でコレクション インターフェイスを実装します。  
  
 **X のしないで** などの非ジェネリックの基本コレクションから継承 `CollectionBase`します。 使用 `Collection<T>`, 、`ReadOnlyCollection<T>`, 、および `KeyedCollection<TKey,TItem>` 代わりにします。  
  
### カスタム コレクションの名前を付ける  
 コレクション \(型を実装する `IEnumerable`\) 主に 2 つの理由が作成されます: 既存のデータ構造とは異なるパフォーマンス特性の構造に固有の操作と多くの場合は、新しいデータ構造を作成するには \(1\) \(など  <xref:System.Collections.Generic.List%601>, 、<xref:System.Collections.Generic.LinkedList%601>, 、<xref:System.Collections.Generic.Stack%601>\)、および特定の項目のセットを保持するための特殊なコレクションを作成するには \(2\) \(など  <xref:System.Collections.Specialized.StringCollection>\)。 データ構造は、アプリケーションやライブラリの内部の実装で最もよく使用されます。 専用コレクションは、\(プロパティおよびパラメーターの型\) としての Api で公開するには、主にします。  
  
 **✓ は** を実装する抽象化の名前に「辞書」サフィックスを使用して `IDictionary` または `IDictionary<TKey,TValue>`です。  
  
 **✓ は** を実装する型の名前に「コレクション」サフィックスを使用 `IEnumerable` \(またはその子孫のいずれかの\) 項目のリストを表すとします。  
  
 **✓ は** カスタム データ構造に適切なデータ構造の名前を使用します。  
  
 **X 回避** コレクションの抽象化の名前に"LinkedList"または「ハッシュ」などの特定の実装を暗に示してのサフィックスを使用します。  
  
 **✓ を検討してください** コレクションが付いている項目の種類の名前を付けることです。 たとえば、型の項目を格納するコレクション `Address` \(実装 `IEnumerable<Address>`\) はという名前で `AddressCollection`します。 プレフィックス"I"項目の種類が、インターフェイスの場合は、項目の種類を省略できます。 したがって、一連の <xref:System.IDisposable> 項目を呼び出すことができる `DisposableCollection`です。  
  
 **✓ を検討してください** 、対応する書き込み可能なコレクションを追加する場合や、フレームワークに既に存在する場合に、読み取り専用のコレクション名に"ReadOnly"プレフィックスを使用します。  
  
 たとえば、文字列の読み取り専用コレクションを呼び出す必要があります `ReadOnlyStringCollection`します。  
  
 *部分 © 2005年、2009 Microsoft Corporation します。 All rights reserved.*  
  
 *翔泳社からのアクセス許可によって検出 [Framework デザイン ガイドライン: 規則が、表現方法と再利用可能な .NET ライブラリを 2 nd Edition パターン](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) は Cwalina Brad エイブラムスによる、Microsoft Windows の開発シリーズの一部として Addison\-wesley Professional、2008 年 10 月 22 日を公開します。*  
  
## 参照  
 [Framework デザイン ガイドライン](../../../docs/standard/design-guidelines/index.md)   
 [使用方法のガイドライン](../../../docs/standard/design-guidelines/usage-guidelines.md)