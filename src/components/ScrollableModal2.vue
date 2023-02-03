<template>
  <div
    v-show="value"
    class="scrollable-modal"
  >
    <div
      class="scrollable-modal__overlay"
      @click="close"
    >
      <div
        class="scrollable-modal__content-wrapper"
        @click.stop
      >
        <div class="modal-content">
            <div class="modal-content__header">
              <span class="modal-content__title">スクロール可能モーダル(overscroll-behavior版)</span>
            </div>
            <div class="modal-content__body">
              <div class="item-container">
                <span
                  v-for="(item, index) in items"
                  class="item-container__item"
                  :key="index"
                >{{ item }}</span>
              </div>
            </div>
            <div class="modal-content__footer">
              <button @click="close">閉じる</button>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ScrollableModal2',
  props: {
    value: { type: Boolean, default: false }
  },
  data () {
    return {
      items: [...Array(100)].map((_, index) => `item-${index}`)
    }
  },
  methods: {
    close () {
      this.$emit('input', false)
    }
  }
}
</script>

<style scoped lang="scss">
%no-scroll-bar {
  /*スクロールバー非表示（IE・Edge）*/
  -ms-overflow-style: none;
  /*スクロールバー非表示（Firefox）*/
  scrollbar-width: none;
  /*スクロールバー非表示（Chrome・Safari）*/
  &::-webkit-scrollbar{
    display:none;
  }
}

.scrollable-modal {
  &__overlay {
    position: fixed;
    inset: 0;
    background-color: rgba(0, 0, 0, 0.5);
    overflow-y: scroll;
    overscroll-behavior: none;
    @extend %no-scroll-bar;
    &:after {
      content: '';
      display: block;
      height: calc(100% + 1px);
    }
  }
  &__content-wrapper {
    position: fixed;
    inset: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    // スクロールイベント
    pointer-events: none;
    & > * {
      pointer-events: auto;
    }
  }
}

.modal-content {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  width: 500px;
  height: 300px;
  background-color: #ffffff;
  overflow-y: auto;
  overscroll-behavior: none;
  @extend %no-scroll-bar;
  &__header {
    position: sticky;
    top: 0;
    left: 0;
    background-color: #cccccc;
    padding: 10px;
  }
  &__body {
    flex-grow: 1;
    padding: 10px;
  }
  &__footer {
    position: sticky;
    bottom: 0;
    left: 0;
    border-top: 1px solid #cccccc;
    padding: 10px;
    background-color: #ffffff;
  }
  &__title {
    font-weight: bold;
  }
}

.item-container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  gap: 20px;
  &__item {
    display: inline-block;
    padding: 10px;
    background-color: lightblue;
    font-weight: bold;
  }
}
</style>
