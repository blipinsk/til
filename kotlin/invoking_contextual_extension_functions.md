# Invoking contextual extension functions
(_2022/03/02_)

Extension functions can be defined in a specific context.

E.g. here the `process` extension function is defined in the context of a `Clazz` instance:
```kotlin
class Clazz(
  val importantDependency: Dependency,
) {

  fun String.process(): String {
    return if (importantDependency.shouldReverse()){
      this.reversed()
    } else {
      this
    }
  }
}
```

You can easily run the `process` function in the context of a `Clazz` instance using `with` scoping function.
This is especially useful for Unit Testing.

(_using `mockk` and `strikt` in the example_  👇)
```kotlin
@RunWith(JUnit4::class)
class ClazzTest {

  private val importantDependency: Dependency = mockk()
  private val clazz = Clazz(importantDependency)

  @Test
  fun `process returns reversed string when shouldReverse is true`(){
    // given
    every { importantDependency.shouldReverse() } returns true
    val input = "abcd"
    val expected = input.reversed()

    // when
    val result = with(clazz) { input.process() }

    // then
    expectThat(result).isEqualTo(expected)
  }

  @Test
  fun `process returns unchanged string when shouldReverse is false`(){
    // given
    every { importantDependency.shouldReverse() } returns false
    val input = "abcd"

    // when
    val result = with(clazz) { input.process() }

    // then
    expectThat(result).isEqualTo(input)
  }
}
```
