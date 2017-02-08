<template>
  <div class="hello">

    <lz-button loading="true"  type="primary" :onClick="bc"><span>adadfa1243</span>adfad</lz-button>

    <lz-button-group>
      <lz-button loading="true"   type="primary" :onClick="bc">1</lz-button>
      <lz-button type="primary">
            <span>Forward</span><Icon type="right" />
        </lz-button>
    </lz-button-group>
  </div>
</template>

<script>

import Button from './button';
import Icon from './icon';

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components:{
    'lz-button': Button,
    'lz-button-group': Button.Group,
    Icon: Icon
  },
  methods: {
    bc(){
      console.log("bc");
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
