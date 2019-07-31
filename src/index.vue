<template>
  <div class="component">
    <section class="comp_detail_1">
      <h1 :class='{titlePage: type == 4}' :style="{fontSize: info.titleFont + 'px', color: info.titleColor}">
        <span class='icon' v-if='type == 3' :style="{backgroundColor: info.iconColor}"></span>
        <span class="iconCenter" v-if='type == 4' :style="{backgroundColor: info.iconColor}"></span>
        <span class='content'>{{info.title}}</span>
        <span class="iconCenter" v-if='type == 4' :style="{backgroundColor: info.iconColor}"></span>
      </h1>
      <div class="comp_detail" v-if='[1, 2].includes(type)'>
        <img :src="info.img" alt="" v-if="type == 1">
        <span class="desc-tags">
          <label v-for='(v, i) in info.tag' :key='i'>
            <p class="fd-desc" :style="{color: v.color}">{{v.label}}</p>
          </label>
        </span>
      </div>

      <div class='comp_text' v-if='[3, 4].includes(type)'>
        <div v-html="info.content"></div>
      </div>
    </section>
  </div>
</template>

<script>
  import {VueExtend} from 'godspen-lib'

  export default {
    mixins: [VueExtend.mixin],
    name: 'paragraph',
    label: process.env.LABEL,
    style: process.env.STYLE,
    props: {
      type: {
        type: Number,
        default: 1,
        editer: {
          ignore: true // 忽略，码良基础在编辑器中不显示
        }
      },
      info: {
        type: Object,
        default () {
          return {
            title: '高扩展的在线网页制作平台',
            img: 'https://gw.alipayobjects.com/zos/rmsportal/XKBFuFdRUegzStHGTVdj.png',
            tag: []
          }
        },
        editor: {
          ignore: true
        }
      }
    },
    computed: {
    },
    editorMethods: {
    },
    methods: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component {
    position relative
    .comp_detail_1 {
      padding 8px 16px
      h1 {
        font-weight bolder
        color #333
        border 0
        box-shadow aqua
        font-size 22px
        display flex
        align-items center
        -webkit-box-align: center;
        margin 0
        .content {
          margin 0 8px
        }
        span {
          display inline-block
        }
        .icon {
          width: 4px;
          height: 18px;
          border-radius: 2px 0 0 2px;
          background-color: rgb(98, 96, 225);
          margin-right 6px
        }
        .iconCenter {
          width 12px
          height 3px
          background-color #ffa020
        }
      }
      .titlePage {
        justify-content: center;
      }
      .comp_text {
        padding: 8px 0
        font-size: 14px
        color: #333;
      }
      .comp_detail {
        display: flex;
        align-items: center;
        margin-top: 12px;
        padding 0 8px
        img{
          display: block;
          height: 24px;
          width: 24px;
          border-radius: 50%;
          margin-right 8px
        }
        .desc-tags{
          label {
            position: relative;
            display: inline-block;
            margin: 0 8px 0 0;
            padding: 0 8px 0 0;
            white-space: nowrap;
            p {
              font-size 14px
              margin 0
            }
            &::after {
              position: absolute;
              display: block;
              content: "";
              top: 50%;
              right: 0;
              width: 1px;
              height: 14px;
              transform: translateY(-50%);
              background: #e9e9e9;
            }
            &:last-child::after {
              width 0
            }
          }
        }
      }
    }
  }
</style>
