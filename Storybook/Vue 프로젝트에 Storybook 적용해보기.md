## Vue 프로젝트에 Storybook 적용해보기

> https://www.learnstorybook.com/intro-to-storybook/vue/en/get-started/
>
> https://storybook.js.org/docs/vue/get-started/introduction
>
> 위 레퍼런스를 참고하여 작성한 글입니다.

React 프로젝트에 Storybook 적용기는 엄청 많고, 심지어 문서까지 한글로 되어 있는데 Vue 프로젝트에 적용하는 경우는 상대적으로 찾기 어려운 것 같다. 아쉽게 문서도 영어다 ㅎㅎ;;

최근 회사에서 새 프로젝트를 시작했고, 슬슬 UI컴포넌트를 만들 것 같은데Storybook을 도입하면 어떨까하여 간단하게 Storybook을 접해보려고 한다.

우선 내가 생각한 Storybook 도입의 장점은 다음과 같다.

1. 기본적으로 UI컴포넌트를 문서화해서 차후 유지 및 보수를 편하게 함. 
   - 처음 개발한 사람의 의도를 좀 더 명확하게 알 수 있음.

2. 현재 피그마를 통해 디자인을 전달받는데, 스토리북과 피그마의 연동이 가능함.
   - 스토리북 하나를 보면서 디자인과 실제 개발된 UI를 비교하면서 개발이 가능 (왔다 갔다 할 필요가 전혀 없음)
   - 피그마로는 동적인 부분이 표현이 안되는데, 스토리북을 통해서 동적인 부분에 대한 커뮤니케이션도 가능.

3. 독립적인 UI 플레이그라운드
   - 만약 환불 페이지의 ui를 고쳐야 한다면, 기존의 방식대로라면 매번 로그인을 하고 테스트를 위해서 테스트 할 물건을 구매하고, 환불 페이지로 들어가서 UI를 고쳐야 함. 스토리북을 사용하면 그런 방식없이 바로 환불 페이지의 UI를 고칠 수 있음.

### Let's Get Started!!

우선 Vue CLI를 이용해 프로젝트를 하나 만들어준다. 나는 Vue (v2.6.11) + Typescript(v3.9.3) + Composition API(v1.0.0-beta.19)가 적용된 프로젝트에 Storybook을 추가하려고 한다.

`npx -p @storybook/cli sb init` 명령어로 간단하게 Vue 프로젝트에 추가할 수 있고, `npm run storybook`으로 실행할 수 있다.

![](https://images.velog.io/images/harrycod/post/50298c33-635a-4513-ae1f-823752a736a8/%E1%84%89%E1%85%B3%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%84%87%E1%85%AE%E1%86%A8%20%E1%84%91%E1%85%A9%E1%86%AF%E1%84%83%E1%85%A5%20%E1%84%8E%E1%85%AE%E1%84%80%E1%85%A1.png)<img src="https://images.velog.io/images/harrycod/post/3ed9b701-4580-49dd-9e8c-dda81680630a/%E1%84%89%E1%85%B3%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%84%87%E1%85%AE%E1%86%A8%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20%E1%84%8E%E1%85%A9%E1%84%80%E1%85%B5%E1%84%92%E1%85%AA%E1%84%86%E1%85%A7%E1%86%AB.png" alt="drawing" width="650"/>

Storybook을 설치하면 `stories` 파일이 생성되고 기본적인 세팅이 완료된다. 오른쪽 사진은 `npm run storybook` 으로 실행했을 때 보이는 창이다. 기본 `localhost:6006` 으로 설정되어 있다.

우선 테스트를 진행하기에 앞서 CSS 파일은 삭제하고 Vue파일의 <style>태그로 이동시켰고, 합쳐진 Vue파일은 `components` 폴더로 옮겼다. stories파일은 그대로 두었다.

만약 `props`로 `size`, `label`, `backgroundColor`를 받는 Button.vue 컴포넌트가 있을 때, Button 컴포넌트를 import 해주고, 템플릿화 시킨다음 `small`,`medium`,`large` 로 구분하였다. 또 디자인은 Figma로 받기 때문에 `storybook-addon-designs` 를 설치해서 Figma와 연동시켰다.

```js
// Button.stories.js
import MyButton from "../components/UI/Button.vue";
import { withDesign } from "storybook-addon-designs";

export default {
  title: "Example/Button",
  component: MyButton,
  decorators: [withDesign],
  parameters: {
    design: {
      type: "figma",
      url:
        "https://www.figma.com/file/PmsloKhkpAkuhBYpxlUaK1/00_Design-System?node-id=1771%3A640",
    },
  },
};

const Template = (args, { argTypes }) => ({
  props: Object.keys(argTypes),
  components: { MyButton },
  template:
    "<MyButton :label='label' :size='size' :backgroundColor='backgroundColor' />",
});

export const Small = Template.bind({});
Small.args = {
  size: "small",
  label: "Button",
};

export const Medium = Template.bind({});
Medium.args = {
  size: "medium",
  label: "Button",
};

export const Large = Template.bind({});
Large.args = {
  size: "large",
  label: "Button",
};
```

이 상태에서 실행시키면 `addon` 에 디자인 탭이 추가되고, 적어준 Figma URI와 잘 연동되는 모습을 확인할 수 있다. 

![](https://images.velog.io/images/harrycod/post/aa177ace-4443-4b29-86a3-9c3a84728428/%E1%84%91%E1%85%B5%E1%84%80%E1%85%B3%E1%84%86%E1%85%A1.png)

문서도 별 다른 공수없이 잘 작성되었다.

![](https://images.velog.io/images/harrycod/post/41ad04b8-3738-4bae-9c04-e4277e7deb04/%E1%84%83%E1%85%A1%E1%86%A8%E1%84%89%E1%85%B3.png)

아주아주 간단하게 스토리북을 적용시켜봤다. 나는 Button이라는 UI컴포넌트 하나에만 적용했지만, 기능 플로우 혹은 페이지 단위로도 적용이 가능하다. 문서도 좀 더 예쁘고 깔끔하게 정리가 가능하다. 이 부분은 만약 실제 사용하게 된다면 찾아보면서 해봐야겠다.

적용하면서 가장 기대했던 부분은 UI컴포넌트 문서화 그리고 Figma와의 연동성이었는데, 우선 글쎄 UI컴포넌트 문서화가 정말 필요할까? 하는 의문이 들었고, Figma는 CSS를 참고하려고 했던 건데 스토리북에 연동된 Figma는 약간 미리보기 같은 느낌이라 CSS 속성을 확인하려면 다시 링크 페이지로 이동해야되서 생각보다 불편했던 것 같다.

그래서 도입해야할까 아닐까 잘 모르겠다 :(