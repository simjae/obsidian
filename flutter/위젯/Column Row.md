
`Column`과 `Row`는 자식 위젯을 수직 또는 수평으로 배치하는 레이아웃 위젯입니다. 둘 다 Flutter의 레이아웃 구성에서 매우 중요하며, 자식 위젯을 배열할 때 다양한 옵션을 제공합니다.

**주요 속성**

1. **children**: `Column` 또는 `Row` 안에 배치할 위젯 목록을 설정합니다.
2. **mainAxisAlignment**: 주 축 방향(수직/수평)으로 자식 위젯의 정렬을 설정합니다.
3. **crossAxisAlignment**: 반대 축 방향(수평/수직)으로 자식 위젯의 정렬을 설정합니다.
4. **mainAxisSize**: 주 축의 크기를 자식 위젯에 맞출지, 부모 크기를 꽉 채울지 설정합니다.
5. **verticalDirection**: 수직 방향으로 배치할 때 위젯을 위에서 아래로, 또는 아래에서 위로 정렬할 수 있습니다.
6. **textDirection**: 텍스트 방향을 설정하여 위젯의 배치를 LTR(왼쪽에서 오른쪽) 또는 RTL(오른쪽에서 왼쪽)으로 지정합니다.
7. **key**: 위젯의 고유 키를 설정하여 특정 요소를 참조할 수 있습니다.
8. **textBaseline**: 텍스트 기준선을 설정합니다. `alphabetic` 또는 `ideographic`를 선택할 수 있습니다.

**추가 속성 및 팁**

9. **mainAxisAlignment - spacing**: `SpaceBetween`, `SpaceAround`, `SpaceEvenly`를 통해 자식 위젯 간 간격을 설정할 수 있습니다.
10. **Expanded 및 Flexible**: `Expanded` 또는 `Flexible`을 자식 위젯으로 사용해 `Column`이나 `Row` 내에서 가변 크기를 조정할 수 있습니다.
11. **IntrinsicWidth**와 **IntrinsicHeight**: `Column`과 `Row`의 자식 위젯 크기를 부모 위젯의 크기에 맞추어 자동 조정할 때 사용됩니다.
12. **SizedBox**: 위젯 사이에 고정 간격을 추가하려면 `SizedBox`를 사용합니다.


**상황별 스타일링 예제**

1. **Vertically Centered Column with Spacing**
	-  자식 위젯을 수직 중앙에 정렬하고, 간격을 균등하게 배치한 `Column`입니다.
```Dart
Column(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly, // 자식 위젯 사이에 균등한 간격을 추가
  crossAxisAlignment: CrossAxisAlignment.center, // 수평 중앙 정렬
  children: [
    Text("Item 1"),
    Text("Item 2"),
    Text("Item 3"),
  ],
)

```

2. **Row with Expanded Widgets**
	- `Expanded`를 사용하여 `Row`의 자식들이 가능한 공간을 균등하게 차지하도록 만듭니다.
```Dart
Row(
  children: [
    Expanded(
      child: Container(
        color: Colors.red,
        height: 100,
        child: Center(child: Text("Item 1")),
      ),
    ),
    Expanded(
      child: Container(
        color: Colors.blue,
        height: 100,
        child: Center(child: Text("Item 2")),
      ),
    ),
  ],
)

```


3. **Row with SpaceBetween**
	- `SpaceBetween`을 사용하여 `Row`에서 첫 번째와 마지막 아이템을 양 끝에 배치합니다.
```Dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceBetween, // 첫 번째와 마지막 아이템을 양 끝에 배치
  children: [
    Text("Left"),
    Text("Center"),
    Text("Right"),
  ],
)

```

4. **Nested Columns and Rows**
	- `Column`과 `Row`를 중첩하여 복잡한 레이아웃을 만드는 예제입니다.
```Dart
Column(
  children: [
    Row(
      mainAxisAlignment: MainAxisAlignment.spaceAround,
      children: [
        Icon(Icons.star, color: Colors.red),
        Icon(Icons.star, color: Colors.green),
        Icon(Icons.star, color: Colors.blue),
      ],
    ),
    SizedBox(height: 20), // 간격 추가
    Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        Text("Item 1"),
        Text("Item 2"),
        Text("Item 3"),
      ],
    ),
  ],
)
```

5. **Column with Flexible Widgets**
	- `Flexible`을 사용하여 각 위젯이 공간을 비율대로 차지하도록 설정하는 예제입니다.
```Dart
Column(
  children: [
    Flexible(
      flex: 2, // 비율을 2로 설정
      child: Container(
        color: Colors.orange,
        child: Center(child: Text("Flex 2")),
      ),
    ),
    Flexible(
      flex: 1, // 비율을 1로 설정
      child: Container(
        color: Colors.purple,
        child: Center(child: Text("Flex 1")),
      ),
    ),
  ],
)

```