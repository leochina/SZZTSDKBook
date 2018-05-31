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

AID示例：

9F0608A0000003330101019F09020140DF010100DF1105D84000A800DF1205D84004F800DF130500100000009F1B0400000000DF150400000000DF160199DF170199DF14039F3704DF1801019F7B06000000100000DF1906000000100000DF2006999999999999DF2106000000100000

9F06 - 应用AID

```
Length = 8

Value = A0 00 00 03 33 01 01 01 
```

9F09 - --

```
Length = 2

Value = 01 40 
```

DF01 - 应用选择指示符

```
Length = 1

Value = 00 
```

DF11 - TAC缺省

```
Length = 5

Value = D8 40 00 A8 00 
```

DF12 - TAC联机

```
Length = 5

Value = D8 40 04 F8 00 
```

DF13 - TAC拒绝

```
Length = 5

Value = 00 10 00 00 00 
```

9F1B - 终端最低限额

```
Length = 4

Value = 00 00 00 00 
```

DF15 - 偏置随机选择的阈值

```
Length = 4

Value = 00 00 00 00 
```

DF16 - 偏置随机选择的最大目标百分数

```
Length = 1

Value = 99 
```

DF17 - 随机选择的目标百分数

```
Length = 1

Value = 99 
```

DF14 - 缺省DDOL

```
Length = 3

Value = 9F 37 04 
```

DF18 - 终端联机PIN支持能力

```
Length = 1

Value = 01 
```

9F7B - 终端电子现金交易限额

```
Length = 6

Value = 00 00 00 10 00 00 
```

DF19 - 非接触读写器脱机最低限额

```
Length = 6

Value = 00 00 00 10 00 00 
```

DF20 - 非接触读写器交易限额

```
Length = 6

Value = 99 99 99 99 99 99 
```

DF21 - 非接触读写器CVM限额

```
Length = 6

Value = 00 00 00 10 00 00 
```

RID示例：

DF25080420081231145137DF2801019F0605A0000003339F220101DF050420101231DF060101DF070101DF040103DF0314E881E390675D44C2DD81234DCE29C3F5AB2297A0DF028180BBE9066D2517511D239C7BFA77884144AE20C7372F515147E8CE6537C54C0A6A4D45F8CA4D290870CDA59F1344EF71D17D3F35D92F3F06778D0D511EC2A7DC4FFEADF4FB1253CE37A7B2B5A3741227BEF72524DA7A2B7B1CB426BEE27BC513B0CB11AB99BC1BC61DF5AC6CC4D831D0848788CD74F6D543AD37C5A2B4C5D5A93B

DF25 - --

```
Length = 8

Value = 04 20 08 12 31 14 51 37 
```

DF28 - --

```
Length = 1

Value = 01 
```

9F06 - 应用AID

```
Length = 5

Value = A0 00 00 03 33 
```

9F22 - 公钥索引

```
Length = 1

Value = 01 
```

DF05 - 公钥有效期

```
Length = 4

Value = 20 10 12 31 
```

DF06 - 公钥哈什算法标识

```
Length = 1

Value = 01 
```

DF07 - 公钥算法标识

```
Length = 1

Value = 01 
```

DF04 - 公钥指数

```
Length = 1

Value = 03 
```

DF03 - 公钥校验值

```
Length = 20

Value = E8 81 E3 90 67 5D 44 C2 DD 81 23 4D CE 29 C3 F5 AB 22 97 A0 
```

DF02 - 公钥模

```
Length = 128

Value = BB E9 06 6D 25 17 51 1D 23 9C 7B FA 77 88 41 44 AE 20 C7 37 2F 51 51 47 E8 CE 65 37 C5 4C 0A 6A 4D 45 F8 CA 4D 29 08 70 CD A5 9F 13 44 EF 71 D1 7D 3F 35 D9 2F 3F 06 77 8D 0D 51 1E C2 A7 DC 4F FE AD F4 FB 12 53 CE 37 A7 B2 B5 A3 74 12 27 BE F7 25 24 DA 7A 2B 7B 1C B4 26 BE E2 7B C5 13 B0 CB 11 AB 99 BC 1B C6 1D F5 AC 6C C4 D8 31 D0 84 87 88 CD 74 F6 D5 43 AD 37 C5 A2 B4 C5 D5 A9 3B 
```

示例代码：

```java
String aid = 9F0608A0000003330101019F09020140DF010100DF1105D84000A800DF1205D84004F800DF130500100000009F1B0400000000DF150400000000DF160199DF170199DF14039F3704DF1801019F7B06000000100000DF1906000000100000DF2006999999999999DF2106000000100000;

String rid = DF25080420081231145137DF2801019F0605A0000003339F220101DF050420101231DF060101DF070101DF040103DF0314E881E390675D44C2DD81234DCE29C3F5AB2297A0DF028180BBE9066D2517511D239C7BFA77884144AE20C7372F515147E8CE6537C54C0A6A4D45F8CA4D290870CDA59F1344EF71D17D3F35D92F3F06778D0D511EC2A7DC4FFEADF4FB1253CE37A7B2B5A3741227BEF72524DA7A2B7B1CB426BEE27BC513B0CB11AB99BC1BC61DF5AC6CC4D831D0848788CD74F6D543AD37C5A2B4C5D5A93B;

                boolean update = SDKManager.getPboc().updateRID(1, rid);
                if (update) {
                    Log.e(TAG, "rid update success!");
                } else {
                    Log.e(TAG, "aid update failed===>" + rid);
                }



                boolean update = SDKManager.getPboc().updateAID(1, aid);
                if (update) {
                    Log.e(TAG, "aid update success!");
                } else {
                    Log.e(TAG, "aid update failed===>" + aid);
                }
```



