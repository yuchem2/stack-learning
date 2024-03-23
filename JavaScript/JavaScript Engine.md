## What is JavaScript Engine
스크립트를 실행하는 소프트웨어 구성 요소입니다. 최초의 JS engine은 단순한 interpreter였지만 최신 JS engine은 성능 향상을 위해 just-in-time compliation를 사용합니다.

일반적으로 웹 브라우저 공급업체에서 개발하고 있으며 모든 주요 브라우저에 존재합니다. 이러한 엔진의 사용은 브라우저 뿐만 아니라 Node.js 등에서도 사용될 수 있습니다. 
## Notable Engine
+ Google의 V8: 가장 많이 사용되는 JS engine입니다. Google Chrome 및 Chromium 기반 브라우저에서 사용되며 Node.js 및 Deno runtime system에서도 사용됩니다.
+ Mozilla의 SpiderMonkey: Firefox 및 Mozilla의 fork에서 사용되기 위해 작성되었습니다. 
+ JavaScriptCore: Apple의 Safari 브라우저 용 엔진으로, Webkit 기반 브라우저와 Bun runtime system에서도 사용됩니다.
+ Chakra: 원래 Internet Explorer의 엔진이었습니다. Microsoft의 Edge에도 사용되었지만 현재 Edge는 Chrominum 기반 브라우저로 다시 구성되어 V8을 사용하고 있습니다.
## Simple pipeline
동작 기본 원리는 다음과 같습니다.
1. 엔진이 스크립트를 읽습니다.(파싱)
2. 읽어 들인 스크립트를 기계어로 전환합니다.(컴파일)
3. 기계어로 전환된 코드가 실행됩니다. 기계어로 전환되었기 때문에 실행 속도가 빠릅니다.

엔진은 프로세스 각 단계마다 최적화를 진행합니다. 컴파일이 끝나고 실행 중인 코드를 감시하면서 흘러가는 데이터를 분석하고, 분석 결과를 토대로 기계어로 전환된 코드를 다시 최적화하기도 합니다. 
## 출처
+ https://en.wikipedia.org/wiki/JavaScript_engine
+ https://ko.javascript.info/intro
+ 

