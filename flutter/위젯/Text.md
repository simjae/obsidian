`Text` 위젯은 Flutter에서 텍스트를 표시하는 기본 위젯입니다. 다양한 속성을 통해 글자의 크기, 색상, 정렬, 스타일 등을 손쉽게 조정할 수 있습니다. `Text`는 React Native의 `Text`와 매우 유사하며, 다양한 속성을 제공하여 자유로운 텍스트 스타일링이 가능합니다.

**주요 속성**

1. **data**: 표시할 문자열을 설정합니다.
   
2. **style**: `TextStyle` 객체로 텍스트의 색상, 크기, 굵기 등을 설정합니다.
   
3. **textAlign**: 텍스트 정렬을 설정합니다. `TextAlign.center`, `TextAlign.left`, `TextAlign.right` 등.
   
4. **overflow**: 텍스트가 넘칠 경우 어떻게 처리할지 설정합니다. `TextOverflow.ellipsis`로 줄임표 표시 가능.
   
5. **maxLines**: 텍스트 표시의 최대 줄 수를 설정합니다.
   
6. **softWrap**: 텍스트 줄바꿈을 허용할지 설정합니다. `true` 또는 `false`.
   
7. **textDirection**: 텍스트 방향을 설정합니다. `TextDirection.ltr` (왼쪽에서 오른쪽) 또는 `TextDirection.rtl`.
   
8. **textScaleFactor**: 기본 텍스트 크기 대비 확장 비율을 설정합니다.
   
9. **semanticsLabel**: 접근성을 위해 화면 판독기에 사용할 레이블을 설정합니다.
   
10. **locale**: 지역 설정을 통해 언어별 특수 문자를 설정할 수 있습니다.
    
11. **strutStyle**: 텍스트 높이를 조정하여 줄 간격을 설정합니다.
    
12. **key**: 위젯의 고유 키를 설정하여 특정 텍스트를 참조할 수 있습니다.
    
13. **textWidthBasis**: 텍스트의 너비 기준을 설정하여 레이아웃을 정밀하게 조정할 수 있습니다.
    
14. **textHeightBehavior**: 줄 높이를 제한하거나, 줄 높이의 추가적인 설정을 허용합니다.
    
15. **selectionColor**: 텍스트 선택 시 하이라이트 색상을 설정합니다.
    
16. **showCursor**: 텍스트 선택 시 커서를 표시할지 여부를 설정합니다.
    
17. **cursorColor**: 텍스트 선택 커서의 색상을 지정합니다.
    
18. **cursorHeight**: 커서의 높이를 설정합니다.
    
19. **cursorRadius**: 커서의 모서리 둥글기 정도를 설정합니다.
    
20. **textBaseline**: 텍스트의 기준선을 설정합니다. `TextBaseline.alphabetic`, `TextBaseline.ideographic`.
    

**추가 속성 및 팁**

21. **letterSpacing**: `TextStyle`의 `letterSpacing`을 사용하여 글자 간격을 설정합니다.
    
22. **wordSpacing**: `TextStyle`의 `wordSpacing`을 사용해 단어 간격을 설정합니다.
    
23. **fontFeatures**: `TextStyle`에서 사용하여 폰트 기능을 활성화합니다. (ex. `FontFeature.enable('smcp')`로 소문자를 대문자로 변환)
    
24. **foreground**와 **background**: 텍스트의 전경과 배경을 색상 외에도 `Paint`로 더 세밀하게 제어합니다.
    
25. **fontFamilyFallback**: 글꼴이 없을 때 사용할 글꼴 목록을 설정하여 다양한 언어 지원을 할 수 있습니다.


### **상황별 스타일링 예제**

1. **Center-aligned Bold Text with Spacing**
	- 중앙 정렬된 볼드 텍스트와 글자 간격을 설정하는 예제입니다.  
```
Text(
  "Welcome to Flutter!",
  textAlign: TextAlign.center, // 텍스트를 중앙 정렬
  style: TextStyle(
    fontSize: 24, // 텍스트 크기 설정
    fontWeight: FontWeight.bold, // 볼드체 적용
    color: Colors.blue, // 텍스트 색상
    letterSpacing: 2.0, // 글자 간격을 2.0으로 설정
  ),
)

```

2. ** **Ellipsis Overflow with Max Lines****
	- 텍스트가 길 때 두 줄까지만 표시하고, 넘치는 텍스트는 줄임표(...)로 표시하는 예제입니다.
```Dart
Text(
  "This is a long text that will get truncated if it exceeds two lines",
  maxLines: 2, // 최대 두 줄까지만 표시
  overflow: TextOverflow.ellipsis, // 넘치는 텍스트는 줄임표(...)로 표시
  style: TextStyle(
    fontSize: 18, // 텍스트 크기
    color: Colors.black, // 텍스트 색상
  ),
)
```

3. **Stylized Text with Shadows and Gradient**  
	- 텍스트에 그림자와 그라데이션 색상을 적용하여 스타일을 강조하는 예제입니다.
```Dart
Text(
  "Stylish Text",
  style: TextStyle(
    fontSize: 30, // 텍스트 크기
    fontWeight: FontWeight.w600, // 텍스트 굵기 설정
    foreground: Paint() // 텍스트의 전경을 페인트로 스타일링
      ..shader = LinearGradient(
        colors: <Color>[Colors.pink, Colors.orange], // 그라데이션 색상 설정
      ).createShader(Rect.fromLTWH(0.0, 0.0, 200.0, 70.0)),
    shadows: [
      Shadow(
        offset: Offset(3.0, 3.0), // 그림자 위치 조정
        blurRadius: 3.0, // 그림자 흐림 효과
        color: Colors.black38, // 그림자 색상 설정
      ),
    ],
  ),
)

```


4. **Responsive Text with Scale Factor**  
	- 텍스트 크기를 화면 크기에 맞춰 확장하는 반응형 텍스트 예제입니다.
```Dart
Text(
  "Responsive Text",
  textScaleFactor: 1.5, // 텍스트 크기를 1.5배로 확장
  style: TextStyle(
    fontSize: 16, // 기본 텍스트 크기
    color: Colors.green, // 텍스트 색상
  ),
)
```

5. **Text with Custom Font and Features**  
	- 사용자 정의 폰트와 폰트 기능을 적용하여 특별한 텍스트 스타일을 만드는 예제입니다.
```Dart
Text(
  "Flutter Custom Font",
  style: TextStyle(
    fontFamily: 'RobotoMono', // 사용자 정의 폰트 설정
    fontFeatures: [FontFeature.enable('smcp')], // 소문자를 대문자로 변환하는 기능 활성화
    fontSize: 24, // 텍스트 크기
    color: Colors.indigo, // 텍스트 색상
  ),
)
```