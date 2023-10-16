
### 水平虚线

```
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="line">

  <stroke
      android:color="#D3D3D3"
      android:dashGap="2dp"
      android:dashWidth="4dp"
      android:width="1dp"/>
</shape>
```

### 垂直虚线
//

```
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:left="-600dp"
        android:right="-600dp">
        <rotate
            android:drawable="@drawable/polygon_ic_line_stroke"
            android:fromDegrees="90"
            android:visible="true" />
    </item>
</layer-list>
```
