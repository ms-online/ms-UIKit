
<template>
    <button class="ui-btn" @click="onClickBtn"
        :class="[Shadow, {
            'ui-btn-long': long,
            'ui-btn-xsmall': xsmall,
            'ui-btn-small': small,
            'ui-btn-large': large,
            'ui-btn-xlarge': xlarge,
            'ui-btn-border': border,
            'ui-btn-dashed': dashed,
            'ui-btn-text': text,
            'ui-btn-tile': tile,
            'ui-btn-rounded': rounded,
            'ui-btn-circle': circle,
            'ui-btn-disabled': disabled,
        }]"
        :style="{
            '--color-tint': TintColor,
            '--color-title': TitleColor,
        }"
    >
        <slot>Button</slot>
    </button>
</template>


<script lang="ts">
import { Vue, Component, Emit, Prop, Mixins } from 'vue-property-decorator';
import UIShadow from './UIShadow.vue';

@Component
export default class UIButton extends Mixins(UIShadow) {

    /** 长按钮 */
    @Prop(Boolean) readonly long!: boolean;
    /** 大小 - 超小 */
    @Prop(Boolean) readonly xsmall!: boolean;
    /** 大小 - 小 */
    @Prop(Boolean) readonly small!: boolean;
    /** 大小 - 大 */
    @Prop(Boolean) readonly large!: boolean;
    /** 大小 - 超大 */
    @Prop(Boolean) readonly xlarge!: boolean;
    /** 样式 - 边框按钮 */
    @Prop(Boolean) readonly border!: boolean;
    /** 样式 - 边框按钮 - 虚线 */
    @Prop(Boolean) readonly dashed!: boolean;
    /** 样式 - 文本按钮 */
    @Prop(Boolean) readonly text!: boolean;
    /** 圆角半径 - 矩形 */
    @Prop(Boolean) readonly tile!: boolean;
    /** 圆角半径 - 半圆 */
    @Prop(Boolean) readonly rounded!: boolean;
    /** 圆角半径 - 圆形 */
    @Prop(Boolean) readonly circle!: boolean;
    /** 颜色 - 主色调 */
    @Prop(String) readonly color!: string;
    /** 颜色 - 标题 */
    @Prop(String) readonly titleColor!: string;
    /** 禁用 */
    @Prop(Boolean) readonly disabled!: boolean;

    /** Computed 属性 - 按钮主色调 */
    private get TintColor() {
        if (this.disabled) {
            if (this.border || this.text) {
                return '#C5C8CE';
            }
            return '#F5F5F5';
        }
        if (this.color) {
            return this.color;
        }
        return '#2D8CF0';
    }

    /** Computed 属性 - 标题颜色 */
    private get TitleColor() {
        if (this.disabled) {
            return '#C5C8CE';
        }
        if (this.titleColor) {
            return this.titleColor;
        }
        if (this.border || this.text) {
            return this.TintColor;
        }
        return '#17233D';
    }

    /** 向父组件发送 click 事件 */
    @Emit('click') emitClick(e: MouseEvent) { return }

    /** 响应按钮的点击事件 */
    private onClickBtn(e: MouseEvent) {
        if (!this.disabled) {
            this.emitClick(e);
        }
    }
}
</script>


<style lang="stylus" scope>
Resize(mW, h, pLR, fs)
    min-width mW
    height h
    padding 0 pLR
    font-size fs
    &.ui-btn-circle
        width @height
        min-width 0
        padding 0
.ui-btn
    Resize(64px, 36px, 16px, 0.875rem)
    border 0 solid var(--color-tint)
    border-radius 4px
    color var(--color-title)
    background-color var(--color-tint)
    font-weight 500
    letter-spacing 0.09em
    cursor pointer
    user-select none
    outline none
    &:not(.ui-btn-disabled):hover
        filter brightness(120%)
    &:not(.ui-btn-disabled):active
        filter brightness(80%)
.ui-btn-long
    width 100%
.ui-btn-xsmall
    Resize(36px, 20px, 9px, 0.625rem)
.ui-btn-small
    Resize(50px, 28px, 12px, 0.75rem)
.ui-btn-large
    Resize(78px, 44px, 19px, 0.875rem)
.ui-btn-xlarge
    Resize(92px, 52px, 23px, 1rem)
.ui-btn-border
    border-width 1px
.ui-btn-dashed
    border-style dashed
.ui-btn-text, .ui-btn-border
    background-color transparent
.ui-btn-tile
    border-radius 0
.ui-btn-rounded, .ui-btn-circle
    border-radius 1000px
.ui-btn-disabled
    cursor not-allowed
</style>
