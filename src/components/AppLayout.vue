<script setup>
import { useRoute, useRouter } from 'vue-router';
import { Back } from '@element-plus/icons-vue';
import { computed } from 'vue';
import { ROUTER_PATHS } from '../constants/router';

  const props = defineProps({
    imgUrl: {
      type: String,
      required: true
    },
    backFunc: {
      type: Function
    },
    isBackButtonVisible: {
      type: Boolean,
      default: true
    }
  });

  const route = useRoute();
  const router = useRouter();

  const routeName = computed(() => route.name);

  function goForCoctailRandom() {
    router.push(ROUTER_PATHS.COCKTAIL_RANDOM);

    if(routeName.value === ROUTER_PATHS.COCKTAIL_RANDOM) {
      router.go();
    }
  }

  function goBack() {
    props.backFunc ? props.backFunc() : router.go(-1)
  }
</script>

<template>
  <div class="root">
    <div :style="`background-image: url(${imgUrl})`" class="img"></div>
    <div class="main">
      <div class="btns">
        <el-button
        v-if="isBackButtonVisible"
          type="primary"
          :icon="Back"
          circle class="back"
          @click="goBack"
        />
        <el-button class="btn" @click="goForCoctailRandom">Get random cocktail</el-button>
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import '../assets/styles/main.scss';
.root {
  background-color: $background;
  display: flex;
  min-height: 100vh;
}

.img {
  width: 50%;
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-size: cover;
}

.main {
  position: relative;
  width: 50%;
  padding: 32px 40px;
}

.btn {
  position: absolute;
  top: 32px;
  right: 40px;
  font-size: 16px;
  font-family: 'Raleway';
  background-color: $accent;
  border-color: $accent;
  color: $text;

  &:hover,
  &:active {
    background-color: darken($accent, 20%);
    border-color: darken($accent, 20%);
  }
}

.btns {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.back {
  background-color: transparent;
  border-color: #fff;

  &:hover {
    border-color: $accent;
  }
}
</style>