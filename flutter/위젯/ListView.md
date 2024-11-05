
`ListView`는 스크롤이 가능한 리스트 형태로 UI를 구성할 때 사용되는 위젯입니다. 수직 및 수평 방향으로 아이템을 배치할 수 있으며, 많은 양의 데이터를 표시할 때 최적화된 `ListView.builder`나 `ListView.separated` 등을 사용하여 효율적으로 리스트를 렌더링할 수 있습니다.

**주요 속성**

1. **children**: `ListView`의 각 아이템으로 사용할 위젯 목록입니다.
   
2. **scrollDirection**: 스크롤 방향을 설정합니다. `Axis.vertical` 또는 `Axis.horizontal`.
   
3. **padding**: 리스트의 패딩을 설정합니다.
   
4. **reverse**: 스크롤 방향을 역방향으로 설정합니다.
   
5. **primary**: 기본 스크롤 뷰로 설정할지 여부를 결정합니다.
   
6. **shrinkWrap**: 리스트가 스크롤 뷰 내에 있을 때 모든 아이템을 한 번에 렌더링할지 설정합니다.
   
7. **itemExtent**: 각 아이템의 고정 높이 또는 너비를 설정하여 렌더링 성능을 최적화할 수 있습니다.
   
8. **physics**: 스크롤 방식이나 바운스 효과 등을 설정합니다. (e.g., `BouncingScrollPhysics`, `NeverScrollableScrollPhysics`)
   
9. **controller**: `ScrollController`를 사용해 스크롤 제어를 추가할 수 있습니다.
   
10. **cacheExtent**: 현재 화면 외의 추가 아이템을 미리 로드하여 스크롤 성능을 높입니다.
    
11. **keyboardDismissBehavior**: 키보드를 닫을지 여부를 설정합니다. (`onDrag` 등)
    
12. **semanticChildCount**: 접근성 지원을 위해 자식 위젯 수를 설정합니다.

**ListView.builder 속성 및 추가 설명**

13. **itemBuilder**: 리스트 아이템을 생성하는 빌더 함수입니다. (반드시 제공해야 함)
    
14. **itemCount**: 리스트에 표시할 총 아이템 수를 설정합니다.
    
15. **addAutomaticKeepAlives**: `KeepAlive`를 자동으로 추가하여 상태를 유지할지 설정합니다.
    
16. **addRepaintBoundaries**: 스크롤 성능을 개선하기 위해 다시 그려야 할 범위를 지정합니다.

**ListView.separated 속성 및 추가 설명**

17. **separatorBuilder**: 아이템 사이에 구분선을 추가하는 빌더 함수입니다.
    
18. **shrinkWrap**: 스크롤 범위를 제한하여 리스트의 크기를 조정할 수 있습니다.

**상황별 스타일링 예제**

1. **Simple Vertical ListView**
    - 기본적인 수직 `ListView`로 여러 텍스트 아이템을 표시합니다.
```Dart
ListView(
  padding: EdgeInsets.all(8.0),
  children: [
    Text("Item 1"),
    Text("Item 2"),
    Text("Item 3"),
  ],
)

```

2. **Horizontal ListView with Scroll Control**
	- 가로 스크롤이 가능하며 스크롤 효과를 조정한 `ListView`입니다.
```Dart
ListView(
  scrollDirection: Axis.horizontal, // 가로 스크롤 설정
  physics: BouncingScrollPhysics(), // 바운스 스크롤 효과 추가
  children: [
    Container(width: 100, color: Colors.red, child: Center(child: Text("1"))),
    Container(width: 100, color: Colors.blue, child: Center(child: Text("2"))),
    Container(width: 100, color: Colors.green, child: Center(child: Text("3"))),
  ],
)

```

3. **ListView.builder for Large Data**
	- 많은 데이터를 효율적으로 렌더링할 때 사용하는 `ListView.builder`입니다.
```Dart
ListView.builder(
  itemCount: 100, // 100개의 아이템을 표시
  itemBuilder: (context, index) {
    return ListTile(
      title: Text("Item $index"),
    );
  },
)

```


4. **ListView.separated with Dividers**
	- 각 아이템 사이에 구분선을 추가한 `ListView.separated`입니다.
```Dart
ListView.separated(
  itemCount: 10, // 총 10개의 아이템
  itemBuilder: (context, index) {
    return ListTile(
      title: Text("Item $index"),
    );
  },
  separatorBuilder: (context, index) {
    return Divider(color: Colors.grey); // 각 아이템 사이에 구분선 추가
  },
)

```

5. **Fixed Height ListView for Optimization**
	- 고정된 높이의 아이템을 가진 `ListView`로 렌더링 성능을 높이는 예제입니다.
```Dart
ListView.builder(
  itemCount: 20,
  itemExtent: 50.0, // 각 아이템의 높이를 50으로 고정
  itemBuilder: (context, index) {
    return Container(
      color: index % 2 == 0 ? Colors.lightBlue : Colors.lightGreen,
      child: Center(child: Text("Fixed Height Item $index")),
    );
  },
)

```


---
**TIP**

- **대량 데이터 최적화**: `ListView.builder`와 `ListView.separated`는 많은 데이터를 다룰 때 렌더링 효율을 높여줍니다.
- **고정 크기 설정**: `itemExtent`를 사용하여 아이템의 고정 크기를 설정하면 스크롤 성능이 개선됩니다.
- **cacheExtent로 스크롤 성능 개선**: `cacheExtent`를 조정하여 화면에 보이지 않는 아이템을 미리 렌더링하여 스크롤 시 버벅임을 줄일 수 있습니다.