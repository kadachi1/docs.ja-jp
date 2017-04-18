---
title: "F# 言語リファレンス"
description: "F# 言語リファレンス"
keywords: "visual f#, f#, 関数型プログラミング"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: b1707be1-7b7c-4fdd-a717-d9c190bc5fb5
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: e0b7058513b0487902b2a57b889e77df1abfef98
ms.lasthandoff: 04/05/2017

---

# <a name="f-language-reference"></a>F# 言語リファレンス

このセクションでは、.NET プラットフォーム向けのマルチパラダイム プログラミング言語である F# 言語のリファレンスを示します。 F# 言語は、関数型プログラミング、オブジェクト指向プログラミング、および命令型プログラミングのモデルをサポートします。


## <a name="f-tokens"></a>F# トークン
次の表に、F# でトークンとして使用されるキーワード、シンボル、およびリテラルを表にまとめたリファレンス トピックを示します。



|タイトル|説明|
|-----|-----------|
|[キーワード リファレンス](keyword-reference.md)|F# 言語のすべてのキーワードに関する情報へのリンクを示します。|
|[シンボルと演算子のリファレンス](symbol-and-operator-reference/index.md)|F# 言語で使用するシンボルと演算子の表を示します。|
|[リテラル](literals.md)|F# のリテラル値の構文と、F# のリテラルの型情報を指定する方法を示します。|

## <a name="f-language-concepts"></a>F# 言語の概念
次の表に、言語の概念について説明したリファレンス トピックを示します。



