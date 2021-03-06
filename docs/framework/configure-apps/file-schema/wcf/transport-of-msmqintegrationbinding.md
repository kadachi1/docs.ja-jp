---
title: "&lt;msmqIntegrationBinding&gt; の &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 054579e3-7fdd-47df-99ca-952706ba5c8e
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# &lt;msmqIntegrationBinding&gt; の &lt;transport&gt;
メッセージ キュー統合トランスポートのセキュリティ設定を定義します。  
  
## 構文  
  
```  
  
<security>  
    <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
        msmqEncryptionAlgorithm="RC4Stream/AES"  
        msmqProtectionLevel="None/Sign/EncryptAndSign"  
        msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
</security>  
```  
  
## 属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### 属性  
  
|属性|説明|  
|--------|--------|  
|`msmqAuthenticationMode`|MSMQ トランスポートによるメッセージの認証方法を指定します。  これが `None` に設定されている場合、`msmqProtectionLevel` 属性の値も `None` に設定する必要があります。<br /><br /> 以下の値が有効です。<br /><br /> -   None: 認証は行われません。<br />-   WindowsDomain: 認証機構により Active Directory が使用され、メッセージに関連付けられた SID の X.509 証明書が取得されます。  次に、これを使用してキューの ACL がチェックされ、ユーザーがキューに書き込む権限を持っていることが確認されます。<br />-   Certificate: チャネルは、証明書ストアから証明書を取得します。<br /><br /> 既定値は WindowsDomain です。  この属性は <xref:System.ServiceModel.MsmqAuthenticationMode> 型です。|  
|`msmqEncryptionAlgorithm`|メッセージ キュー マネージャー間でメッセージを転送するときに、ネットワーク上でメッセージの暗号化に使用されるアルゴリズムを指定します。  以下の値が有効です。<br /><br /> -   RC4Stream<br />-   AES<br /><br /> 既定値は RC4Stream です。  この属性は <xref:System.ServiceModel.MsmqEncryptionAlgorithm> 型です。|  
|`msmqProtectionLevel`|MSMQ トランスポートのレベルでメッセージをセキュリティで保護する方法を指定します。  暗号化を行うとメッセージの整合性が確保されますが、EncryptAndSign を使用するとメッセージの整合性と否認防止の両方が確保されます。つまり、メッセージは本当にその送信者から送信されていることになり、記載されている送信者が実際の送信者になります。<br /><br /> -   以下の値が有効です。<br />-   None: 保護されません。<br />-   Sign: メッセージは署名されます。<br />-   EncryptAndSign: メッセージは暗号化および署名されます。<br /><br /> 既定値は Sign です。  この属性は、ProtectionLevel 型です。|  
|`msmqSecureHashAlgorithm`|-   署名の一部としてダイジェストの計算に使用されるアルゴリズムを指定します。  以下の値が有効です。<br />-   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> 既定値は SHA1 です。  この属性は <xref:System.ServiceModel.MsmqSecureHashAlgorithm> 型です。|  
  
### 子要素  
 なし  
  
### 親要素  
  
|要素|説明|  
|--------|--------|  
|[\<security\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)|MSMQ バインディングのセキュリティ設定を定義します。|  
  
## 解説  
 この要素は、メッセージ キュー統合トランスポートのセキュリティ設定をカプセル化します。  設定は、メッセージ キュー統合トランスポートとキューに置かれているトランスポートの両方で同じです。  この設定を使用すると、認証モード、暗号化アルゴリズム、セキュア ハッシュ アルゴリズム、および保護レベルを設定できます。  
  
## 参照  
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.MsmqTransportSecurity>   
 [サービスおよびクライアントのセキュリティ保護](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [サービスおよびクライアントのセキュリティ保護](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [バインディング](../../../../../docs/framework/wcf/bindings.md)   
 [システムが提供するバインディングの構成](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ja-jp/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<binding\>](../../../../../docs/framework/misc/binding.md)