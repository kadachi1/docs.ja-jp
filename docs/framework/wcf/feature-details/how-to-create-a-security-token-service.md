---
title: "方法 : セキュリティ トークン サービスを作成する | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "フェデレーション"
  - "WCF, フェデレーション"
ms.assetid: 98e82101-4cff-4bb8-a220-f7abed3556e5
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# 方法 : セキュリティ トークン サービスを作成する
セキュリティ トークン サービスは、WS\-Trust 仕様に定義されているプロトコルを実装します。このプロトコルでは、セキュリティ トークンの発行、更新、キャンセル、および検証を行うためのメッセージ形式とメッセージ交換パターンが定義されています。セキュリティ トークン サービスでは、これらの機能が 1 つ以上提供されます。ここでは、最も一般的なシナリオであるトークンの発行の実装について説明します。  
  
## トークンの発行  
 WS\-Trust は、トークンを発行するための `RequestSecurityToken` XML スキーマ定義言語 \(XSD: XML Schema Definition Language\) スキーマ要素および `RequestSecurityTokenResponse` XSD スキーマ要素に基づいたメッセージ形式を定義しています。また、関連するアクション URI \(Uniform Resource Identifier\) も定義しています。`RequestSecurityToken` メッセージに関連付けられているアクション URI は http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/RST\/Issue です。`RequestSecurityTokenResponse` メッセージに関連付けられているアクション URI は http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/RSTR\/Issue です。  
  
### 要求メッセージの構造  
 発行要求メッセージの構造は、通常、次の項目で構成されます。  
  
-   "要求の種類" URI。値は http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/Issue です。  
  
-   "トークンの種類" URI。SAML \(Security Assertions Markup Language\) 1.1 トークンの場合、この URI の値は http:\/\/docs.oasis\-open.org\/wss\/oasis\-wss\-saml\-token\-profile\-1.1\#SAMLV1.1 です。  
  
-   発行済みトークンに関連付けられるキーのビット数を示すキー サイズの値。  
  
-   "キーの種類" URI。対称キーの場合、この URI の値は http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/SymmetricKey です。  
  
 また、以下のような項目が含まれている必要があります。  
  
-   クライアントによって提供されたキー マテリアル。  
  
-   発行済みトークンが使用されるターゲット サービスを示すスコープ情報。  
  
 セキュリティ トークン サービスは、発行応答メッセージを作成する際に、発行要求メッセージの情報を使用します。  
  
## 応答メッセージの構造  
 発行応答メッセージの構造は、通常、次の項目で構成されます。  
  
-   発行済みセキュリティ トークン \(例 : SAML 1.1 アサーション\)。  
  
-   セキュリティ トークンに関連付けられた証明トークン。対称キーでは、多くの場合、これは暗号化されたキー マテリアルです。  
  
-   発行済みセキュリティ トークンへの参照。通常、セキュリティ トークン サービスが返す参照は、2 とおりに使用できます。1 つは、クライアントによって送信された後続のメッセージ内に、発行済みトークンが存在する場合で、もう 1 つは、後続のメッセージ内にトークンが存在しない場合です。  
  
 さらに、2 つの項目が含まれている必要があります。  
  
-   セキュリティ トークン サービスによって提供されたキー マテリアル。  
  
-   共有キーを計算するために必要なアルゴリズム。  
  
-   発行済みトークンの有効期間情報。  
  
## 要求メッセージの処理  
 セキュリティ トークン サービスは、要求メッセージのさまざまな部分を検査し、要求を満たすトークンを発行できることを確認することによって発行要求を処理します。セキュリティ トークン サービスは、発行するトークンを作成する前に次のことを確認する必要があります。  
  
-   要求が、実際に発行されるトークンに対する要求であること。  
  
-   要求されたトークンの種類をセキュリティ トークン サービスがサポートしていること。  
  
-   要求を行う権限が要求者にあること。  
  
