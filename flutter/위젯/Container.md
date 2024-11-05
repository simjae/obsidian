`Container`는 Flutter에서 레이아웃을 구성할 때 가장 많이 사용하는 위젯입니다. `div`와 비슷하게 스타일링, 크기 조정, 배경, 여백 등을 설정할 수 있으며, 자식 위젯을 감싸거나 원하는 위치에 배치할 때 유용합니다.

**주요 속성**

1. **width**: 너비를 설정합니다. `double` 값으로 지정합니다.
   
2. **height**: 높이를 설정합니다.
   
3. **color**: 배경 색상을 설정합니다.
   
4. **padding**: 내부 여백을 설정하여, 자식 요소와 `Container` 사이에 공간을 추가합니다.
   
5. **margin**: 외부 여백을 설정하여 `Container`와 다른 요소들 사이에 공간을 추가합니다.
   
6. **alignment**: 자식 위젯을 `Container` 내에서 정렬할 수 있습니다.
   
7. **decoration**: `BoxDecoration`을 통해 그림자, 테두리, 둥근 모서리 등의 스타일을 추가할 수 있습니다.
   
8. **constraints**: `BoxConstraints`로 최소 및 최대 너비와 높이를 설정할 수 있습니다.
   
9. **child**: `Container` 내부에 배치할 위젯을 지정합니다.
   
10. **borderRadius**: `BoxDecoration`과 함께 모서리를 둥글게 만듭니다.
    
11. **boxShadow**: 그림자를 추가하여 입체감을 줄 수 있습니다.
    
12. **gradient**: 그라데이션 배경 색상을 적용할 수 있습니다.
    
13. **transform**: `Matrix4`로 회전, 크기 조정 등의 변형을 적용할 수 있습니다.
    
14. **clipBehavior**: 자식 위젯의 잘리는 부분을 설정합니다.
    
15. **foregroundDecoration**: `Container` 위에 추가적인 장식을 추가합니다.
    
16. **border**: 테두리를 설정할 수 있습니다.
    
17. **shape**: `BoxShape.circle`을 사용해 원형으로 설정하거나 기본 사각형을 사용할 수 있습니다.
    
18. **decorationImage**: 배경 이미지를 설정합니다.
    
19. **backgroundBlendMode**: 배경 이미지와 색상을 혼합하여 스타일링할 수 있습니다.
    
20. **alignmentGeometry**: 자식 위젯의 위치를 설정합니다.

**추가 속성 및 팁**

21. **semanticLabel**: 접근성을 위해 레이블을 설정할 수 있습니다.
    
22. **shadowColor**: 그림자 색상을 설정하여 더 강조된 효과를 줄 수 있습니다.
    
23. **boxConstraints**: 반응형 디자인을 위한 크기 제한을 설정합니다.
    
24. **opacity**: 투명도를 조절하려면 `Opacity` 위젯으로 감싸 사용합니다.
    
25. **alignmentDirectional**: RTL 레이아웃을 고려하여 정렬할 수 있습니다.

---

**상황별 스타일링 예제**

1. **Rounded Gradient Button with Shadow**

```Dart
Container(
  width: 150,
  height: 50,
  decoration: BoxDecoration(
    borderRadius: BorderRadius.circular(30),
    gradient: LinearGradient(
      colors: [Colors.blue, Colors.purple],
    ),
    boxShadow: [
      BoxShadow(
        color: Colors.black.withOpacity(0.2),
        spreadRadius: 3,
        blurRadius: 5,
        offset: Offset(0, 3),
      ),
    ],
  ),
  alignment: Alignment.center,
  child: Text(
    "Press Me",
    style: TextStyle(color: Colors.white, fontSize: 16),
  ),
)

```

2. **Responsive Container**

```Dart
Container(
  constraints: BoxConstraints(
    minWidth: 100,
    maxWidth: 300,
  ),
  padding: EdgeInsets.all(20),
  decoration: BoxDecoration(
    color: Colors.amber,
    borderRadius: BorderRadius.circular(20),
  ),
  child: Text("This container adjusts its width!"),
)

```

3. **Background Image with Overlay**

```Dart
Container(
  width: 300,
  height: 200,
  decoration: BoxDecoration(
    image: DecorationImage(
      image: AssetImage("assets/background.png"),
      fit: BoxFit.cover,
    ),
  ),
  foregroundDecoration: BoxDecoration(
    color: Colors.black.withOpacity(0.3),
  ),
  alignment: Alignment.center,
  child: Text(
    "Overlay Text",
    style: TextStyle(color: Colors.white, fontSize: 24),
  ),
)

```


4. **Complex Shape and Shadow**

```Dart
Container(
  width: 100,
  height: 100,
  decoration: BoxDecoration(
    color: Colors.green,
    borderRadius: BorderRadius.only(
      topLeft: Radius.circular(20),
      bottomRight: Radius.circular(20),
    ),
    boxShadow: [
      BoxShadow(
        color: Colors.green.withOpacity(0.5),
        blurRadius: 10,
        offset: Offset(3, 3),
      ),
    ],
  ),
  alignment: Alignment.center,
  child: Text("Shape!"),
)

```