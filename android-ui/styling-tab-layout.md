# Styling TabLayout
(_2020/09/13_)

There are two styles that you need to worry about when styling the `com.google.android.material.tabs.TabLayout`:

1. Root style of `TabLayout`
```xml
<style name="Widget.ExampleApp.Tabs" parent="Widget.Design.TabLayout">
    <item name="tabIndicatorColor">#FF00FF</item>
    <item name="tabIndicatorFullWidth">false</item>
    <item name="tabTextAppearance">@style/TextAppearance.ExampleApp.Tab</item>
</style>
```

2. `TextAppearance` used for the nested `Tab` texts.
```xml
<style name="TextAppearance.ExampleApp.Tab" parent="TextAppearance.Design.Tab">
    <item name="android:letterSpacing">-0.5</item>
    <item name="android:textSize">16sp</item>
</style>
```
---

The `TextAppearance` one is especially interesting, because there are a few gotchas with it:

* When you want to disable `textAllCaps` (it's `true` by default), you need to use **exactly** `textAllCaps` and **NOT** the `android:textAllCaps`.
```xml
<style name="TextAppearance.ExampleApp.Tab" parent="TextAppearance.Design.Tab">
    <item name="android:letterSpacing">-0.5</item>
    <item name="android:textSize">16sp</item>
    <item name="textAllCaps">false</item>
</style>
```

* Even though the root `TextAppearance` (the `TextAppearance.Design.Tab`) specifies the color `selector` for the text, when you try to specify your own, it's properties will be overridden by the `TabLayout's` params: `tabTextColor` & `tabTextSelectedColor`. Just use those two.

```xml
<style name="Widget.ExampleApp.Tabs" parent="Widget.Design.TabLayout">
    <item name="tabIndicatorColor">#FF00FF</item>
    <item name="tabIndicatorFullWidth">false</item>
    <item name="tabTextAppearance">@style/TextAppearance.ExampleApp.Tab</item>
    <item name="tabSelectedTextColor">#FF00FF</item>
    <item name="tabTextColor">#000000</item>
</style>
```
