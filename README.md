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

따라서 module을 지원하지 않는 브라우저에서도 코드가 작동할 수 있도록 변환해주는 babel이 적용되어 있지 않습니다.

[@vitejs/plugin-legacy](https://github.com/vitejs/vite/tree/main/packages/plugin-legacy)를 통해 해결할 수 있다고 합니다.

[Vite - browser compatibility](https://vitejs.dev/guide/build.html#browser-compatibility)

- esbuild의 한계

vite에서 babel은 [@vitejs/plugin-react](https://www.npmjs.com/package/@vitejs/plugin-react)를 통해 build시에만 babel을 사용하고 있습니다.

dev시에는 매우 빠른 ESbuild를 사용하는데, ESbuild는 아직 시험단계이어서 class instance나 Decorator같은 기능을 사용하지 못합니다.

[vite-plugin-babel](https://www.npmjs.com/package/vite-plugin-babel)이 해결해 줄 수 있지만, ESbuild의 속도를 늦출 수 있어 정말 필요할 때만 사용하라고 권고하고 있습니다.

### plugin과 extension

plugin은 eslint에서 따로 제공하지않는 custom rule을 주입할 수 있는 것이고 extension은 미리 작성된 eslintrc를 확장해서 사용한다는 의미입니다.

[difference-between-eslint-extends-and-plugins](https://prateeksurana.me/blog/difference-between-eslint-extends-and-plugins/)

## prettier

prettier의 옵션들은 모두 eslint에서 가능합니다. **따라서 따로 설정하지 않았습니다.**

이러한 설정의 중복은 관리 소요를 더 크게 한다고 생각하여, prettier의 auto formatting이 아닌, eslint --fix를 save시에 발동하는 방법으로 auto formatting을 설정하려고 합니다.

# commit

commit 관련 규칙과 도구들입니다.

## [husky](https://typicode.github.io/husky/#/)

git hook을 편하게 쓸 수 있도록 도와줍니다.

git에서 어떤 action이 일어날 때, 그 action의 전과 후 처리를 합니다.

husky 혼자선 아무것도 못하지만, 여러 도구들을 husky hook에 넣어둠으로서 제 기능을 합니다!

보통 shell script로 hook을 작성하지만, Node 환경의 JS 코드로도 hook을 작성할 수 있다고 합니다!

### refs

https://library.gabia.com/contents/8492/

## [commitLint](https://commitlint.js.org/#/)

협업할 때에 commit message의 형식이 모두 제각각이라면, commit history 파악이 쉽지 않을 것 입니다.

commitLint로 여러 사람들의 commit message의 형식을 통일할 수 있습니다.

여러가지 commit message 형식이 있지만, 그 중 가장 유명한 것은 [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0/) 입니다.

### refs

https://blog.flynnpark.dev/m/13

## [lint-staged](https://www.npmjs.com/package/lint-staged)

git에서 staged된 파일만을 골라 eslint 등의 command를 실행시킬 수 있는 tool입니다.

- lint-stared가 필요한 이유

개발을 하다 보면, eslint server가 잘못된 것을 알려주지만, 그것을 알아차리지 못한 채, 잘못된 코드가 commit될 수 있습니다.

그 코드를 바꾸기 위해 오타같은 아주 사소한 commit이 끼어들어가게 되는데 이는 commit history 관리 면에서 바람직하지 못합니다.

하지만 lint-staged + husky를 통해 commit전에 변경된 코드를 확인할 수 있다면, 이런 사소한 commit history를 남길일이 없어질 것입니다!

- 한정된 lint 범위

매 commit마다 모든 파일에 eslint를 실행하면 굉장히 오래걸릴 것입니다.

하지만, lint-staged를 통해 정확히 필요한 파일에만 lint를 적용할 수 있습니다.

### refs.

https://www.huskyhoochu.com/how-to-use-lint-staged/
