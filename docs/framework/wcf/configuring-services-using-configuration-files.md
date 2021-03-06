---
title: "構成ファイルを使用してサービスを構成する方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "サービスの構成 [WCF]"
ms.assetid: c9c8cd32-2c9d-4541-ad0d-16dff6bd2a00
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# 構成ファイルを使用してサービスを構成する方法
構成ファイルを使用して [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] サービスを構成すると、デザイン時ではなく配置時にエンドポイントとサービス動作のデータを指定できるという柔軟性が生まれます。 ここでは使用可能な主要な技術について説明します。  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスは、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] の構成技術を使用して構成できます。 通常、XML 要素は、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスをホストするインターネット インフォメーション サービス \(IIS\) サイトの Web.config ファイルに追加されます。 この要素によって、コンピューターごとにエンドポイント アドレス \(サービスと通信するために使用する実際のアドレス\) などの詳細情報を変更できます。 また、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] には、システム指定の要素がいくつか用意されており、これらの要素によって、サービスの最も基本的な機能を簡単に選択できます。[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] 以降では、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] には、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 構成要件を簡略化する新しい既定の構成モデルが付属しています。 特定のサービスに対し [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 構成を指定しないと、ランタイムは自動的にいくつかの標準エンドポイントおよびバインディング\/動作でサービスを構成します。 実際、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] アプリケーションのプログラミングにおいては、構成ファイルの記述が作業の大きな部分を占めます。  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [サービスのバインディングの構成](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)。 最もよく使用される要素の[!INCLUDE[crlist](../../../includes/crlist-md.md)]については、「[システム標準のバインディング](../../../docs/framework/wcf/system-provided-bindings.md)」を参照してください。 既定のエンドポイント、バインディング、および動作の[!INCLUDE[crabout](../../../includes/crabout-md.md)]については、「[簡略化された構成](../../../docs/framework/wcf/simplified-configuration.md)」および「[WCF サービスの簡略化された構成](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)」を参照してください。  
  
> [!IMPORTANT]
>  2 つの異なるバージョンのサービスが配置される side\-by\-side のシナリオを配置する場合、構成ファイルで参照されるアセンブリの部分名を指定する必要があります。 これは構成ファイルがすべてのバージョンのサービスで共有されて、異なるバージョンの .NET Framework で実行される可能性があるためです。  
  
## System.Configuration: Web.config と App.config  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] では、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] の System.Configuration 構成システムを使用します。  
  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] でサービスを構成するとき、Web.config ファイルまたは App.config ファイルのいずれかを使用して、設定を指定します。 選択する構成ファイル名は、サービスに選択したホスト環境によって異なります。 サービスのホストに IIS を使用している場合は、Web.config ファイルを使用します。 他のホスト環境を使用している場合、App.config ファイルを使用します。  
  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] では、App.config という名前のファイルを使用して、最終の構成ファイルを作成します。 構成で実際に使用される最終的な名前は、アセンブリ名によって異なります。 たとえば、アセンブリ名が "Cohowinery.exe" の場合、最終の構成ファイルの名前は "Cohowinery.exe.config" になります。 ただし、変更する必要があるのは App.config ファイルだけです。 このファイルで行った変更は、コンパイル時に自動的に最終のアプリケーション構成ファイルに反映されます。  
  
 App.config ファイルを使用しているとき、アプリケーションが開始され、構成が適用されると、構成システムは App.config ファイルを Machine.config ファイルの内容とマージします。 このしくみによって、Machine.config ファイルにはコンピューター全体の設定を定義できます。 App.config ファイルは、Machine.config ファイルの設定をオーバーライドするために使用できます。また、Machine.config ファイルにある設定をロックしてこの設定が使用されるようにすることもできます。 Web.config の場合、構成システムは、アプリケーション ディレクトリまでのすべてのディレクトリにある Web.config ファイルを、適用される構成にマージします。 構成と設定の優先順位[!INCLUDE[crabout](../../../includes/crabout-md.md)]、<xref:System.Configuration> 名前空間のトピックを参照してください。  
  
## 構成ファイルの主要セクション  
 構成ファイルの主要セクションには、次の要素があります。  
  
```  
<system.ServiceModel>  
  
   <services>  
   <!—- Define the service endpoints. This section is optional in the new  
    default configuration model in .NET Framework 4. -->  
      <service>  
         <endpoint/>  
      </service>  
   </services>  
  
   <bindings>  
   <!-- Specify one or more of the system-provided binding elements,  
    for example, <basicHttpBinding> -->   
   <!-- Alternatively, <customBinding> elements. -->  
      <binding>  
      <!-- For example, a <BasicHttpBinding> element. -->  
      </binding>  
   </bindings>  
  
   <behaviors>  
   <!-- One or more of the system-provided or custom behavior elements. -->  
      <behavior>  
      <!-- For example, a <throttling> element. -->  
      </behavior>  
   </behaviors>  
  
</system.ServiceModel>  
```  
  
