AID-应用标识符的组成规则

AID:即唯一标识一个应用，分为两部分，RID\(5字节\)+PIX（最多11字节）

RID:注册标识符，由ISO组织来分配，标识一个全球唯一的应用提供商，一般是分配给卡组织。

PIX:扩展应用标识符，一般是由应用提供商自己定义。



|  |  |  |  | AID |
| :--- | :--- | :--- | :--- | :--- |
| 发卡行 | RID | 产品 | PIX | AID |
| Visa | A0 00 00 00 03 | Visa credit or debit | 10 10 | A0 00 00 00 03 10 10 |
|  |  | Visa Electron | 20 10 | A0 00 00 00 03 20 10 |
|  |  | Interlink | 30 10 | A0 00 00 00 03 30 10 |
|  |  | V PAY | 20 20 | A0 00 00 00 03 20 20 |
|  |  | Plus | 80 10 | A0 00 00 00 03 80 10 |
| MasterCard | A0 00 00 00 04 | MasterCard credit or debit | 10 10 | A0 00 00 00 04 10 10 |
|  |  | MasterCard | 99 99 | A0 00 00 00 04 99 99 |
|  |  | MasterCard\(debit card\) | 30 60 | A0 00 00 00 04 30 60 |
|  |  | Cirrus\(interbank network\) | 60 00 | A0 00 00 00 04 60 00 |
| UK Domestic Maestro | A0 00 00 00 05 | Meastro UK | 00 01 | A0 00 00 00 05 00 01 |
|  |  | Solo | 00 02 | A0 00 00 00 05 00 02 |
| American Expree | A0 00 00 00 25 | American Expree | 01 | A0 00 00 00 25 01 |
| JCB | A0 00 00 00 65 | Japan Credit Bureau | 10 10 | A0 00 00 00 65 10 10 |
| PBOC | A0 00 00 03 33 | PBOC借记应用 | 01 01 01 | A0 00 00 03 33 01 01 01 |
|  |  | PBOC贷记应用 | 01 01 02 | A0 00 00 03 33 01 01 02 |
|  |  | PBOC准贷记应用 | 01 01 03 | A0 00 00 03 33 01 01 03 |
|  |  | PBOC纯电子现金应用 | 01 01 06 | A0 00 00 03 33 01 01 06 |
| RuPay\(India\) | A0 00 00 05 24 | RuPay | 10 10 | A0 00 00 05 24 10 10 |



