ComfyUI는 다재다능한 오픈소스 이미지 생성형 AI인 스테이블 디퓨전을 위한 GUI중 하나입니다. 원래는 AUTOMATIC1111이 훨씬 더 많이 사용되었지만, 여러가지 워크플로를 쉽게 생성하고 변경할 수 있어서 사용자가 급격하게 늘어나는 중입니다. 

다만, ComfyUI는 스테이블 디퓨전의 기술적인 내용과 많은 관련이 있어서 사용하기가 쉽지 않습니다. 요즘 들어 ComfyUI 에 관한 글이 더 많아졌는데, 사용법이 잘 정리된 문서가 없어서 고민하던 중이었는데, 이 투토리얼은 아주 기초적인 내용부터 고급 사용법까지 아우르는 여러가지 내용을 담고 있습니다. 처음부터 따라해보면 ComfyUI를 좀 더 확실하게 이해하실 수 있게 될 것입니다.

이 투토리얼은 Open.ai 의 [ComfyUI Academy](https://openart.ai/workflows/academy)에 올려진 11개의 유튜브 내용을 나름 편집해 정리한 것입니다. 따라서 이 글을 읽으신다면 해당 유튜브를 보면서 읽는 것을 추천드립니다.

이 튜토리얼은 모두 세편으로 이루어져 있습니다.

- [ComfyUI 튜토리얼-1](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1) : 유튜브 1~4편
- [ComfyUI 튜토리얼-2](https://www.internetmap.kr/entry/ComfyUI-Tutorial-2) : 유튜브 5~8편
- [ComfyUI 튜토리얼-3](https://www.internetmap.kr/entry/ComfyUI-Tutorial-3) : 유튜브 9~11편

아래는 이 글의 목차입니다.

- [ComfyUI 아카데미 소개](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#intro)
- [레슨 1: ComfyUI 사용하기 기본(Using ComfyUI, EASY basics)](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#lesson1)
    - [ComfyUI Manager 설치](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#manager)
    - [워크플로 생성시 참고사항](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#info)
    - [Reroute 노드 활용](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#reroute)
    - [입력슬롯과 입력위젯 바꾸기](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#slot)
- [레슨 2: 멋진 ComfyUI txt2img 비법](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#lesson2)
    - [비슷한 이미지 동시 생성](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#multi)
    - [ControlNet을 사용한 개선](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#controlnet)
    - [최종 워크플로](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#final)
- [레슨 3: 잠재 이미지 확대(Latent Upscaling)](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#lesson3)
- [레슨 4: Image to Image 생성](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#lesson4)
    - [기본 img2img](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#bimg2img)
    - [고급 img2img](https://www.internetmap.kr/entry/ComfyUI-Tutorial-1#aimg2img)

## ComfyUI 아카데미 소개

Openart.ai는  이미지 생성형 AI와 관련해 제가 좋아하는 사이트중 하나입니다. 그런데 얼마전 사이트가 전면적으로 개편되면서, ComfyUI 를 기본으로 사용하는 것처럼 보입니다. 아직 세세하게 살펴본 건 아니지만요.

그중에서 [ComfyUI Academ](https://openart.ai/workflows/academy)y라고, ComfyUI 사용법을 알려주는 코너가 생겼습니다. 현재 총 11개의 유튜브가 올려져 있는데, 기본적인 내용이 많기는 해도 중간중간 쓸만한 정보들이 포함되어 있어서 소개드리려고 합니다. 

![](https://blog.kakaocdn.net/dn/wQ8pc/btsEEyLgngr/nklMboKoLqU5YX3CBXbBdK/img.png)

다만, 유튜브 내용을 모두 정리하는 것은 별로 필요가 없을 듯하고, 제가 잊어버리지 않도록 정리하는 차원이니, 관련 내용을 원하시면 직접 사이트를 방문하시는 게 좋을 것 같습니다.





9,10,11,12