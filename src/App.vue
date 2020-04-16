
<template>
    <div>
        <UIButton @click="sayHello" shadow="2"
            :long="long" :disabled="disabled"
            :xsmall="xsmall" :small="small" :large="large" :xlarge="xlarge"
            :border="border" :dashed="dashed" :text="text"
            :tile="tile" :rounded="rounded" :circle="circle"
        >点我鸭</UIButton>

        <div class="btn-group">
            <UIButton class="btn-ctrl" @click="relong">长按钮</UIButton>
            <UIButton class="btn-ctrl" @click="resize('xsmall')">超小</UIButton>
            <UIButton class="btn-ctrl" @click="resize('small')">小</UIButton>
            <UIButton class="btn-ctrl" @click="resize('normal')">正常</UIButton>
            <UIButton class="btn-ctrl" @click="resize('large')">大</UIButton>
            <UIButton class="btn-ctrl" @click="resize('xlarge')">超大</UIButton>
        </div>
        <div class="btn-group">
            <UIButton class="btn-ctrl" @click="reborder('normal')">正常</UIButton>
            <UIButton class="btn-ctrl" @click="reborder('border')">边框</UIButton>
            <UIButton class="btn-ctrl" @click="reborder('dashed')">虚线</UIButton>
            <UIButton class="btn-ctrl" @click="reborder('text')">文本按钮</UIButton>
        </div>
        <div class="btn-group">
            <UIButton class="btn-ctrl" @click="reradius('normal')">正常</UIButton>
            <UIButton class="btn-ctrl" @click="reradius('tile')">矩形</UIButton>
            <UIButton class="btn-ctrl" @click="reradius('rounded')">半圆</UIButton>
            <UIButton class="btn-ctrl" @click="reradius('circle')">圆形</UIButton>
        </div>
        <div class="btn-group">
            <UIButton class="btn-ctrl" @click="disable">禁用</UIButton>
        </div>
    </div>
</template>


<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import UIButton from '@/components/UIButton.vue';

@Component({
    components: {
        UIButton,
    },
})
export default class App extends Vue {

    private disabled = false;

    private disable() {
        this.disabled = !this.disabled;
    }

    private tile = false;
    private rounded = false;
    private circle = false;

    private reradius(name: string) {
        this.tile = false;
        this.rounded = false;
        this.circle = false;
        switch (name) {
            case 'tile':
                this.tile = true;
                break;
            case 'rounded':
                this.rounded = true;
                break;
            case 'circle':
                this.circle = true;
                break;
        }
    }

    private border = false;
    private dashed = false;
    private text = false;

    private reborder(name: string) {
        this.border = false;
        this.dashed = false;
        this.text = false;
        switch (name) {
            case 'border':
                this.border = true;
                break;
            case 'dashed':
                this.border = true;
                this.dashed = true;
                break;
            case 'text':
                this.text = true;
                break;
        }
    }

    private long = false;

    private relong() {
        this.long = !this.long;
    }

    private xsmall = false;
    private small = false;
    private large = false;
    private xlarge = false;

    private resize(name: string) {
        this.xsmall = false;
        this.small = false;
        this.large = false;
        this.xlarge = false;
        switch (name) {
            case 'xsmall':
                this.xsmall = true;
                break;
            case 'small':
                this.small = true;
                break;
            case 'large':
                this.large = true;
                break;
            case 'xlarge':
                this.xlarge = true;
                break;
        }
    }

    sayHello(e: MouseEvent) {
        console.log(e);
    }
}
</script>


<style lang="stylus">
html, body
    box-sizing border-box
    font-size 18px
    font-family "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif
*, ::before, ::after
    box-sizing inherit
    font-size inherit
    font-family inherit
.btn-group
    margin 6px auto
.btn-ctrl
    margin 0 4px
</style>
