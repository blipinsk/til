# Named parameters in function types
(_2021/12/10_)

Parameters defined for [Function Types](https://kotlinlang.org/docs/lambdas.html#function-types) can have names to describe their purpose/meaning.

Without any names:
```kotlin
fun initializeUi(onCredentialsChanged: (String, String) -> Unit){
  // ... do something
}
```

when building the lambda expression, there wouldn't be any suggestions from the IDE on the purpose of those `String` arguments:
```kotlin
initializeUi { s, s2 -> /* */ }
```
(you would need to manually change `s` and `s2` names to have correct values).

However if you used named parameters for the function type:
```kotlin
fun initializeUi(onCredentialsChanged: (login: String, password: String) -> Unit){
  // ... do something
}
```

everything would be clear out of the box (IDE would correctly fill this info in for you):

```kotlin
initializeUi { login, password -> /* */ }
```
