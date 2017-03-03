<template>
    <div
      v-if="closing"
      :class="alertCls"
    >
      <Icon class="ant-alert-icon" :type="leftType" v-if="showIcon" />
      <span :class="`${prefixCls}-message`">{{message}}</span>
      <span :class="`${prefixCls}-description`">{{description}}</span>
      <a v-if="closable" @click="handleClose" :class="`${prefixCls}-close-icon`">
         <Icon v-if="closeText" type="cross" />
      </a>
    </div>
</template>

<script>
import './style';
import Icon from "../icon";

let defaultProps = {
  prefixCls: {
    default:'ant-alert'
  },
  showIcon: {
    default:false
  },
  onClose: {
    default: null
  },
  type:{
    default:
     'info'
   },
   message:{
     default: ''
   },
   description:{
     default: ''
   }
};

export default {
  props: defaultProps,
  data(){
    return {
      closing: true,
      closed: false,
      closable: true,
      closeText: true,
    }
  },
  methods: {
    handleClose (e){
      this.closing = false;
      typeof this.onClose === "function" && this.onClose(e);
    }
  },
  computed:{
    alertCls(){
      // use outline icon in alert with description
      let description = false;
      let showIcon = false;

      let alertCls = {
        [this.prefixCls]: true,
        [`${this.prefixCls}-${this.type}`]: true,
        [`${this.prefixCls}-close`]: !this.closing,
        [`${this.prefixCls}-with-description`]: !!description,
        [`${this.prefixCls}-no-icon`]: !showIcon,
      };
      return alertCls;
    },
    leftType(){
      let iconType = '';
      switch (this.type) {
        case 'success':
          iconType = 'check-circle';
          break;
        case 'info':
          iconType = 'info-circle';
          break;
        case 'error':
          iconType = 'cross-circle';
          break;
        case 'warning':
          iconType = 'exclamation-circle';
          break;
        default:
          iconType = 'default';
      }
      return iconType;
    }
  },
  components: {
    Icon: Icon
  }
}
</script>
