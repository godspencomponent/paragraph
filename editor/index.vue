<template>
  <div class="component-editor">
    <div class='sty'>
      <span>样式：</span>
      <div class='list-type' @click='chooseType(1)'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1564476973676.png" alt="文字列表" />
        <div class="tip">文章标题 + 文章信息 - 1</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == 1'></i>
      </div>
      <div class='list-type' @click='chooseType(2)'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1564483247307.png" alt="文字列表" />
        <div class="tip">文章标题 + 文章信息 - 2</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == 2'></i>
      </div>
      <div class='list-type' @click='chooseType(3)'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1564551969616.png" alt="文字列表" />
        <div class="tip">小标题 + 正文 - 左对齐</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == 3'></i>
      </div>
      <div class='list-type' @click='chooseType(4)'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/resource/ymm_1564556088057.png" alt="文字列表" />
        <div class="tip">小标题 + 正文 - 居中</div>
        <i class="el-icon-circle-check" v-if='componentInfo.type == 4'></i>
      </div>
    </div>
    <el-card class="box-card" header='基础配置'>
      <div>
        <el-form ref="form" label-width="100px" label-position='right' size='mini'>
          <el-form-item label="标题:">
            <div class="tag">
              <el-input v-model="componentInfo.info.title" placeholder="请输入标题"></el-input>
              <el-color-picker v-model="componentInfo.info.titleColor" show-alpha></el-color-picker>
            </div>
          </el-form-item>

          <el-row>
            <el-col :span='12'>
              <el-form-item label="标题字号:">
                <el-input placeholder="请输入文字大小" v-model="componentInfo.info.titleFont" min='0' type='number'>
                    <template slot="append">px</template>
                  </el-input>
              </el-form-item>
            </el-col>
            <el-col :span='12' v-if='[3, 4].includes(componentInfo.type)'>
              <el-form-item label="标题图标颜色:" label-width="150px">
                <el-color-picker v-model="componentInfo.info.iconColor" show-alpha></el-color-picker>
            </el-form-item>
            </el-col>
          </el-row>
          
          <el-form-item label="头像:" v-if='componentInfo.type == 1'>
            <attr-resource type="image" :url.sync="componentInfo.info.img"></attr-resource>
          </el-form-item>
          <el-form-item label="标签列表:" v-if='[1, 2].includes(componentInfo.type)'>
            <el-button type="text" @click='addTag(componentInfo.info)'>新增标签</el-button>
            <div class='tag' v-for='(tag, j) in componentInfo.info.tag' :key='j'>
              <el-input v-model="tag.label" placeholder="标签名"></el-input>
              <el-color-picker v-model="tag.color" show-alpha></el-color-picker>
              <i class="el-icon-delete" @click='delTag(componentInfo.info.tag, j)'></i>
            </div>
          </el-form-item>
          <el-form-item label="内容:" v-if='[3, 4].includes(componentInfo.type)' label-width="50px">
            <attr-richtext :id="componentInfo.type" v-model='componentInfo.info.content'></attr-richtext>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>

<script>
  export default {
    name: 'maliangeditor',
    props: {
      componentInfo: { // 固定字段，收集所有属性值
        type: [Object],
        default () {
          return {
            type: 1,
            info: {
              title: '高扩展的在线网页制作平台',
              img: 'https://gw.alipayobjects.com/zos/rmsportal/XKBFuFdRUegzStHGTVdj.png',
              titleFont: 20,
              titleColor: '',
              iconColor: '#6260e1',
              content: '1.高扩展的在线网页制作平台。<br/> 2.营销团队可以使用码良创建配置非常灵活的页面，配合获取到的访问等数据，可以直观的看到营销效果。',
              tag: [
                  {
                    label: '阿拉雷',
                    color: '#000'
                  },
                  {
                    label: '码良',
                    color: ''
                  }
                ]
            }
          }
        }
      }
    },
    data: function () {
      return {
      }
    },
    computed: {
    },
    watch: {
      componentInfo: {
        hanlder: function (v) {
          console.log('editor index', v)
        },
      }
    },
    mounted: function () {
    },
    methods: {
      chooseType (v) {
        this.componentInfo.type = v
        this.componentInfo.info.title = v == 4 ? '标题' : '高扩展的在线网页制作平台'
        if (v == 2) {
          this.componentInfo.info.tag = [
            {
              label: '10K/月',
              color: 'red'
            },
            {
              label: '月结',
              color: ''
            }
          ]
        } else if (v == 1) {
          this.componentInfo.info.tag = [
              {
                label: '阿拉雷',
                color: '#000'
              },
              {
                label: '码良',
                color: ''
              }
            ]
        } else if (v == 3) {
          this.componentInfo.info.content = '1.高扩展的在线网页制作平台。<br/> 2.营销团队可以使用码良创建配置非常灵活的页面，配合获取到的访问等数据，可以直观的看到营销效果。'
        } else if (v == 4) {
          this.componentInfo.info.content = '码良是一个在线生成h5页面并提供页面管理和页面编辑的平台，用于快速制作H5页面。用户无需掌握复杂的编程技术，通过简单拖拽、少量配置即可制作精美的页面，可用于营销场景下的页面制作。'
        }
      },
      delItem (i) {
        this.componentInfo.list.splice(i, 1)
      },
      addTag (item) {
        let _tag = {
          label: '码良',
          color: ''
        }
        item.tag.push(_tag)
      },
      delTag (tag = [], j) {
        tag.splice(j, 1)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component-editor {
    .sty {
      margin-bottom 30px
    }
    .list-type{
      margin-top 10px
      max-width 250px
      position relative
      border 1px solid #505152
      padding 10px
      border-radius 5px
      img{
        width 100%
      }
      i {
        position absolute
        right 10px
        bottom 15px
        font-size 22px
        color #409EFF
      }
      .tip{
        display: none
        width 100%
        position: absolute
        background-color: rgba(0, 0, 0, 0.7)
        text-align center
        font-size 12px
        padding 3px 0
        bottom 0
        left 0
        color #ccc
      }
      &:hover{
        .tip{
          display: block
        }
      }
    }
    .del-item{
      color #F56C6C
      margin-right 15px
      display none
    }
    .el-collapse-item{
      &:hover{
        .del-item{
          display block
        }
      }
    }
    .tag{
      padding-right 80px
      position relative
      margin-bottom 5px
      .el-color-picker{
        position absolute
        right 30px
        top 0
      }
      i {
        display none
        position absolute
        right 0
        top 5px
        color #F56C6C
        cursor: pointer
      }
      &:hover {
        i {
          display block
        }
      }
    }
  }
</style>
