<template>
  <q-layout view="lHr lpR fFf">
    <q-header bordered class="bg-white text-black">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bold">
          <span class="gt-sm">{{ $route.name }}</span>
          <q-icon
            class="header-icon q-pa-md lt-md"
            name="fa-solid fa-dove"
            size="sm"
            color="primary"
          />
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      show-if-above
      v-model="leftDrawerOpen"
      :width="283"
      side="left"
      bordered
    >
      <q-icon
        class="q-pa-md"
        name="fa-solid fa-dove"
        size="lg"
        color="primary"
      />
      <q-list>
        <q-item to="/" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="home" size="md" />
          </q-item-section>
          <q-item-section class="text-h6 text-weight-bold">홈</q-item-section>
        </q-item>

        <q-item to="/About" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="help" size="md" />
          </q-item-section>
          <q-item-section class="text-h6 text-weight-bold">소개</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <q-input placeholder="검색하기" class="q-ma-md" outlined rounded dense>
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>

      <q-list separator padding>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">국제</q-item-label>
            <q-item-label class="text-weight-bold text-ellipsis"
              >후쿠시마 오염수 방류</q-item-label
            >
            <q-item-label caption>
              일본 정부가 올여름 오염수 해양 방류를 강행한다는 입장을
              보여왔습니다. IAEA 조사단은 포괄적 검증을 마쳤고, 최종 보고서를
              공개할 계획이라고 합니다.
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5분전</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">정치</q-item-label>
            <q-item-label class="text-weight-bold text-ellipsis"
              >남북 관계와 한반도 정세
            </q-item-label>
            <q-item-label caption>
              북한이 5월 31일 오전 기습 발사한 우주 발사체가 비정상 비행 도중
              서해 먼바다에 떨어졌습니다. 군은 발사체 잔해를 수거해 분석에
              들어갔습니다.
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>10분전</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">스포츠</q-item-label>
            <q-item-label class="text-weight-bold text-ellipsis"
              >2023 FIFA U-20 월드컵
            </q-item-label>
            <q-item-label caption>
              한국 축구가 3회 연속 국제축구연맹(FIFA) U-20 월드컵 3회 연속 16강
              진출에 성공하며 '어게인 2019'를 향한 힘찬 발걸음을 이어갔습니다.
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>15분전</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const rightDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
    };
  },
};
</script>

<style lang="sass">
.header-icon
  position: absolute
  bottom: 0
  left: 50%
  transform: translateX(-50%)

.text-ellipsis
  overflow: hidden
  text-overflow: ellipsis
  white-space: nowrap
</style>
