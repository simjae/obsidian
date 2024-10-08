
1. **Canvas 기반 렌더링:**
    
    - Excalidraw는 **HTML5 Canvas**를 기반으로 렌더링합니다. Canvas는 픽셀 단위의 제어가 가능하여, **실시간 드로잉 및 지연 없이** 복잡한 그래픽을 효율적으로 처리할 수 있습니다.
    - Canvas의 `requestAnimationFrame`을 활용하여 애니메이션이나 드로잉 연산을 GPU 가속을 통해 부드럽게 구현합니다.
2. **React의 상태 관리와 동기화:**
    
    - Excalidraw는 React 상태 관리와 Canvas 렌더링을 조화롭게 사용합니다.
    - 상태 관리가 필요한 데이터만 React 컴포넌트에서 관리하고, 순수한 렌더링은 Canvas에서 처리하여 불필요한 React 리렌더링을 최소화합니다.
3. **Virtualization 기법:**
    
    - Excalidraw는 현재 화면에 보이는 영역만 렌더링하고, 보이지 않는 영역은 렌더링하지 않는 **가상화 기법**을 사용합니다.
    - 이 기법은 특히 대규모 드로잉이나 노드가 있을 때 렌더링 성능을 크게 향상시킵니다.
4. **웹 워커(Web Workers):**
    
    - 무거운 연산(예: 복잡한 드로잉 계산, 데이터 처리 등)은 **웹 워커**를 통해 메인 스레드와 분리하여 비동기적으로 처리합니다.
    - 이를 통해 UI 스레드가 차단되지 않아, 사용자가 인터랙션할 때 끊김 없이 부드럽게 동작합니다.
5. **최적화된 데이터 구조:**
    
    - Excalidraw는 드로잉 객체들을 효율적으로 관리하기 위해 **최적화된 데이터 구조**(예: 해시맵 또는 퀵 선택 데이터 구조)를 사용합니다.
    - 이러한 구조는 특정 객체의 속성이나 위치를 빠르게 업데이트하거나 선택할 수 있도록 도와줍니다.
6. **Reconciler 사용 및 최소화된 리렌더링:**
    
    - Excalidraw는 `reconciler`를 사용해 **변경된 부분만 업데이트**합니다. 이렇게 하면 전체 컴포넌트를 다시 렌더링하지 않고도 필요한 부분만 업데이트할 수 있습니다.
7. **오프스크린 캔버스 (Offscreen Canvas):**
    
    - `OffscreenCanvas`는 메인 스레드와 독립적으로 작동하는 캔버스로, **복잡한 렌더링 작업**을 백그라운드에서 처리할 수 있습니다.
    - Excalidraw는 이를 활용해 무거운 렌더링 작업을 백그라운드에서 수행하고, 메인 스레드는 사용자와의 인터랙션에 집중할 수 있게 합니다.