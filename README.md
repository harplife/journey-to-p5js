# P5.js 정리

자바스크립트 라이브러리 P5.js에 대한 정보를 정리하며, 저자의 경험담을 공유한다.

## P5.js는 무엇인가

아주 간단히 말하자면, P5.js는 예술 전용 자바스크립트 라이브러리다.
포인트 그리기, 라인 그리기, 도형 그리기 등 캔버스에 그리는 기능을 메인으로,
외부 입력 장치의 데이터를 받아 이펙트를 주어 표출하는 등의 부가적인 기능과 함께,
개발자가 아닌 예술가가 쉽게 이해하고 사용할 수 있는 구조를 P5.js에서 제공한다.

실제로 _Generative Art/Digital Art_ 관련 분야에서 많이 사용되는 Processing 언어의 자바스크립트 버전이 P5.js이다.

## 왜 P5.js를 사용해야 하는가?

사용 용도는 명확하다 - P5.js의 모든 기능은 모두 예술을 위한 것이다.
캔버스 위에 간단한 도형을 그리거나,
마우스에 따라 이미지가 변형되게 하거나,
카메라에 찍힌 비디오를 작은 동그라미들로만 표출하거나,
마이크에 담기는 오디오에 따라 모형을 변형하는 것을 보여주거나,
기술에 한계, 상상의 한계까지 그 어느것이나 가능하다. (아마도)

## 장단점

### Pros

1. __초기 접근성이 좋다.__
   특히 `setup()`과 `draw()`를 중점으로 둔 구조를 봐도 자동으로 처리되는 요소들이 많다는 것을 알 수가 있으며,
   전체적인 구조가 미술가를 관점으로 만들어진 구조라는 것을 알수가 있다. 거기에 더불어 client-side interaction 기능들을 쉽게 제공해준다 (예: 슬라이더, 버튼, 키보드 이벤트, 마우스 이벤트 등).
2. __캔버스를 사용하며 이에 대한 기능이 많다.__
   보통 JS로 무언가를 그리고자 한다면 그 무언가는 데이터를 기반으로 한 차트일 가능성이 높다.
   그렇기 때문에 통상 "그리는" library들은 차트 그리는 기능 위주로 되어 있으며 SVG를 많이 활용한다.
3. __도움을 퍼부어주는 공동체가 있다.__
   p5.js community는 좀 작은 편이긴 하지만 그 뒤에 processing community가 제법 규모가 있는 편이다.
   p5.js로 이해가 안 되는 요소가 있으면 processing 위주로 확인하면 해결방안을 찾을 수가 있다.
4. __부가 기능이 많다.__
   DOM 활용, 웹캠 활용, Audio 활용 등의 기능들이 제공된다.

### Cons

1. __사용법이 좀 난해하다.__
  이는 js에 대한 이해가 부족해서 발생되는 이슈일 가능성도 있지만, 사용하다 보면 "이게 왜 안되지"라는 생각을 자주 하게 된다.
  그것도 "하라는 대로 했는데 이게 왜 안되지"가 아니라 "이렇게 하면 될 것 같은데 이게 안되네"에 더 가깝다.
2. __버그가 많다.__
3. __문서가 잘 되어있지 않다.__
4. __보고 배울수 있는 자료가 별로 없다.__
   그나마 유투브 채널 _coding train_이 도움을 많이 주는데, 매번 영상을 봐야하는게 귀찮고 p5.js의 모든 요소들을 하나하나 설명해주는 형식이 아니다.
5. __Contributor(개발자) 수가 적은 것 같다.__
   깃헙에 이슈를 2번 등록했는데, 한번은 p5.js 창시자가 직접 답변을 했고, 다른 한번은 일주일이 지나도 제대로 된 답이 나오지 않았다.
   업데이트도 자주 되는 편은 아닌 것 같다.
6. __관련된 구글 또는 stackoverflow 답변이 적다.__
   답이 안 되거나 제대로 된 답변이 없는 이슈가 꽤 있는 편이다.
7. __기본 renderer P2D를 사용할 경우 느리다.__
   `filter(BLUR, 3)`만 해도 frame rate이 크게 떨어지는 것을 볼수가 있다.
   물론 이 사항은 컴퓨터 사양에 따라 많은 영향을 받지만, 아무리 좋은 MacBook이여도 10 프레임 이하로 뚝 떨어지는 것 같다.
   이와 관련된 사항은 포럼에도 명시되어 있다 ([링크](https://forum.processing.org/two/discussion/11141/why-is-filter-blur-so-slow)).
8. __Renderer에 따라 사용법이 확 달라진다.__
   속도로 인한 이슈는 기존 renderer인 `P2D`를 `WEBGL`로 변경함으로서 해결할 수가 있다.
   이로서 CPU자원이 아닌 GPU자원을 사용함으로서 속도가 개선되는 것인데, 문제는 `P2D`와 `WEBGL`의 사용법이 다르다는 것이다.
   특히 Processing 코딩 디자인으로 봤을때 `P2D/CPU`는 2D 전용, `WEBGL/GPU`는 3D 전용으로 여기기 때문에 GPU로 2D 그래픽을 그리고 싶은 경우 3D 환경에서 2D 그래픽을 그려야 하는 어려움이 추가된다.
9. __이미지 관련 작업이 좀 어렵다.__
   - `loadImage()`를 사용하는 경우 외부 링크를 사용할 수 없다.
   - 이미지를 그리는 경우 `image()`를 사용해야 하는데, 이에는 그리는 대상(Canvas 또는 Graphic)에 대한 선택권이 없다.
     - `image()`로 이미지를 그리는 대신에, `img.loadPixel()`, `img.updatePixel()`을 활용하여 이미지 `object`에 픽셀 값들을 하나 하나 읽어 따로 `Graphic`에 그리는게 가능하다. [P5.js Examples](https://p5js.org/examples/)에 이미지 관련 예시들을 보면 실제로 그렇게 구현되어 있는 것을 볼 수가 있다. 저자의 생각엔 아마 이게 이미지 그리기 정석이다.
   - `filter()`, `tint()` 기능은 사실 이미지 대상으로 적용되는게 아니라 Canvas 대상 전체로 적용되기 때문에 여러모로 불편하다. 
   - 지정된 `filter()` 기능 규격 외의 custom filter를 만들 수가 없는 것 같다 - 대신에 custom `Shader()`는 사용이 가능한데, 이건 `WEBGL` renderer를 사용해야만이 가능한 기능이며, custom `Shader()`를 만드는 방식은 공식 문서에 자세히 명시되어 있지 않다.
   - 사실상 이미지 `object` 자체에 직접적인 영향을 주는 기능은 없는 듯 하다. Pixel 자체에 영향을 주는게 최선인 듯 하다.

## 프로젝트 리스트

1. 
2. 

