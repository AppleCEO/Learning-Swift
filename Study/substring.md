## substring



#### 1. 정의

- 문자열을 생성할때 하위문자열(부분열?)을 생성한다.
- 하위문자열은 본래의 문자열과 같은 저장소를 사용하기 때문에 하위문자얄의 작동은 빠르고 효율적이다.
- 문자열과 하위문자열은 동일한 인터페이스를 제공하기 때문에 문자열의 내용을 복사하거나 지연?시킬수 있다.



#### 2. 기본적인 사용

```swift
let greeting = "Hi there! It's nice to meet you! 👋"
let endOfSentence = greeting.index(of: "!")!
let firstSentence = greeting[...endOfSentence]
// firstSentence == "Hi there!"
```



#### 3. substring의 다양한 함수는 아래링크를 참조하자

- 내가 사용해본 함수

> `index(of: )` 함수와 nil결합연산자 사용
>
> - String의 범위 서브스크립트를 사용하여 원하는 숫자를 추출해냄
> - index of 함수의 반환타입이 옵셔널이기 때문에 nil결합연산자를 사용해주거나, 옵셔널 바인딩을 해야함

```swift
var cmUnitNum : String = "14444444cm"
cmUnitNum = "142m"

if cmUnitNum.contains("cm") {
    let firstCharOfUnit = cmUnitNum.index(of: "c") ?? cmUnitNum.endIndex
    let justNum = cmUnitNum[..<firstCharOfUnit]
    print (String("\(Double(justNum)!/100)m"))
} else {
    let firstCharOfUnit = cmUnitNum.index(of: "m") ?? cmUnitNum.endIndex
    let justNum = cmUnitNum[..<firstCharOfUnit]
    print (String("\(Double(justNum)!*100)cm"))
}
```

#### 

> `prefix(upTo: )`의 정의 : [원문](https://developer.apple.com/documentation/swift/string/2893967-prefix)
>
> upto 포지션의 전까지 포함하여 반환한다.

```swift
let numbers = [10, 20, 30, 40, 50, 60]
if let i = numbers.index(of: 40) {
    print(numbers.prefix(upTo: i))
}
// Prints "[10, 20, 30]"
```

> 삼항연산자 사용해서 내용변경

```swift
var (unitNumCm, just) = ("1.5m", "")
if unitNumCm.contains("cm") {
    just += unitNumCm.prefix(upTo: unitNumCm.index(of: "c")!)
} else {
    just += unitNumCm.prefix(upTo: unitNumCm.index(of: "m")!)
}
unitNumCm.contains("cm") ? print("\(Double(just)!/100)m") : print("\(Double(just)!*100)cm")
```



> `trimmingCharacters` 사용해서 구현

이 함수는 양끝의 문자를 지정해준 character로 제거해주는데, 제거하려는 character가

양끝중에서 한쪽에만 있어도 에러없이 제거 후 제거된 값을 반환해준다

만약 제거하려는 값만으로 구성되어 있다면 반복해서 제거후 빈문자열을 반환한다.

```swift
// version[3] : trimmingCharacters 사용
let cmStr = "145cm"
if cmStr.contains("cm") {
    print("\(Double(cmStr.trimmingCharacters(in: ["c","m"]))! / 100)m")
} else {
    print("\(Double(cmStr.trimmingCharacters(in: ["m"]))! * 100)cm")
}
```



#### 4. substring과 stringprotocol의 차이

>문자열을 처리하는 데이터 타입은 String 인데 핵심적인 기본 기능은 Struct String 에 구현해놓고, Substring은 문자열 중에 일부분만 접근할 때 사용하는 타입이고, StringProtocol은 기본 기능 외에 부가 기능들을 모아놓고 따로 구현한 함수들입니다.



#### 5. substring 사용

**```endIndex```** 의 정의를 잘 생각하고 사용하자!  

![d](http://postfiles12.naver.net/MjAxNzEwMTlfMjU3/MDAxNTA4NDAxMTkzOTYy.pOnpvUWSswqijhQf5KCURVXRVKXnIIkEdVJ-InNCRLEg.z4foMADkHiCYh9DsS7ZVVfj3eIzsE6gnhJJf4bFpccEg.PNG.bb_9900/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2017-10-19_%EC%98%A4%ED%9B%84_5.19.04.png?type=w773)

```swift
// 천재 정훈을 상수로 선언
let someString = "Genius JeongHoon!"

// 공백을 추출
var whiteSpace = someString.index(of: " ") ?? someString.startIndex

// 중간문자 제거후 합치기
someString.components(separatedBy: [" "]).joined()

// 문자열 subscript활용하여 앞문자열 뺴오기
var frontofSomeString = someString[someString.startIndex..<whiteSpace]

// 문자열 subscript활용하여 뒷문자열 뺴오기
/*
 someString.endIndex는 전체 길이에 +1 인거 같습니다
 var strTest =“12345”
 strTest.count 하면 5가 나오는데 갯수는 5개이고 endIndex도 그대로 사용하는 대신 0부터 시작해서 0..<5 해서 다 출력되는게 아닌가 싶네요
 */
var rearofSomeString = someString[someString.index(after: whiteSpace)..<someString.endIndex]
print (rearofSomeString)


let exampleString: String = "!!!!@@@@"
exampleString.trimmingCharacters(in: ["!","@"])
print(exampleString) // 출력결과 = 
```



