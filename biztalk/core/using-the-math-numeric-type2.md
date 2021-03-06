---
title: 使用 MATH_NUMERIC Type2 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- exponents, JD Edwards OneWorld adapters
- currency, JD Edwards OneWorld adapters
- MATH_NUMERIC type
- adapters [JD Edwards OneWorld adapters], currency
ms.assetid: 14d04576-0028-4af4-84bd-92c4ca492126
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 13de687f158bc18f4fa6a036ab239a25774d02ba
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36998902"
---
# <a name="using-the-mathnumeric-type"></a>使用 MATH_NUMERIC 类型
本主题介绍了 MATH_NUMERIC 类型并详细说明了指数的处理方式、数字的最大位数以及小数的最大位数。 它还包括有关以下内容的讨论：  
  
- 指数的后面  
  
- 无效值  
  
- 操作精度  
  
- 货币  
  
  MATH_NUMERIC 类型为数值字符串类型。 若要使用此类型，请输入以下格式的参数值：  
  
```  
<OptionalSign><IntegerAndFractionalPart><OptionalExponentPart>  
```  
  
 位置  
  
- `<OptionalSign>` 可以是`+`或`-`。 `+` 默认值。  
  
- `<IntegerAndFractionalPart>` 是最大数值的 32 有效数字，不包括小数点符号。 小数点符号对于 JD Edwards OneWorld 安装来说是特定于区域设置的 - 通常为句点 (.) 或逗号 (,)。 数字可能是所有整数、 所有分数，或一部分整数和部分分数，但它们不能超过 32。  
  
- `<OptionalExponentPart>` 等于：  
  
  ```  
  'e' <OptionalSign><ExponentDigits>  
  ```  
  
  位置  
  
- `<OptionalSign>` 可以是`+`或-。 `+` 默认值。  
  
- `<ExponentDigits>` 最多是两位数字。 允许使用 63 之间，不包括零值。  
  
## <a name="valid-values"></a>有效值  
 有效 MATH_NUMERIC 值的示例：  
  
-   123.045  
  
-   4089 （请注意数千个没有逗号）  
  
-   -9084  
  
-   -230.75  
  
-   0.010503  
  
-   1.023e-10，其等同于 0.0000000001023  
  
-   0.097e5 或 0.097e + 5，等效于 9700  
  
-   1.0e-32，等于 0.00000000000000000000000000000001  
  
     （此值有效，因为在这种情况下，整数“0”将被忽略，所以有效小数位为 32。）  
  
## <a name="invalid-values"></a>无效值  
 无效的值取决于值的种类。 太小，为小数部分被解释为零 （全部有效数字都将丢失）。 一个整数，过多的有效数字会导致意外的结果。 在这种情况下，JD Edwards OneWorld 不会始终导致错误。  
  
 太大或太小的指数会返回无效值。  
  
 无效 MATH_NUMERIC 值的示例：  
  
- 1034.00000000000000000000000000001023-太多的有效数字  
  
- 1.023e-64-指数太小  
  
- 0.00317e64-指数太大  
  
  适用于符号和十进制符号以外的任何非数字字符会导致无效的值。  
  
## <a name="exponents"></a>指数的后面  
 指数由 JD Edwards OneWorld MATH_NUMERIC 提供以便于输入值。 但是，大多数值返回不带指数的后面 （与所有 32 有效数字可见）。  
  
## <a name="precision-for-operations"></a>操作精度  
 如果操作导致丢失精度，舍入将会发生。 例如：  
  
 1.9e-31 / 10.0 = 0.00000000000000000000000000000002  
  
 1.9e-31 / 100.0 = 0.00000000000000000000000000000000  
  
 在其他情况下，不可预知的结果发生，因为当非常大的正数值乘以另一个。  
  
 1.01e32 * 2.053e32 不生成可靠的结果并不会引发错误。  
  
 大多数业务情况下，未超过这些范围。  
  
## <a name="currency"></a>货币  
 当 JD Edwards OneWorld 业务功能需要货币值时，业务功能会始终对四个字符的货币代码拥有单独的参数。 不必传递此代码，除非您使用的货币不是为 JD Edwards OneWorld 系统配置的默认货币。  
  
## <a name="see-also"></a>请参阅  
 [附录 A：数据类型](../core/appendix-a-data-types.md)