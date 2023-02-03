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
            <span class="modal-content__title">スクロール可能モーダル(overflow: hidden版)</span>
          </div>
          <div class="modal-content__body">
            <div class="item-container">
              <span
                v-for="(item, index) in items"
                class="item-container__item"
                :key="index"
              >{{ item }}</span>
              <!-- <template v-for="(item, index) in items">
                <span :key="index">{{ item }}</span>
              </template> -->
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
  name: 'ScrollableModal',
  props: {
    value: { type: Boolean, default: false }
  },
  data () {
    return {
      items: [...Array(100)].map((_, index) => `item-${index}`)
    }
  },
  watch: {
    value () {
      this.updateBodyOverflow(this.value)
    }
  },
  created () {
    this.updateBodyOverflow(this.value)
  },
  methods: {
    updateBodyOverflow (hidden) {
      document.body.style.overflow = hidden ? 'hidden' : ''
    },
    close () {
      this.$emit('input', false)
    }
  }
}
</script>

<style scoped lang="scss">
.scrollable-modal__overlay {
  position: fixed;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
  // overflow-y: scroll;
  // overscroll-behavior: none;
  // &:after {
  //   content: '';
  //   display: block;
  //   height: calc(100% + 1px);
  // }
}
.scrollable-modal__content-wrapper {
  width: 500px;
  height: 300px;
}

.modal-content {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  height: 100%;
  background-color: #ffffff;
}
.modal-content__header {
  background-color: #cccccc;
  padding: 10px;
}
.modal-content__body {
  flex-grow: 1;
  overflow-y: auto;
  // overscroll-behavior: none;
}
.modal-content__footer {
  border-top: 1px solid #cccccc;
  padding: 10px;
}
.modal-content__title {
  font-weight: bold;
}

.item-container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  gap: 20px;
}
.item-container__item {
  display: inline-block;
  padding: 10px;
  background-color: lightblue;
  font-weight: bold;
}
</style>
