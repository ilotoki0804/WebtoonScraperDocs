# WebtoonScraper Github 및 PyPI 버전의 구조 및 사용

WebtoonScraper의 핵심 로직은 Apache-2.0 license로 Github에 공개되어 있습니다.
PyPI에서도 WebtoonScraper 패키지를 다운로드해 사용할 수 있습니다.

## WebtoonScraper 패키지 구조

WebtoonScraper 패키지는 다음과 같은 구조로 이루어져 있습니다.

```
WebtoonScraper/
├── __main__.py
├── base.py
├── directory_state.py
├── exceptions.py
└── scrapers/
    ├── _scraper.py
    ├── _callback_manager.py
    ├── _helpers.py
    └── _naver_webtoon.py
```

`base.py`에는 WebtoonScraper의 버전 정보, logger, 플랫폼 딕셔너리 등 WebtoonScraper의 기본적인 사항들이 저장되어 있습니다.

`directory_state.py`는 디렉토리의 내부 콘텐츠를 바탕으로 WebtoonScraper 형식의 웹툰 디렉토리인지 아니면 기타 다른 목적의 디렉토리인지 감지합니다.

`exceptions.py`는 WebtoonScraper에서 정의하는 모든 예외 타입이 정의되어 있습니다.

`scrapers` 서브모듈에는 WebtoonScraper에서 웹툰을 다운로드하는 골격인 Scraper와 네이버 웹툰을 다운로드받을 수 있는 Scraper가 내장되어 있습니다.
`scrapers` 서브모듈의 `_scraper.py` 항목에는 Scraper 기본 클래스에 대한 정의가, `_helpers.py`에는 Scraper를 구동하기 위한 다양한 도움 함수가 클래스가, `_callback_manager.py`에는 Scraper에서 사용되는 Callback 관리 도구가, `_naver_webtoon.py`에는 네이버 웹툰에 대한 스크래퍼 구현이 들어있습니다.

`__main__.py`에는 WebtoonScraper의 CLI 환경을 구성합니다. 이를 통해 WebtoonScraper의 CLI 환경을 사용할 수 있습니다.

## Scraper가 작동하는 방식

WebtoonScraper의 알파이자 오메가는 바로 Scraper 함수입니다. 이 Scraper 함수를 상속해 다양한 플랫폼의 스크래퍼를 제작하게 됩니다.

왜 composition이 아니라 상속을 사용하는지 궁금하실 수도 있습니다. 그 이유는 웹툰 플랫폼마다 정보를 불러오는 방식은 대체로는 비슷하지만 특정 아주 특이한 웹툰 플랫폼들의 경우에는 별도의 구현을 붙여야 하는데, 이렇게 '거의 대부분은 같은 속성을 공유하지만 아주 특이한 경우에 특이한 구현을 덧붙여야 하는 경우, 일단 일반적인 경우를 Scraper의 기본 구현으로 두고, 특이한 구현이 필요한 경우에만 서브클래스에서 override하는 것이 훨씬 간편하기 때문입니다.

그러나 WebtoonScraper도 적극적으로 composition을 이용해 상속의 대안으로서 코드를 작성하는 방향으로 점진적으로 나아가고 있습니다. 사실상 웹툰 플랫폼과 적극적으로 상호작용하는 코드가 아니라면 composition을 통해 코드 구조를 조금 더 덜 엉킨 형태로 구성할 수 있기 때문입니다. 실제로 CallbackManager는 별도의 구현체가 아니라 Scraper 내부에 메소드로서 존재했지만, 현재는 코드에서 분리되어 콜백만을 관리하는 코드로 발전하게 되었습니다.

## 자신만의 Scraper를 구현하는 방법

Scraper는 몇 개의 추상 메서드와 속성이 존재합니다. 여기에서 설명하는 것들을 구현하면 스크래퍼의 최소 사양을 구현되는 것입니다. 물론 보통은 여기에 더해 다양한 플랫폼 한정적인 구현이 덧붙여지는 경우가 많습니다.

`Scraper.PLATFORM`은 해당 플랫폼의 구분자가 됩니다. 이 이름은 해당 스크래퍼가 어떤 플랫폼을 다운로드하는지 결정합니다. 

`Scraper._extract_webtoon_id`는 url로부터 웹툰 id를 추출합니다. 이 메서드가 구현이 되어야 CLI 환경에서 제대로 구현이 될 수 있습니다.

`Scraper.fetch_webtoon_information`과 `Scraper.fetch_episode_information`은 각각 웹툰 자체에 대한 정보와 웹툰 에피소드에 대한 정보를 Scraper에 저장합니다.
단, 에피소드를 정보를 불러오는 과정이 에피소드를 불러오는 과정과 분리되기 어렵다면 `Scraper.fetch_webtoon_information`에서 `UseFetchEpisode` exception을 올리도록 하고 `fetch_episode_information`을 사용하도록 할 수 있습니다.

`Scraper.get_episode_image_urls`에서는 특정 에피소드가 주어졌을 때 해당 에피소드의 이미지 URL 리스트를 리턴합니다. 이 이미지 리스트에서 다운로드한 이미지들이 웹툰 디렉토리를 구성합니다.

이론적으로는 위의 다섯 개의 메서드만 완성시켜도 작동합니다. 그러나 보통은 플랫폼 한정적인 사양이 있어 그에 맞추어 베이스 Scraper의 구현의 일부를 변경하는 것이 보통입니다.
