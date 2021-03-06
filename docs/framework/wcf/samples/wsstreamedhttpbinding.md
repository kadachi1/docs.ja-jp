---
title: "WSStreamedHttpBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97ce4d3d-ca6f-45fa-b33b-2429bb84e65b
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# WSStreamedHttpBinding
このサンプルでは、HTTP トランスポート使用時にストリーミングをサポートする目的でデザインされたバインディングを作成する方法を示します。  
  
> [!NOTE]
>  このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Binding\WSStreamedHttpBinding`  
  
 新しい標準バインディングを作成して構成する手順は、次のとおりです。  
  
1.  新しい標準バインディングを作成する  
  
     basicHttpBinding や netTcpBinding などの [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] の標準バインディングは、特定の要件に合わせて、基になるトランスポートとチャネル スタックを構成します。このサンプルでは、`WSStreamedHttpBinding` は、ストリーミングをサポートするようチャネル スタックを構成します。既定では、WS\-Security と信頼できるメッセージ機能はチャネル スタックに追加されません。どちらの機能もストリーミングではサポートされないためです。新しいバインディングは、<xref:System.ServiceModel.Channels.Binding> から派生するクラス `WSStreamedHttpBinding` に実装されます。`WSStreamedHttpBinding` には、<xref:System.ServiceModel.Channels.HttpTransportBindingElement>、<xref:System.ServiceModel.Channels.HttpsTransportBindingElement>、<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>、および <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> のバインディング要素が含まれます。このクラスは、作成されるバインディング スタックを構成する `CreateBindingElements()` メソッドを提供します。次のサンプル コードを参照してください。  
  
    ```  
    public override BindingElementCollection CreateBindingElements()  
    {  
         // return collection of BindingElements  
         BindingElementCollection bindingElements = new BindingElementCollection();  
  
        // the order of binding elements within the collection is important: layered channels are applied in the order included, followed by  
        // the message encoder, and finally the transport at the end  
        if (flowTransactions)  
        {  
            bindingElements.Add(transactionFlow);  
        }  
        bindingElements.Add(textEncoding);  
  
        // add transport (http or https)  
        bindingElements.Add(transport);  
        return bindingElements.Clone();  
    }  
  
    ```  
  
2.  構成サポートを追加する  
  
     構成を使用してトランスポートを公開するため、サンプルではさらに、`WSStreamedHttpBindingConfigurationElement` クラスと `WSStreamedHttpBindingSection` クラスという 2 つのクラスを実装します。クラス `WSStreamedHttpBindingSection` は <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602> で、`WSStreamedHttpBinding` を [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] の構成システムに公開します。実装の大部分は `WSStreamedHttpBindingConfigurationElement` で代行されます。これは <xref:System.ServiceModel.Configuration.StandardBindingElement> の派生です。クラス `WSStreamedHttpBindingConfigurationElement` には `WSStreamedHttpBinding` のプロパティに対応するプロパティがあり、各構成要素をバインディングにマップする関数があります。  
  
     次のセクションをサービスの構成ファイルに追加することにより、ハンドラを構成システムに登録します。  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <extensions>  
          <bindingExtensions>  
            <add name="wsStreamedHttpBinding" type="Microsoft.ServiceModel.Samples.WSStreamedHttpBindingCollectionElement, WSStreamedHttpBinding, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null" />  
          </bindingExtensions>  
        </extensions>  
      </system.serviceModel>  
    </configuration>  
  
    ```  
  
     ハンドラーは serviceModel 構成セクションから参照できます。  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint  
                    address="https://localhost/servicemodelsamples/service.svc"  
                    bindingConfiguration="Binding"  
                    binding="wsStreamedHttpBinding"  
                    contract="Microsoft.ServiceModel.Samples.IStreamedEchoService"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
### サンプルを設定、ビルド、および実行するには  
  
1.  次のコマンドを使用して、[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 をインストールします。  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  「[Windows Communication Foundation サンプルの 1 回限りのセットアップの手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)」の手順が実行済みであることを確認します。  
  
3.  「[インターネット インフォメーション サービス \(IIS\) サーバー証明書インストール手順](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md)」が実行済みであることを確認します。  
  
4.  ソリューションをビルドするには、「[Windows Communication Foundation サンプルのビルド](../../../../docs/framework/wcf/samples/building-the-samples.md)」の手順に従います。  
  
5.  複数コンピュータ構成でサンプルを実行するには、「[Windows Communication Foundation サンプルの実行](../../../../docs/framework/wcf/samples/running-the-samples.md)」の手順に従います。  
  
6.  クライアント ウィンドウが表示されたら、「Sample.txt」と入力します。ディレクトリで "Sample.txt のコピー" を検索する必要があります。  
  
## WSStreamedHttpBinding サービスのサンプル  
 `WSStreamedHttpBinding` を使用するサービスのサンプルは、サービス サブディレクトリにあります。`OperationContract` の実装は `MemoryStream` を使用して、最初に受信ストリームからすべてのデータを取得し、その後 `MemoryStream` を返します。このサンプル サービスは、インターネット インフォメーション サービス \(IIS\) によってホストされます。  
  
```  
[ServiceContract]  
public interface IStreamedEchoService  
{  
    [OperationContract]  
    Stream Echo(Stream data);  
}  
  
public class StreamedEchoService : IStreamedEchoService  
{  
    public Stream Echo(Stream data)  
    {  
        MemoryStream dataStorage = new MemoryStream();  
        byte[] byteArray = new byte[8192];  
        int bytesRead = data.Read(byteArray, 0, 8192);  
        while (bytesRead > 0)  
        {  
            dataStorage.Write(byteArray, 0, bytesRead);  
            bytesRead = data.Read(byteArray, 0, 8192);  
        }  
        data.Close();  
        dataStorage.Seek(0, SeekOrigin.Begin);  
  
        return dataStorage;  
    }  
}  
  
```  
  
## WSStreamedHttpBinding クライアントのサンプル  
 `WSStreamedHttpBinding` を使用してサービスとやり取りするクライアントは、クライアント サブディレクトリにあります。このサンプルで使用する証明書は Makecert.exe で作成されたテスト証明書なので、ブラウザで https:\/\/localhost\/servicemodelsamples\/service.svc のような HTTPS アドレスにアクセスしようとするとセキュリティ警告が表示されます。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] クライアントがテスト証明書に対して問題なく動作するようにするには、クライアントにコードを追加して、セキュリティ警告を非表示にする必要があります。そのためのコードとそれに必要なクラスは、本運用の証明書を使用するときには不要です。  
  
```  
// WARNING: This code is only required for test certificates such as those created by makecert. It is   
// not recommended for production code.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
  
```  
  
## 参照