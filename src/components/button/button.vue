<!-- import * as React from 'react';
import classNames from 'classnames';
import { findDOMNode } from 'react-dom';
import Icon from '../icon';
import splitObject from '../_util/splitObject';
const rxTwoCNChar = /^[\u4e00-\u9fa5]{2}$/;
const isTwoCNChar = rxTwoCNChar.test.bind(rxTwoCNChar);
function isString(str) {
  return typeof str === 'string';
}

// Insert one space between two chinese characters automatically.
function insertSpace(child) {
  if (isString(child.type) && isTwoCNChar(child.props.children)) {
    return React.cloneElement(child, {},
                              child.props.children.split('').join(' '));
  }
  if (isString(child)) {
    if (isTwoCNChar(child)) {
      child = child.split('').join(' ');
    }
    return <span>{child}</span>;
  }
  return child;
}

type ButtonType = 'primary' | 'ghost' | 'dashed'
type ButtonShape = 'circle' | 'circle-outline'
type ButtonSize = 'small' | 'large'

interface ButtonProps {
  type?: ButtonType;
  htmlType?: string;
  icon?: string;
  shape?: ButtonShape;
  size?: ButtonSize;
  onClick?: React.FormEventHandler;
  loading?: boolean;
  disabled?: boolean;
  style?: React.CSSProperties;
  prefixCls?: string;
}

export default class Button extends React.Component<ButtonProps, any> {
  static Group: any;

  static defaultProps = {
    prefixCls: 'ant-btn',
    onClick() {},
    loading: false,
  };

  static propTypes = {
    type: React.PropTypes.string,
    shape: React.PropTypes.oneOf(['circle', 'circle-outline']),
    size: React.PropTypes.oneOf(['large', 'default', 'small']),
    htmlType: React.PropTypes.oneOf(['submit', 'button', 'reset']),
    onClick: React.PropTypes.func,
    loading: React.PropTypes.bool,
    className: React.PropTypes.string,
    icon: React.PropTypes.string,
  };

  timeout: any;
  clickedTimeout: any;

  componentWillUnmount() {
    if (this.clickedTimeout) {
      clearTimeout(this.clickedTimeout);
    }
    if (this.timeout) {
      clearTimeout(this.timeout);
    }
  }

  clearButton = (button) => {
    button.className = button.className.replace(` ${this.props.prefixCls}-clicked`, '');
  }

  handleClick = (e) => {
    // Add click effect
    const buttonNode = findDOMNode(this);
    this.clearButton(buttonNode);
    this.clickedTimeout = setTimeout(() => buttonNode.className += ` ${this.props.prefixCls}-clicked`, 10);
    clearTimeout(this.timeout);
    this.timeout = setTimeout(() => this.clearButton(buttonNode), 500);

    this.props.onClick(e);
  }

  // Handle auto focus when click button in Chrome
  handleMouseUp = (e) => {
    (findDOMNode(this) as HTMLElement).blur();
    if (this.props.onMouseUp) {
      this.props.onMouseUp(e);
    }
  }

  render() {
    const props = this.props;
    const [{ type, shape, size, className, htmlType, children, icon, loading, prefixCls }, others] = splitObject(props,
      ['type', 'shape', 'size', 'className', 'htmlType', 'children', 'icon', 'loading', 'prefixCls']);

    // large => lg
    // small => sm
    const sizeCls = ({
      large: 'lg',
      small: 'sm',
    })[size] || '';

    const classes = classNames({
      [prefixCls]: true,
      [`${prefixCls}-${type}`]: type,
      [`${prefixCls}-${shape}`]: shape,
      [`${prefixCls}-${sizeCls}`]: sizeCls,
      [`${prefixCls}-icon-only`]: !children && icon,
      [`${prefixCls}-loading`]: loading,
      [className]: className,
    });

    const iconType = loading ? 'loading' : icon;

    const kids = React.Children.map(children, insertSpace);

    return (
      <button {...others}
        type={htmlType || 'button'}
        className={classes}
        onMouseUp={this.handleMouseUp}
        onClick={this.handleClick}
      >
        {iconType ? <Icon type={iconType} /> : null}{kids}
      </button>
    );
  }
} -->

<template>
  <button
    :class="classes"
    @MouseUp="handleMouseUp"
    @click="handleClick"
  >
  <Icon :type="iconType" v-if="iconType" />
  <slot></slot>
  </button>
</template>

<script>

import './style'
import Icon from "../icon"

const prefixCls = 'ant-btn';

export default{
  created(){
    // console.log(this);
  },
  props: {
    type: '',
    shape: '',
    size: '',
    htmlType: '',
    onClick: null,
    loading: false,
    className: '',
    icon: '',
    onMouseUp: null
  },
  data () {
    return {
      clicked: false,
      timeout: null
    }
  },
  methods: {
    handleClick(e){
      // Add click effect
      // const buttonNode = findDOMNode(this);
      // this.clearButton(buttonNode);
      this.clicked = false;
      this.clickedTimeout = setTimeout(() => this.clicked = true , 10);
      clearTimeout(this.timeout);
      this.timeout = setTimeout(() => this.clicked = false, 500);
      //
      typeof this.onClick === 'function' && this.onClick(e);
    },

    // Handle auto focus when click button in Chrome
    handleMouseUp(e){
      // (findDOMNode(this) as HTMLElement).blur();
      if (this.props.onMouseUp) {
        this.props.onMouseUp(e);
      }
    }
  },
  computed: {
    classes(){
      // large => lg
      // small => sm
      const sizeCls = ({
        large: 'lg',
        small: 'sm',
      })[this.size] || '';

      let className = {
        [prefixCls]: true,
        [`${prefixCls}-${this.type}`]: this.type,
        [`${prefixCls}-${this.shape}`]: this.shape,
        [`${prefixCls}-${sizeCls}`]: sizeCls,
        [`${prefixCls}-icon-only`]: !this.children && this.icon,
        [`${prefixCls}-loading`]: this.loading,
        [this.className]: this.className,
        [`${prefixCls}-clicked`] : this.clicked
      }

      return className;
    },
    iconType(){
      return this.loading ? 'loading' : this.icon;
    }
  },
  components: {
    Icon: Icon
  }
}
</script>