|タイトル|説明|
|-----|-----------|
|[関数](functions/index.md)|関数は、あらゆるプログラミング言語においてプログラムの実行の基本となる単位です。 他の言語の場合と同様に、F# の関数にもそれぞれ名前と本体があり、パラメーターや引数を受け取ることができます。 F# ではさらに、関数型プログラミング構成要素もサポートしています。たとえば、関数を値として処理したり、名前のない関数を式で使用したりできます。また、関数の合成による新しい関数の作成、カリー化関数、関数の引数の部分適用による関数の暗黙の定義などがサポートされます。|
|[F# の型](fsharp-types.md)|F# で使用される型と、それらを指定および記述する方法について説明します。|
|[型推論](type-inference.md)|F# コンパイラが値、変数、パラメーター、および戻り値の型を推論する方法について説明します。|
|[自動ジェネリック化](generics/automatic-generalization.md)|F# のジェネリックな構成要素について説明します。|
|[継承](inheritance.md)|継承について説明します。継承は、オブジェクト指向プログラミングで "is-a" 関係 (サブタイプ) をモデル化するために使用されます。|
|[メンバー](members/index.md)|F# オブジェクト型のメンバーについて説明します。|
|[パラメーターと引数](Parameters-and-Arguments.md)|パラメーターを定義して、関数、メソッド、およびプロパティに引数を渡すのための言語サポートについて説明します。 参照渡しの方法についても説明します。|
|[演算子のオーバーロード](operator-overloading.md)|クラス型またはレコード型の算術演算子をオーバーロードする方法と、グローバル レベルで算術演算子をオーバーロードする方法について説明します。|
|[キャストと変換](casting-and-conversions.md)|F# の型変換のサポートについて説明します。|
|[アクセス制御](access-control.md)|F# のアクセス制御について説明します。 アクセス制御とは、特定のプログラム要素 (型、メソッド、関数など) を使用できるクライアントを宣言することを意味します。|
|[パターン一致](pattern-matching.md)|パターンについて説明します。パターンは、F# 言語全体で使用される入力データの変換規則です。データをパターンと比較して抽出したり、データを構成要素に分解したり、さまざまな方法でデータから情報を抽出したりするために使用されます。|
|[アクティブ パターン](active-patterns.md)|アクティブ パターンについて説明します。 アクティブ パターンでは、入力データを分割する名前付きパーティションを定義できます。 アクティブ パターンを使用すると、パーティションごとにカスタマイズした方法でデータを分解できます。|
|[アサーション](assertions.md)|`assert` 式について説明します。これは、式のテストに使用できるデバッグ機能です。 デバッグ モードでエラーが発生すると、アサーションによってシステム エラーのダイアログ ボックスが生成されます。|
|[例外処理](exception-handling/index.md)|F# 言語での例外処理のサポートについて説明します。|
|[属性](attributes.md)|属性について説明します。属性により、プログラミング構造にメタデータを適用できます。|
|[リソースの管理: `use` キーワード](resource-management-the-use-keyword.md)|`use` キーワードと `using` キーワードについて説明します。これらを使用して、リソースの初期化と解放を制御できます。|
|[名前空間](namespaces.md)|F# における名前空間のサポートについて説明します。 名前空間を使用すると、プログラム要素のグループに名前を割り当てて、関連する機能の区分にコードを編成することができます。|
|[モジュール](modules.md)|モジュールについて説明します。 F# のモジュールは、F# プログラムにおける値、型、関数値などの F# コードのグループです。 モジュールのコードをグループ化すると、関連するコードをまとめることができ、プログラム内で名前の競合を回避するのに役立ちます|
|[インポート宣言: `open` キーワード](import-declarations-the-open-keyword.md)|`open` の動作について説明します。 インポート宣言は、完全修飾名を使用せずに参照できる要素が含まれるモジュールまたは名前空間を指定します。|
|[シグネチャ](signatures.md)|シグネチャとシグネチャ ファイルについて説明します。 シグネチャ ファイルには、型、名前空間、モジュールなど F# プログラムの一連の要素のパブリック シグネチャに関する情報が含まれています。 これらのプログラム要素のアクセシビリティを指定するために使用できます。|
|[XML に関するドキュメント](xml-documentation.md)|XML ドキュメント コメント (トリプル スラッシュ コメントとも呼ばれます) のドキュメント ファイルを生成するためのサポートについて説明します。 他の .NET 言語と同様に、F# のコード コメントからドキュメントを生成できます。|
|[冗語構文](verbose-syntax.md)|軽量構文が有効になっていない場合の F# の構成要素の構文について説明します。 冗語構文は、コード ファイルの先頭にある `#light "off"` ディレクティブで示されています。|

## <a name="f-types"></a>F# の型
次の表に、F# 言語でサポートされる型について説明したリファレンス トピックを示します。



|タイトル|説明|
|-----|-----------|
|[値](values/index.md)|値について説明します。値は、特定の型を持つ変更不可の数量です。値は、整数または浮動小数点数、文字またはテキスト、リスト、シーケンス、配列、タプル、判別共用体、レコード、クラス型、関数値のいずれかです。|
|[プリミティブ型](primitive-types.md)|F# 言語で使用される基本的なプリミティブ型について説明します。 また、対応する .NET 型と各型の最小値と最大値も示します。|
|[Unit 型](unit-type.md)|`unit` 型について説明します。これは、特定の値を持たないことを示す型です。`unit` 型には値が 1 つだけあり、他の値が存在しない場合や不要な場合のプレースホルダーとして機能します。|
|[文字列](strings.md)|F# の文字列について説明します。 `string` 型は、Unicode 文字のシーケンスとしての、変更不可のテキストを表します。 `string` は、.NET Framework の `System.String` のエイリアスです。|
|[タプル](tuples.md)|タプルについて説明します。タプルは、名前のない値の順序を指定したグループです。各値の型は異なる場合もあります。|
|[F# コレクション型](fsharp-collection-types.md)|配列、リスト、シーケンス (seq)、マップ、およびセットの型を含む、F# 機能のコレクション型の概要を示します。|
|[リスト](lists.md)|リストについて説明します。 F# のリストは、順序が指定されており変更できない一連のすべて同じ型の要素です。|
|[オプション](options.md)|オプション型について説明します。 F# のオプションは、値が存在する場合にも存在しない場合にも使用されます。 オプションには基になる型があり、その型の値を保持する場合と値がない場合があります。|
|[シーケンス](sequences.md)|シーケンスについて説明します。 シーケンスは、すべてが 1 つの型である論理的な一連の要素です。 シーケンスの個々の要素は必要な場合にのみ計算されるため、リテラル要素が示す数よりも少ない要素で表現されることがあります。|
|[配列](arrays.md)|配列について説明します。 配列は、0 から始まる一連のデータ要素の、固定サイズの変更可能なシーケンスで、その型はすべて同じです。|
|[レコード](records.md)|レコードについて説明します。 レコードは、名前付きの値の単純な集合を表しており、オプションでメンバーを含みます。|
|[判別共用体](discriminated-unions.md)|判別共用体について説明します。これは、さまざまな名前付きケースのうちのいずれかである可能性がある値をサポートします。値や型はそれぞれ異なる場合もあります。|
|[列挙型](enumerations.md)|列挙型について説明します。列挙型は、定義された一連の名前付きの値を持つ型です。 リテラルの代わりに使用すると、コードの読み取りおよび保守が容易になります。|
|[参照セル](reference-cells.md)|参照セルについて説明します。参照セルは、参照セマンティクスを持つ変更可能な値を作成できる格納場所です。|
|[型略称](type-abbreviations.md)|型略称について説明します。型略称は、型の代替名です。|
|[クラス](classes.md)|クラスについて説明します。クラスは、プロパティ、メソッド、およびイベントを持つことができるオブジェクトを表す型です。|
|[構造体](structures.md)|構造体について説明します。構造体はコンパクトなオブジェクト型であり、データが少量で動作が単純な型のクラスよりも効率が良い場合があります。|
|[インターフェイス](interfaces.md)|インターフェイスについて説明します。インターフェイスでは、他のクラスが実装する関連メンバーのセットを指定します。|
|[抽象クラス](abstract-classes.md)|抽象クラスについて説明します。抽象クラスは、一部またはすべてのメンバーを実装しないようにして、派生クラスから実装できるようにするためのクラスです。|
|[型拡張](type-extensions.md)|型拡張について説明します。型拡張を使用すると、定義済みのオブジェクト型に新しいメンバーを追加できます。|
|[フレキシブル型](flexible-types.md)|フレキシブル型について説明します。 フレキシブル型の注釈は、パラメーター、変数、または値の型が、指定された型と互換性があることを示します。互換性は、クラスまたはインターフェイスのオブジェクト指向の階層における位置によって決まります。|
|[デリゲート](delegates.md)|デリゲートについて説明します。デリゲートとは、オブジェクトとしての関数呼び出しを表します。|
|[測定単位](units-of-measure.md)|測定単位について説明します。 F# の浮動小数点値には測定単位を関連付けることができます。測定単位は一般に、長さ、体積、質量などを示すために使用されます。|
|[型プロバイダー](../tutorials/type-providers/index.md)|型プロバイダーについて説明します。組み込みの型プロバイダーを使用してデータベースや Web サービスにアクセスする方法に関するチュートリアルへのリンクを提供します。|

## <a name="f-expressions"></a>F# の式
次の表に、F# の式を説明するトピックの一覧を示します。

|タイトル|説明|
|-----|-----------|
|[条件式: `if...then...else`](conditional-expressions-if-then-else.md)|`if...then...else` 式について説明します。これは、コードのさまざまな分岐を実行する機能であり、指定されたブール式に応じて異なる値に評価されます。|
|[match 式](match-expressions.md)|`match` 式について説明します。この式により、式を一連のパターンと比較し、その比較に基づいて分岐を制御できます。|
|[ループ: `for...to` 式](loops-for-to-expression.md)|`for...to` 式について説明します。この式は、ループでループ変数の値の範囲を繰り返し処理するために使用します。|
|[ループ: `for...in` 式](loops-for-in-expression.md)|`for...in` 式について説明します。これは、列挙可能なコレクション (範囲表現、シーケンス、リスト、配列、または列挙型をサポートするその他の構成要素) のパターンと一致するかどうかの照合を反復処理するために使用されるループ構造です。|
|[ループ: `while...do` 式](loops-while-do-expression.md)|`while...do` 式について説明します。これは、指定したテスト条件が true の間に反復実行 (ループ) を行う場合に使用します。|
|[オブジェクト式](object-expressions.md)|オブジェクト式について説明します。これは、既存の基本型、インターフェイス、または一連のインターフェイスに基づいて、動的に作成される匿名のオブジェクト型の新しいインスタンスを作成する式です。|
|[遅延計算](lazy-computations.md)|遅延計算について説明します。遅延計算は、すぐには評価されず、結果が実際に必要なときに評価される計算です。|
|[コンピュテーション式](computation-expressions.md)|F# のコンピュテーション式について説明します。F# のコンピュテーション式には、制御フローの構成要素とバインドを使用してシーケンス化および結合できる計算を記述するための便利な構文が用意されています。 これらの計算式を使用すると、*モナド*の便利な構文が提供されます。モナドとは、関数型プログラムのデータ、制御、および副作用の管理に使用できる関数型プログラミングの機能です。 非同期ワークフローはコンピュテーション式の一種であり、非同期の並列計算をサポートします。 詳細については、「[非同期ワークフロー](asynchronous-workflows.md)」を参照してください。|
|[非同期ワークフロー](asynchronous-workflows.md)|非同期ワークフローについて説明します。非同期ワークフローは、同期コードを通常記述するのと非常に近い方法で非同期コードを記述できる言語機能です。|
|[コード クォート](code-quotations.md)|コード クォートについて説明します。この言語機能を使用すると、F# のコード式をプログラムで生成して使用できます。|
|[クエリ式](query-expressions.md)|クエリ式について説明します。これは、F# 用の LINQ を実装し、データ ソースや列挙可能なコレクションに対するクエリを記述できるようにする言語機能です。|

## <a name="compiler-supported-constructs"></a>コンパイラでサポートされる構成要素
次の表に、特殊なコンパイラでサポートされる構成要素を説明するトピックの一覧を示します。

|トピック|説明|
|-----|-----------|
|[コンパイラ オプション](compiler-options.md)|F# コンパイラのコマンド ライン オプションについて説明します。|
|[コンパイラ ディレクティブ](compiler-directives.md)|プロセッサ ディレクティブとコンパイラ ディレクティブについて説明します。|
|[ソース行、ファイル、およびパスの識別子](source-line-file-path-identifiers.md)|`__LINE__`、`__SOURCE_DIRECTORY__`、`__SOURCE_FILE__` の識別子について説明します。これは、コード内のソース行番号、ディレクトリおよびファイル名にアクセスするできるようにする組み込みの値です。|

## <a name="see-also"></a>関連項目
[Visual F#](../index.md)