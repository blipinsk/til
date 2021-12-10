# Destructuring declarations in lambda expressions
(_2021/12/09_)

Kotlin lets you mix destructured declarations (e.g. for `data classes`) and regular parameters when creating lambda expressions.

---

When specifying a lambda expression, you would usually do this:

```kotlin
data class Rgb(val r: Float, val g: Float, val b: Float)

fun initColorPicker(onSelectionChanged: (rgb: Rgb, alpha: Float) -> Unit) {
  // ... do something
}

initColorPicker { rgb, alpha ->
  println("RED=${rgb.r}, GREEN=${rgb.g}, BLUE=${rgb.b}, ALPHA=$alpha")
}
```

but with a destructured declaration, you can simplify it using a parentheses `()`:

```kotlin
initColorPicker { (r, g, b), alpha ->
  println("RED=$r, GREEN=$g, BLUE=$b, ALPHA=$alpha")
}
```
