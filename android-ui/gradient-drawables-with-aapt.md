# Gradient drawables with aapt
(_2020/09/30_)

If you want to create a gradient drawable using a color resource, you would usually end up creating a separate color resource with applied transparency, or using the pure `hex` values in your gradient.

E.g. for a gradient from `100%` -> `20%` of:
```
<color name="aquamarine">#66ddaa</color>
```

You would either

1. Add:
```
<color name="aquamarine_20">#3366ddaa</color>
```
2. Use both resources:
```
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <gradient
        android:endColor="@color/aquamarine_20"
        android:startColor="@color/aquamarine"/>
</shape>
```

or, simply use hex values:
```
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <gradient
        android:endColor="#3366ddaa"
        android:startColor="#66ddaa"/>
</shape>
```

---

You can use AAPT2 (Android Asset Packaging Tool)  to create a gradient using your resource without duplicating color resources.

Applying transparency to colors using aapt2 is a bit convoluted because you actually need to use a `selector` for that:

```
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:aapt="http://schemas.android.com/aapt">
  <gradient>
    <aapt:attr name="android:endColor">
      <selector>
        <item
            android:alpha="0.2"
            android:color="@color/aquamarine"/>
      </selector>
    </aapt:attr>
    <aapt:attr name="android:startColor">
      <selector>
        <item
            android:alpha="1.0"
            android:color="@color/aquamarine"/>
      </selector>
    </aapt:attr>
  </gradient>
</shape>
```