> [!NOTE]
>  バインディングと動作のセクションは省略可能であり、必要な場合のみ追加されます。  
  
### \<services\> 要素  
 `services` 要素には、アプリケーションによってホストされるすべてのサービスの仕様が入ります。[!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] の簡略化された構成モデル以降の場合、このセクションは省略可能です。  
  
 [\<services\>](../../../docs/framework/configure-apps/file-schema/wcf/services.md)  
  
### \<service\> 要素  
 各サービスには次の属性があります。  
  
-   `name`。 \- サービス コントラクトの実装を提供する型を指定します。 これは、名前空間、期間、および型名を構成する完全修飾名です。 たとえば、`"MyNameSpace.myServiceType"` などです。  
  
-   `behaviorConfiguration`。 \- `behavior` 要素に存在するいずれかの `behaviors` 要素の名前を指定します。 指定された動作は、サービスが偽装を許可するかどうかなどのアクションを制御します。 その値が空の名前であるか、または `behaviorConfiguration` が指定されていない場合、サービスの動作の既定のセットがサービスに追加されます。  
  
-   [\<service\>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)  
  
### \<endpoint\> 要素  
 各エンドポイントには、次の属性で表されるアドレス、バインディング、およびコントラクトが必要です。  
  
-   `address`。 サービスの URI \(Uniform Resource Identifier\) を指定します。絶対アドレスまたはサービスのベース アドレスからの相対アドレスを指定できます。 空の文字列を設定した場合、サービスの <xref:System.ServiceModel.ServiceHost> を作成するときに指定したベース アドレスでエンドポイントを使用できることを示します。  
  
-   `binding`。 \- 通常、<xref:System.ServiceModel.WsHttpBinding> などのシステム指定のバインディングを指定しますが、ユーザー定義バインディングを指定することも可能です。 指定するバインディングによって、トランスポートの種類、使用するセキュリティとエンコーディング、および信頼できるセッション、トランザクション、またはストリーミングがサポートされるかどうか、または有効かどうかが決まります。  
  
-   `bindingConfiguration`。 バインディングの既定値を変更する必要がある場合、`binding` 要素の該当する `bindings` 要素を構成することによって変更できます。 この属性には、既定値の変更に使用される `name` 要素の`binding` 属性と同じ値を指定する必要があります。 名前を指定しない場合、またはバインディングに `bindingConfiguration` を指定しない場合、バインディングの種類の既定のバインディングは、エンドポイントで使用されます。  
  
-   `contract`。 コントラクトを定義するインターフェイスを指定します。 これは `name` 要素の `service` 属性で指定された共通言語ランタイム \(CLR\) 型で実装されたインターフェイスです。  
  
