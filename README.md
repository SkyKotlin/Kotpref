# Kotpref

SharedPreference delegation for Kotlin.

## How to use

### Create preference model

```kotlin
public object UserInfo : KotprefModel() {
    var name: String by stringPrefVar()
    var age: Int by intPrefVar()
    var highScore: Long by longPrefVar()
    var threshold: Float by floatPrefVar()
    var prizes: MutableSet<String> by stringSetPrefVar(default = TreeSet<String>())
}
```

### Set up

```kotlin
Kotpref.init(context)
```

### Read and Write

```kotlin
UserInfo.name = "chibatching"
UserInfo.age = 30
UserInfo.highScore = 49219902
UserInfo.threshold = 49.21F
UserInfo.prizes.add("Bronze")
UserInfo.prizes.add("Silver")
UserInfo.prizes.add("Gold")

Log.d(javaClass.getSimpleName(), "User name: ${UserInfo.name}")
Log.d(javaClass.getSimpleName(), "User age: ${UserInfo.age}")
Log.d(javaClass.getSimpleName(), "User high score: ${UserInfo.highScore}")
Log.d(javaClass.getSimpleName(), "User threshold: ${UserInfo.threshold}")
UserInfo.prizes.forEachIndexed { i, s -> Log.d(javaClass.getSimpleName(), "prize[$i]: ${s}") }
```

### Result shared preference xml

XML file name equals model class name. If model class named `UserInfo`, XML file name is `UserInfo.xml`.

```xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <long name="highScore" value="49219902" />
    <set name="prizes">
        <string>Bronze</string>
        <string>Gold</string>
        <string>Silver</string>
    </set>
    <string name="name">chibatching</string>
    <int name="age" value="30" />
    <float name="threshold" value="49.21" />
</map>
```

### Options

#### Change default value

```kotlin
var age: Int by intPrefVar(18)
```

or

```kotlin
var age: Int by intPrefVar(default = 18)
```


#### Change XML file name

Override `kotprefName` property.

```kotlin
public object UserInfo : KotprefModel() {
    override val kotprefName: String = "user_info"
```

#### Change SharedPreference mode

Override `kotprefMode` property. Default is `Context.MODE_PRIVATE`.

```kotlin
public object UserInfo : KotprefModel() {
    override val kotprefMode: Int = Context.MODE_MULTI_PROCESS
```