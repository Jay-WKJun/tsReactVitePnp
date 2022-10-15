# TypeScript + React with Vite & Yarn pnp

The Boilerplate with TypeScript + React + Vite + Yarn pnp

## tsconfig

noImplicitAny: any를 설정시, 해당 변수의 타입이 모호해지기 때문에 정적 타입을 명확하게 해주는 TypeScript의 장점이 없어지게 됨으로 any 타입은 하지 않는 것으로 설정했습니다!

strictNullChecks: null이나 undefined는 엄연히 다른 정의를 가지고 있기 때문에 명확한게 좋다고 생각합니다.

noFallthroughCasesInSwitch: switch문에서 만약 break나 return이 없다면 분명 의도와는 확연히 다른 코드가 나올 것입니다. 따라서 실수 방지를 위해 설정했습니다.

noImplicitReturns: 함수의 Type을 명확하고 철저하게 하기 위해서 설정했습니다.

noImplicitThis: 헷갈릴 수 있는 this를 막고자 설정했습니다.

noPropertyAccessFromIndexSignature: 변수인 [key]를 설정했다면, 불러올 때에도 변수를 통해서 불러오게 해야한다고 생각합니다.

noUncheckedIndexedAccess: 원래는 변수 [key]를 불러오면 해당 value의 type이 변수에 설정되었는데, [key]는 있을 수도 없을 수도 있기 때문에 undefined, 또한 함께 type 반환을 시켜줄 수 있도록 해당 옵션을 설정합니다.

noUnusedLocals: 쓸데없는 변수가 있어서는 안된다고 생각합니다. 이건 메모리 낭비 및 코드 낭비입니다. 😱

noUnusedParameters: 쓸데없는 파라미터 또한, 메모리 낭비 및 코드 낭비! 방지용 입니다.

Dev용 config
sourceMap: 난독화 되는 코드를 막아줘서 브라우저에서도 디버깅할 수 있게 해줍니다.

extendedDiagnostics: compile시에 시간이 얼마나 걸리는지 측정해주는 option입니다.

## editorConfig

> editorConfig는 project내의 텍스트 파일들의 포맷들을 맞춰줍니다.

특정 언어, 에디터, 프레임워크에 구애받지 않고 모든 곳에서 사용할 수 있기 때문에 매우 유용합니다.

아래와 같은 문제를 해결합니다.

- tab과 space를 섞어쓰는 문제
- line Ending을 섞어쓰는 문제 (git에서는 큰 문제가 되지 않습니다.)
- 문자 encoding이 맞지 않는 문제
- 여러 indenting 포맷의 문제
- 등등... text format이 맞지 않는 문제

### refs

https://www.freecodecamp.org/news/how-to-use-editorconfig-to-standardize-code-styles/

## eslintrc

eslint 설정

### babel

vite는 기본적으로 import.meta, 즉 esm을 지원하는 브라우저에서만 작동하도록 빌드합니다.

[@vitejs/plugin-legacy](https://github.com/vitejs/vite/tree/main/packages/plugin-legacy)를 통해 해결할 수 있다고 하여, 별도의 babel은 셋팅하지 않는 것으로 판단했습니다.

[Vite - browser compatibility](https://vitejs.dev/guide/build.html#browser-compatibility)

### plugin과 extension

plugin은 eslint에서 따로 제공하지않는 custom rule을 주입할 수 있는 것이고 extension은 미리 작성된 eslintrc를 확장해서 사용한다는 의미입니다.

[difference-between-eslint-extends-and-plugins](https://prateeksurana.me/blog/difference-between-eslint-extends-and-plugins/)

## prettier

prettier의 옵션들은 모두 eslint에서 가능합니다.

이러한 설정의 중복은 관리 소요를 더 크게 한다고 생각하여, prettier의 auto formatting이 아닌, eslint --fix를 save시에 발동하는 방법으로 auto formatting을 설정하려고 합니다.