-   [\<endpoint\> element reference](http://msdn.microsoft.com/ja-jp/13aa23b7-2f08-4add-8dbf-a99f8127c017)  
  
### \<bindings\> 要素  
 `bindings` 要素には、任意のサービスで定義される任意のエンドポイントによって使用できるすべてのバインディングに関する仕様が入ります。  
  
 [\<bindings\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)  
  
### \<binding\> 要素  
 `bindings` 要素に含まれる `binding` 要素には、システム指定のバインディング \(「[システム標準のバインディング](../../../docs/framework/wcf/system-provided-bindings.md)」を参照\) またはカスタム バインディング \(「[カスタム バインディング](../../../docs/framework/wcf/extending/custom-bindings.md)」を参照\) のどちらかを指定できます。`binding` 要素には、バインディングを `name` 要素の `bindingConfiguration` 属性で指定されたエンドポイントと関連付ける `endpoint` 属性があります。 名前を指定しない場合、バインディングは、バインディングの既定の種類に対応します。  
  
 サービスとクライアントの構成の[!INCLUDE[crabout](../../../includes/crabout-md.md)]については、「[Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/ja-jp/13cb368e-88d4-4c61-8eed-2af0361c6d7a)」を参照してください。  
  
 [\<binding\>](../../../docs/framework/misc/binding.md)  
  
### \<behaviors\> 要素  
 これは、サービスの動作を定義する `behavior` 要素のコンテナー要素です。  
  
 [\<behaviors\>](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
  
### \<behavior\> 要素  
 各 `behavior` 要素は、`name` 属性によって識別され、\<`throttling`\> などのシステム指定の動作またはカスタム動作のいずれかを定義します。 名前を指定しない場合、動作要素は、既定のサービスまたはエンドポイント動作に対応します。  
  
 [\<behavior\>](../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)  
  
## バインディングと動作の構成を使用する方法  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] では、構成で参照システムを使用することによって、エンドポイント間で構成を簡単に共有できます。 構成値を直接エンドポイントに割り当てるのではなく、バインディング関連の構成値を `bindingConfiguration` セクションの `<binding>` 要素にグループ化します。 バインディング構成とは、バインディングの設定の名前付きグループです。 エンドポイントは、名前によって `bindingConfiguration` を参照できます。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
 <system.serviceModel>  
  <bindings>  
    <basicHttpBinding>  
     <binding name="myBindingConfiguration1" closeTimeout="00:01:00" />  
     <binding name="myBindingConfiguration2" closeTimeout="00:02:00" />  
     <binding closeTimeout="00:03:00" />  <!—- Default binding for basicHttpBinding -->  
    </basicHttpBinding>  
     </bindings>  
     <services>  
      <service name="MyNamespace.myServiceType">  
       <endpoint   
          address="myAddress" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration1"  
          contract="MyContract"  />  
       <endpoint   
          address="myAddress2" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration2"  
          contract="MyContract" />  
       <endpoint   
          address="myAddress3" binding="basicHttpBinding"   
          contract="MyContract" />  
       </service>  
      </services>  
    </system.serviceModel>  
</configuration>  
```  
  
 `name` の `bindingConfiguration` は、`<binding>` 要素で設定します。`name` には、バインディングの種類 \(この場合は [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)\) のスコープ内で一意の文字列、または既定のバインディングを参照する空の値を指定する必要があります。 エンドポイントは、`bindingConfiguration` 属性をこの文字列に設定することによって構成にリンクします。  
  
 `behaviorConfiguration` は、次のサンプルに示すように、同じ方法で実装されます。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myBehavior">  
           <callbackDebug includeExceptionDetailInFaults="true" />  
         </behavior>  
      </endpointBehaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="true" />  
        </behavior>  
      </serviceBehaviors>  
  
    </behaviors>  
    <services>  
     <service name="NewServiceType">  
       <endpoint   
          address="myAddress3" behaviorConfiguration="myBehavior"  
          binding="basicHttpBinding"  
          contract=”MyContract” />  
      </service>  
    </services>  
   </system.serviceModel>  
</configuration>  
```  
  
 サービスの動作の既定のセットは、サービスに追加されることに注意してください。 このシステムでは、設定を再定義することなく、エンドポイント間で共通の構成を共有できます。 コンピューター全体のスコープが必要な場合は、バインディングまたは動作の構成を Machine.config に作成します。 構成設定は、すべての App.config ファイルで操作できます。[構成エディター ツール \(SvcConfigEditor.exe\)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) を使用すると、構成を簡単に作成できます。  
  
## 動作のマージ  
 動作のマージ機能を使用すると、共通動作のセットを常に使用する場合に動作の管理が容易になります。 この機能では、さまざまなレベルの構成階層で動作を指定し、サービスが複数レベルの構成階層から動作を継承することができます。 このしくみを説明するため、IIS に次の仮想ディレクトリ レイアウトが存在するとします。  
  
 ~\\Web.config~\\Service.svc~\\Child\\Web.config~\\Child\\Service.svc  
  
 また ~\\Web.config ファイルに次の内容が含まれているとします。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceDebug includeExceptionDetailInFaults="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 さらに ~\\Child\\Web.config にある子 Web.config に次の内容が含まれているとします。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 ~\\Child\\Service.svc にあるサービスは、serviceDebug 動作と serviceMetadata 動作の両方を持つ場合と同様に動作します。 ~\\Service.svc にあるサービスは、serviceDebug 動作のみを持ちます。 これによって、同じ名前の 2 つの動作コレクション \(この例では空の文字列\) がマージされます。  
  
 また、\<clear\> タグを使用して動作コレクションを消去したり、\<remove\> タグを使用してコレクションから個々の動作を削除することができます。 たとえば、次の 2 つの構成は serviceMetadata 動作のみを持つ子サービスになります。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <remove name="serviceDebug"/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <clear/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 動作のマージは、上に示した名前なし動作コレクションだけでなく、名前付き動作コレクションにも適用できます。  
  
 動作のマージは、IIS ホスト環境で機能し、Web.config ファイルがルートの Web.config ファイルおよび machine.config と階層的にマージされます。 ただし、動作のマージはアプリケーション環境でも機能し、machine.config を App.config ファイルとマージできます。  
  
 動作のマージは、構成内のエンドポイント動作とサービス動作の両方に適用されます。  
  
 親動作コレクションに既に存在する動作が子動作コレクションにも含まれている場合、子動作が親をオーバーライドします。 たとえば、親動作コレクションに `<serviceMetadata httpGetEnabled="False" />` があり、子動作コレクションに `<serviceMetadata httpGetEnabled="True" />` がある場合、動作コレクションで子動作が親動作をオーバーライドし、httpGetEnabled が "true" になります。  
  
## 参照  
 [簡略化された構成](../../../docs/framework/wcf/simplified-configuration.md)   
 [Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/ja-jp/13cb368e-88d4-4c61-8eed-2af0361c6d7a)   
 [\<service\>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)   
 [\<binding\>](../../../docs/framework/misc/binding.md)