**open-data**是做一些隐私数据展示用，故不允许直接通过代码获取的。

```
<view class="userinfo-avatar" bindtap="bindViewTap">
    <open-data type="userAvatarUrl"></open-data>
</view>
<open-data type="userNickName"></open-data>
```

页面会直接显示头像和昵称，不需要用授权。

---

**open-data**

解析：用于展示微信开放的数据，不需要授权也可以获取部分的用户数据。

groupName：拉取群名称  
userNickName：用户昵称  
userAvatarUrl：用户头像  
userGender：用户性别  
userCity：用户所在城市  
userProvince：用户所在省份  
userCountry：用户所在国家  
userLanguage：用户的语言
