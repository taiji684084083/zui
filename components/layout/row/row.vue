<template>
  <component :is="tag" :class="['z-row' , classList]" :style="addStyle">
    <slot></slot>
  </component>
</template>

<script>
export default {
  name: "zRow",
  props: {
    tag: {
      type: String,
      default: "div"
    },
    gutter: Number,
    type: String,
    justify: {
      type: String,
      default: "start"
    },
    algin: {
      type: String,
      default: "top"
    }
  },
  computed: {
      classList(){
          const arr = [];
          // 添加flex布局
          if(this.type == 'flex'){
              arr.push('z-row-flex');
          }
          // 横向排列
          if(this.justify !== 'start'){
              arr.push(`is-justify-${this.justify}`);
          }
          // 纵向排列
          if(this.algin !== 'top'){
              arr.push(`is-justify-${this.algin}`)
          }
          return arr;
      },
      addStyle(){
          const style = {};
          // 设置分栏间隔
          if(this.gutter){
              style.marginLeft = this.gutter / 2 + 'px';
              style.marginRight = style.marginLeft;
          }
          return style;
      }
  }
};
</script>

<style lang="scss" scoped>
@import "../../../style/mixin.scss";

@include b(row) {
  position: relative;
  box-sizing: border-box;
  @include clear();
  // background: red;

  @include m(flex){
      display: flex;    
      &:before,&:after{
        display: none;
      }
      
      @include when(justify-center){
          justify-content: center;
      }

      @include when(justify-end){
          justify-content: flex-end;
      }

      @include when(justify-space-between){
          justify-content: space-between;
      }

      @include when(justify-space-around){
          justify-content: space-around;
      }

      @include when(align-enter){
          align-items: center;
      }

      @include when(align-end){
          align-items:flex-end;
      }

  }
}
</style>