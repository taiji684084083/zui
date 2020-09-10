<template>
  <component :is="tag" :style="insertStyle" class="z-col" :class="[classList_grid,classList_adaptive]">
    <slot></slot>
  </component>
</template>

<script>
export default {
  name: "zCol",
  props: {
    tag: {
      type: String,
      default: "div"
    },
    span: {
      type: Number,
      default: 24
    },
    offset: Number,
    push: Number,
    pull: Number,
    xs: [Number, Object],
    sm: [Number, Object],
    md: [Number, Object],
    lg: [Number, Object],
    xl: [Number, Object]
  },
  computed: {
    //设置分栏间隔
    insertStyle() {
      const style = {};
      let parent = this.$parent;
      while( parent && parent.$vnode && parent.$vnode.tag.indexOf("elRow") == -1){
        parent = parent.$parent;
      }
      if(parent && parent.gutter) {
        style.paddingLeft = parent.gutter / 2 + "px";
        style.paddingRight = style.paddingLeft;
      }
      return style;
    },
    //设置宽度和偏移量
    classList_grid() {
      const list = [];
      if (this.span || this.span == 0) {
        list.push(`z-col-span-${this.span}`);
      }
      if (this.offset || this.offset == 0) {
        list.push(`z-col-offset-${this.offset}`);
      }
      if (this.push || this.push == 0) {
        list.push(`z-col-push-${this.push}`);
      }
      if (this.push || this.pull == 0) {
        list.push(`z-col-pull-${this.pull}`);
      }
      return list;
    },
    //添加自适应class
    classList_adaptive() {
      const list = [];

      ["xs", "sm", "md", "lg", "xl"].forEach(prop => {
        if (typeof this[prop] == "number") {//props中传递的是数字

          list.push(`z-col-${prop}-${this[prop]}`);

        } else if (typeof this[prop] == "object") {//props传递的是对象
         
          //将对象转成数组keys
          //keys里面可能包含 span offset push pull
          const keys = Object.keys(this[prop]);
          keys.forEach(ele => {
            list.push(`z-col-${prop}-${ele}-${this[prop][ele]}`);
          });

        }
      });

      return list;

    }
  }
};
</script>

<style lang="scss" scoped>
@import "../../../style/mixin.scss";

//分栏布局
.z-col{
    float: left;
    box-sizing: border-box;
}
.z-col-0{
    display: none;
}
@for $i from 0 through 24{
    .z-col-span-#{$i}{
        width:(1 / 24 * $i) * 100%;
    }
    .z-col-offset-#{$i}{
        margin-left: (1 / 24 * $i) * 100%;
    }
    .z-col-push-#{$i}{
        position: relative;
        right: (1 / 24 * $i) * 100%;
    }
    .z-col-pull-#{$i}{
        position: relative;
        left: (1 / 24 * $i) * 100%;
    }
}

//响应分栏布局
$res-list:'xs','sm','md','lg','xl';
@each $unit in $res-list{
    @include res($unit){
        .z-col-xs-span-0{
            display: none;
        }
        @for $i from 0 through 24{
            .z-col-#{$unit}-span-#{$i}{
                width:(1 / 24 * $i ) * 100%;
            }
            .z-col-#{$unit}-offset-#{$i}{
                margin-left:(1 / 24 * $i) * 100%;
            }
            .z-col-#{$unit}-push-#{$i}{
                position: relative;
                right:(1 / 24 * $i) * 100%;
            }
            .z-col-#{$unit}-pull-#{$i}{
                position: relative;
                left:(1 / 24 * $i) * 100%;
            }
        }
    }
}

.hidden {
    @each $break-point-name, $value in $--breakpoints-spec {
      &-#{$break-point-name} {
        @include res($break-point-name, $--breakpoints-spec) {
          display: none !important;
        }
      }
    }
}

</style>