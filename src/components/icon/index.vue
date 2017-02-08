
<template>
  <i
  :class="classes"
  />
</template>
<script>
import './style'

export default {
  props: {
    type: "",
    className: ""
  },
  computed:{
    classes(){
      let result = {
        ["anticon"]: true,
        [`anticon-${this.type}`]: this.type,
        [this.className] : this.className
      }
      return result;
    }
  }
}

</script>
