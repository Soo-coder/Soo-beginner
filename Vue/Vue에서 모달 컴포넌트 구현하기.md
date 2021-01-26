## Vue.js 모달 컴포넌트 만들기

Vue 프로젝트 진행 중 모달 창을 구현해야할 일이 생겼다. 지난 번 프로젝트에서는 급히 기능을 구현하기 위해 `Vuetify` 를 사용했는데, 이번에는 직접 구현해봐야 겠다는 생각이 들어 이것저것 리서치를 해보다 Vue로 구현된 모달 창에서 `<template>` 이나 `<slot>` 혹은 `<transition>` 과 `enter/leave` 같은 생소한 태그나 개념을 접하게 되어서 공부해보고, 이를 컴포넌트화 해서 제작해 보았다.

구체적인 개념 설명 없이 바로 예제 코드로 들어갈 것이므로, 예제 코드에서 처음 보는 개념이나 태그에 관해서는 아래 공식 문서를 참조하길 바란다.

1. [transition 태그와enter/leave 개념](https://kr.vuejs.org/v2/guide/transitions.html)

2. [slot 과 template 태그](https://kr.vuejs.org/v2/guide/components-slots.html)



### 예제 코드

*주의 : 프로젝트에서 Vue 2.6.11, composition API + Typescript + SCSS 조합을 사용했고, 이에 관해서 별도로 설명하지 않음, 예제 코드는 각자 상황에 맞게 변형하여 이용*

상황 : `회원가입 페이지`에서 `광고 동의 버튼`을 누를 시에 약관 규정을 보여주는 모달 창을 구현

#### 구현 모습
![구현GIF](https://images.velog.io/images/harrycod/post/5c1dd2bc-8647-4197-b9c4-ee13121bfd16/%E1%84%86%E1%85%A9%E1%84%83%E1%85%A1%E1%86%AF%E1%84%8E%E1%85%A1%E1%86%BC%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB.gif)

#### 자식 컴포넌트(Modal.vue)

```vue
//Modal.vue
<template>
	// transition 문법은 상단 문서 참고
  <transition name="modal" appear>
    <section class="modal">
      <div class="modal__window">
        <div class="modal__title">
          <slot name="title" />
        </div>
        <div class="modal__content">
          <slot name="content" />
        </div>
        <div class="modal__footer">
          <slot name="footer" />
        </div>
      </div>
      <div class="modal__overlay" @click.self="$emit('close')"></div>
    </section>
  </transition>
</template>

<style lang="scss">
.modal {
  position: absolute;
  display: flex;
  width: 100%;
  height: 100%;
  align-items: center;
  justify-content: center;
  
  &__overlay {
    position: absolute;
    width: 100%;
    height: 100%;

    background-color: black;
    opacity: 0.8;
  }

  &__window {
    width: 30rem;
    height: 40rem;
    border-radius: 0.4rem;
    overflow: hidden;
    padding: 1rem;
    z-index: 1;

    background-color: white;
  }

  &__title {
  }

  &__content {
  }

  &__footer {
  }

	// 상황에 따라 transition 변경가능 enter,leave class는 상단 문서 참고
  &-enter,
  &-leave-to {
    opacity: 0;
    transition: opacity 0.4s ease;
  }

  &-enter-to,
  &-leave {
    transition: opacity 0.4s ease;
  }
}
</style>

```

#### 부모 컴포넌트(Signup.vue)

```vue
// Signup.vue
<template>
	<section>
    <!-- 
			광고수신 동의 체크박스
			BoxAgreement는 커스텀 컴포넌트로 동의 여부를 묻는 버튼 정도로 생각
		-->
    <BoxAgreement
      @click.native="controlModal(true)"
    />
    <!-- 
			광고 동의 모달 starts 
			상황에 따라 내용 변경가능, template 태그는 상단 문서 참고
		-->
    <Modal @close="controlModal(false)" v-if="isModalOpen">
      <!-- header slot starts -->
      <template #title>
        <div>타이틀</div>
      </template>

      <!-- content slot starts -->
      <template #content>
        <p>콘텐츠 내용</p>
      </template>

      <!-- footer slot starts -->
      <template #footer>
        <button @click="controlModal(false)">동의</button>
      </template>
    </Modal>

  </section>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/composition-api";
import BoxAgreement from "@/components/Elements/Agreement-Box.vue";
import Modal from "@/components/Elements/Modal.vue";
export default defineComponent({
  components: {
    BoxAgreement,
    Modal,
  },
  setup() {
    const marketingAgree = ref(false);
    const isModalOpen = ref(false);

    const controlModal = (state: boolean) => {
      isModalOpen.value = state;
    };

    return {
      marketingAgree,
      isModalOpen,
      controlModal,
    };
  },
});
</script>
```