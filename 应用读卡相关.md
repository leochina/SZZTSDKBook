### 应用读卡的部分可以重点参考EMVManager这个类

EMVManager类实现了SZZTPboc.PBOCHandler接口。

1.EMVManager的构造方法

```java
public EMVManager(int transType, String amount, EmvBackListener listener) {
        this.transType = transType;
        this.strAmount = amount;
        if (!TextUtils.isEmpty(strAmount)) {
            this.iAmount = Integer.parseInt(strAmount.replace(".", ""));
        }
        emvBackListener = listener;
    }
```

这里第一个参数是交易的类型；第二个参数是交易金额；第三个参数是EMVManager结果的回调。

此时在外部调用readCard这个方法就能读卡了。

```java
public void readCard(boolean magCard, boolean icCard, boolean rfCard, boolean forceOnline,
                         boolean onlinePin) {
        this.forceOnline = forceOnline;
        this.onlinePin = onlinePin;
        this.supportMagCard = magCard;
        this.supportICCard = icCard;
        this.supportRFCard = rfCard;
        checkCard();
    }
```

2.SZZTPboc.ReadCardListener\(\)的读卡回调

```java
private SZZTPboc.ReadCardListener readCardListener = new SZZTPboc.ReadCardListener() {

        @Override
        public void onTimeout() {
            mSZZTPboc.stopCheckCard(); //close card reader
            emvBackListener.timeout();
        }

        @Override
        public void onError(int error) {
            Bundle mBundle = new Bundle();
            mBundle.putInt("error", error);
            mSZZTPboc.stopCheckCard();
            emvBackListener.card(error);
            checkCard(); //restart wait card
        }

        @Override
        public void onCardSwiped(Bundle track) {
            mSZZTPboc.stopCheckCard();
            if (track == null || track.getString("TRACK2") == null) {
                emvBackListener.card(ReadCardError.MAG_SWIPE_ERROR);
                checkCard(); //restart wait card
                return;
            }

            /*The Bank of China stipulates that the composite card is forbidden to swipe cards*/
            if (EMVCard.CheckIcCard(track.getString("TRACK2"))) {
                emvBackListener.card(ReadCardError.IC_FALL_BACK);
                checkCard(); //restart wait card
                return;
            }
            cardType = CARD_TYPE_MAG;
            getCardInfo(track); //read card successful, get card information
            emvBackListener.card(0);
        }

        @Override
        public void onCardActivate() {
            cardType = CARD_TYPE_RF;
            mSZZTPboc.stopCheckCard();
            Bundle bundle = new Bundle();
            bundle.putBoolean("isSupportQ", true);
            bundle.putBoolean("isSupportSM", true);
            bundle.putBoolean("isQPBOCForceOnline", EMVManager.this.forceOnline);
            bundle.putBoolean("isNeedOnlinePin", EMVManager.this.onlinePin);
            bundle.putInt("cardType", 1);
            bundle.putInt("authAmount", iAmount);
            bundle.putBoolean("rfCardNeedConfirmCard", true);
            mSZZTPboc.startPBOC(transType, bundle, EMVManager.this);
            DevicesUtil.doBeep();
        }

        @Override
        public void onCardPowerUp() {
            cardType = CARD_TYPE_IC;
            Bundle bundle = new Bundle();
            bundle.putBoolean("isSupportSM", true);
            bundle.putBoolean("isQPBOCForceOnline", EMVManager.this.forceOnline);
            bundle.putBoolean("isNeedOnlinePin", EMVManager.this.onlinePin);
            bundle.putInt("cardType", 0);
            bundle.putInt("authAmount", iAmount);
            mSZZTPboc.startPBOC(transType, bundle, EMVManager.this);

            mSZZTPboc.stopCheckCard();
//                mEmvBackListener.EMVcardExist(CARD_TYPE.IC_CARD);
        }
    };
```

这里的onCardPowerUp\(\)会在卡片上电成功时回调，onCardActivate\(\)会在读取非接卡成功时回调，onCardSwiped（）是读取磁条卡成功时回调，onTimeout\(\)会在读卡超时时回调，onError\(\)会在读卡失败时回调。

EmvBackListener是EMVManager的结果回调

```java
 public interface EmvBackListener {
        /**
         * the result of reading card
         * @param result 0:success
         */
        void card(int result);

        /**
         * the result of inputting password
         * @param result code
         * @param values pin block
         */
        void pin(int result, byte[] values);

        /**
         * read card timeout
         */
        void timeout();

        void EMVOnlineProcess(Bundle result);

        void EMVTransactionResult(int result, int detail);

    }
```

外部调用下面各种方法可以得到各种卡片的信息

```java
//获取卡号
    public String getPan() {
        return pan;
    }

    //服务码
    public String getServiceCode() {
        return serviceCode;
    }

    //卡片序列号
    public String getCardSn() {
        return cardSn;
    }

    //获取卡片过期日期
    public String getExpiredDate() {
        return expiredDate;
    }

    //获取二磁道信息
    public String getTrack2() {
        return track2;
    }

    //获取三磁道信息
    public String getTrack3() {
        return track3;
    }

    //获取卡片类型
    public int getCardType() {
        return cardType;
    }

    //判断是否需要输入密码
    public boolean isHavePin() {
        return havePin;
    }

    //获取IC卡信息
    public String getIcInfo() {
        return icInfo;
    }
```



