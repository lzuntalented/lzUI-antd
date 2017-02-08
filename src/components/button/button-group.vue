<!-- import * as React from 'react';
import classNames from 'classnames';
import splitObject from '../_util/splitObject';

const prefix = 'ant-btn-group-';

type ButtonSize = 'small' | 'large'

interface ButtonGroupProps {
  size?: ButtonSize;
  style?: React.CSSProperties;
  className?: string;
}

export default function ButtonGroup(props: ButtonGroupProps) {
  const [{ size, className }, others] = splitObject(props, ['size', 'className']);

  // large => lg
  // small => sm
  const sizeCls = ({
    large: 'lg',
    small: 'sm',
  })[size] || '';

  const classes = classNames({
    'ant-btn-group': true,
    [prefix + sizeCls]: sizeCls,
    [className]: className,
  });

  return <div {...others} className={classes} />;
} -->
<template>
  <div
  :class="classes" >
  <slot></slot>
</div>
</template>

<script>

import './style'

const prefixCls = 'ant-btn-group-';

export default{
  props: {
    size: '',
    className: '',
  },
  data () {
    return {
      clicked: false,
      timeout: null
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
        [prefixCls + sizeCls]: sizeCls,
        [this.className]: this.className,
      }

      return className;
    }
  }
}
</script>
