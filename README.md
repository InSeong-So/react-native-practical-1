- [공식 스타일링 문서]( https://reactnative.dev/docs/style)
- [공식 스타일링 컬러](https://reactnative.dev/docs/colors)
- [다양한 코어 컴포넌트](https://reactnative.dev/docs/view)
  - [컴포넌트가 지원하는 스타일 프로퍼티 1](https://reactnative.dev/docs/view#style)
  - [컴포넌트가 지원하는 스타일 프로퍼티 2](https://reactnative.dev/docs/view-style-props)

View는 기본적으로 플렉스 박스로 자식 요소 세로 정렬을 기본 요소로 함

iOS는 Text 컴포넌트에서 borderRadius를 지원하지 않으므로 View로 감싸주는 등 Wrapper 패턴을 사용해야 한다.

React Native는 스타일 상속이 존재하지 없다. color, box 프로퍼티 상속은 없으므로 별도로 설정해야 한다.

각 요소의 높이와 view를 확인하고 스크롤을 추가하는 브라우저와 달리 Native 앱은 이를 지원하지 않지만, 코어 컴포넌트로 제공한다.
- 스크롤 가능 속성은 ScrollView가 제공하지만 스크롤 가능한 영역은 부모 요소가 결정한다. 즉, ScrollView가 위치하는 컨테이너이다.
- 일반적인 View를 추가해서 사용 가능한 높이를 제한하고 View가 높이를 차지하는 공간을 선언해줘야 한다.
- ScrollView는 스크롤을 추가하기에 아주 적합하나 아주 길어질 목록에 대한 스크롤로는 적당하지 않다. ScrollView는 UI가 렌더링 될 때마다 모든 영역을 재렌더링한다. 따라서 1만개, 100만개여도 렌더링하므로 성능상 문제가 생긴다.
  - 즉, 분량이 제한적인 컨텐츠에는 ScrollView는 좋다.
- 더 나은 컴포넌트는 FlatList이다. 보이는 항목만 렌더링하고 화면 밖의 항목은 사용자가 스크롤해야 로딩 및 렌더링 된다. 내부적으로 로딩과 렌더링을 시작하도록 작은 임계값을 갖는데, 사용자 액션에 의해 이를 제어한다.
  - data로 전체 데이터 리스트를, renderItem으로 하위 컴포넌트를 정의하며 metaData까지 합쳐져서 param으로 전달되기 때문에 index, item 프로퍼티를 활용해야 한다. 자식 컴포넌트 자체에 key를 필요로 하지 않는다.
  - FlatList는 자동으로 key를 찾기 때문에 데이터 리스트 하위에 key라는 프로퍼티를 정의해두면 된다.
  - 데이터 리트스에 키를 저장하고 싶지 않다면, 그 대안은 id를 정의하는 것이다. 이것도 싫다면 keyExtractor 라는 프로퍼티를 선언해서 키를 생성하면 된다.

React Native는 클릭 이벤트가 없으며, Pressable 컴포넌트로 원하는 컴포넌트를 감싸서 작업해야 한다.
- Pressable, TouchableHightlight, TouchableNativeFeedback, TouchableOpacity 등 다양하게 존재

Image는 React-Native에서 제공하는 코어 컴포넌트로 source 프로퍼티에 require() 구문으로 절대 경로를 입력하여 호출한다. 스타일로 레이아웃을 정할 수 있다.

Expo를 사용하면 루트 경로의 app.json에서 각 배경을 설정할 수 있다.

앱을 완성하고 보면 Native의 상태 표시줄이 보기 불편해지는데, Expo의 StatusBar 컴포넌트가 이를 효과적으로 해결해준다.