-   キー マテリアルに関する要求者の期待にセキュリティ トークン サービスが応えられること。  
  
 トークンを作成する際には、トークンの署名に使用されるキーと共有キーの暗号化に使用されるキーの 2 つを決定することが重要です。トークンに署名が必要なのは、クライアントがターゲット サービスにトークンを提示する際に、そのサービスが、そのトークンを発行したのが信頼されるセキュリティ トークン サービスであると判定できるようにするためです。キー マテリアルは、ターゲット サービスが復号化できる方法で暗号化される必要があります。  
  
 SAML アサーションに署名する処理では、<xref:System.IdentityModel.Tokens.SigningCredentials> インスタンスを作成します。このクラスのコンストラクターは、次のものを受け取ります  
  
-   SAML アサーションに署名するために使用する <xref:System.IdentityModel.Tokens.SecurityKey>。  
  
-   使用する署名アルゴリズムを識別する文字列。  
  
-   使用するダイジェスト アルゴリズムを識別する文字列。  
  
-   アサーションの署名に使用されるキーを識別する <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> \(必要な場合\)。  
  
 [!code-csharp[c_CreateSTS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#1)]
 [!code-vb[c_CreateSTS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#1)]  
  
 共有キーを暗号化する処理では、キー マテリアルを受け取り、それをターゲット サービスが共有キーの復号化に使用できるキーで暗号化します。通常は、ターゲット サービスの公開キーが使用されます。  
  
 [!code-csharp[c_CreateSTS#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#2)]
 [!code-vb[c_CreateSTS#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#2)]  
  
 さらに、暗号化されたキーの <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> も必要です。  
  
 [!code-csharp[c_CreateSTS#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#3)]
 [!code-vb[c_CreateSTS#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#3)]  
  
 最後に、この <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> を使用して、`SamlSubject` を `SamlToken` の一部として作成します。  
  
 [!code-csharp[c_CreateSTS#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#4)]
 [!code-vb[c_CreateSTS#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#4)]  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [フェデレーション サンプル](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
## 応答メッセージの作成  
 セキュリティ トークン サービスによって発行要求が処理され、発行されるトークンと証明キーが作成されたら、少なくとも、要求されたトークン、証明トークン、および発行されたトークンの参照を含む応答メッセージを作成する必要があります。発行済みトークンは、通常、<xref:System.IdentityModel.Tokens.SamlAssertion> から作成された <xref:System.IdentityModel.Tokens.SamlSecurityToken> です。次の例を参照してください。  
  
 [!code-csharp[c_CreateSTS#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#5)]
 [!code-vb[c_CreateSTS#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#5)]  
  
 セキュリティ トークン サービスによって共有キー マテリアルが提供される場合は、<xref:System.ServiceModel.Security.Tokens.BinarySecretSecurityToken> を作成することにより、証明トークンが作成されます。  
  
 [!code-csharp[c_CreateSTS#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#6)]
 [!code-vb[c_CreateSTS#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#6)]  
  
 クライアントとセキュリティ トークン サービスの両方によって共有キーのキー マテリアルが提供される場合の証明トークンの作成方法[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、「[フェデレーション サンプル](../../../../docs/framework/wcf/samples/federation-sample.md)」を参照してください。  
  
 発行済みトークンの参照を作成するには、<xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause> クラスのインスタンスを作成します。  
  
 [!code-csharp[c_CreateSTS#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#7)]
 [!code-vb[c_CreateSTS#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#7)]  
  
 最後に、これらの値を、クライアントに返される応答メッセージにシリアル化します。  
  
## 例  
 セキュリティ トークン サービスの完全なコードについては、「[フェデレーション サンプル](../../../../docs/framework/wcf/samples/federation-sample.md)」を参照してください。  
  
## 参照  
 <xref:System.IdentityModel.Tokens.SigningCredentials>   
 <xref:System.IdentityModel.Tokens.SecurityKey>   
 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier>   
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>   
 <xref:System.IdentityModel.Tokens.SamlAssertion>   
 <xref:System.ServiceModel.Security.Tokens.BinarySecretSecurityToken>   
 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause>   
 [フェデレーション サンプル](../../../../docs/framework/wcf/samples/federation-sample.md)