如果EMV判断到卡片需要输入密钥的话，那么就会回调到EMVManager类中的onRequestInputPIN方法中去。

```java
@Override
    public void onRequestInputPIN(boolean isOnlinePin, int retryTimes) {
        Log.d(TAG, "onRequestInputPIN: ");
        callInputPIN(getPan());
    }
```

```java
 public void callInputPIN(String cardNo) {
        int ret1 = mPinpad.open(new SZZTPinpad.OnSendKeyListerner() {
            @Override
            public void onSendKey(int arg0) {
                /*if (arg0 == 2) {
                }*/
            }
        });

        if (ret1 < 0) {
            mSZZTPboc.abortPBOC();
            emvBackListener.pin(ret1, null);
            return;
        }
        mPinpad.setPinViewStyle(DataBaseManager.GetPosParam().getiKeyboardType());
        //the PIN PAD of KS8123 is external
        if (SDKManager.getModel().equals("KS8123")) {
            if (!TextUtils.isEmpty(strAmount) && !strAmount.equals("0"))
                mPinpad.showText(1, strAmount.getBytes(), true);
            else
                mPinpad.showText(1, null, true);
        }
        mPinpad.setPinLimit(new byte[]{0, 4, 6});
        if (DataBaseManager.GetPosParam().getIDesType() == FieldConstants.SM4)
        {
            mPinpad.calculatePinBlock(0, cardNo.getBytes(), 60000, 1,
                    PIN_TYPE_ANSI98, SZZTPinpad.Mode.MODE_SM4,
                    new SZZTPinpad.OnInputResultListener() {
                        @Override
                        public void onInputResult(int arg0, byte[] arg1) {
                            handlePinResult(arg0, arg1);
                        }
                    });
        } else {
            mPinpad.calculatePinBlock(0, cardNo.getBytes(), 60000, 1,
                    new SZZTPinpad.OnInputResultListener() {
                        @Override
                        public void onInputResult(int arg0, byte[] arg1) {
                            handlePinResult(arg0, arg1);
                        }
                    });
        }
    }
```

pinpad的open方法是打开密码键盘，如果返回大于等于0的话表示打开设备成功。其参数可以传进去一个OnSendKeyListerner的监听，在其onSendKey回调方法里面可以接受到输入的键盘值。setPinLimit方法用于限制密码键盘可输入的位数。calculatePinBlock方法用于获取联机pin。

