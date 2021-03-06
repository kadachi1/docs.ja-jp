---
title: "移行と相互運用性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "AutoGeneratedOrientationPage"
helpviewer_keywords: 
  - "コントロール [WPF 相互運用性]"
  - "相互運用性 [WPF]"
  - "移行 [WPF]"
  - "Windows フォーム コントロール [WPF 相互運用性]"
  - "Windows Presentation Foundation, 相互運用性"
  - "Windows Presentation Foundation, 移行"
  - "WPF, 相互運用性"
  - "WPF, 移行"
ms.assetid: d655de05-bf63-4814-bc64-6b3be01c70a2
caps.latest.revision: 41
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 41
---
# 移行と相互運用性
このページには、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションと、他の種類の [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] アプリケーションの相互運用を実装する方法を説明したドキュメントへのリンクが含まれています。  
  
## このセクションの内容  
 [WPF と Windows フォームの相互運用性](../../../../docs/framework/wpf/advanced/wpf-and-windows-forms-interoperation.md)  
 [WPF と Win32 の相互運用性](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)  
 [WPF と Direct3D9 の相互運用性](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)  
  
## 関連項目  
  
|語句|定義|  
|--------|--------|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ページの要素としてホストできるようにする要素。|  
|<xref:System.Windows.Forms.Integration.ElementHost>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] コントロールのホストに使用できる [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロール。|  
|<xref:System.Windows.Interop.HwndSource>|[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] アプリケーション内の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 領域をホストします。|  
|<xref:System.Windows.Interop.HwndHost>|<xref:System.Windows.Forms.Integration.WindowsFormsHost> の基本クラス。[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでホストされる場合に、HWND ベースの技術がすべて使用する基本機能を定義します。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション内で [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] ウィンドウをホストするには、これをサブクラス化します。|  
|<xref:System.Windows.Interop.BrowserInteropHelper>|ブラウザーがホストする [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションのブラウザー環境の状態を報告するヘルパー クラス。|  
  
## 関連項目