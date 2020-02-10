<template>
    <div class="m-menu">
        <dl class="nav" @mouseleave="menuLeave">
            <dt>全部分类</dt>
            <dd v-for="(item, index) in menuList" :key="index" @mouseenter="menuEnter(item)">
                <i :class="item.type"></i>
                {{item.name}}
                <span class="arrow"></span>
            </dd>
        </dl>
        <div v-if="curDetail" class="detail" @mouseenter="detailEnter" @mouseleave="detailLeave">
            <template v-for="(item, index) in curDetail.items" >
                <h4 :key="index">{{item.title}}</h4>
                <span v-for="(v, i) in item.items" :key="v + '_'+ i">{{v}}</span>
            </template>
        </div>
    </div>
</template>
<script>
export default {
  data () {
    return {
      curDetail: null,
      menuList: [{
        title: '美食',
        icon: 'food',
        children: [{
          title: '美食',
          children: ['代金卷', '甜点饮品', '火锅自助餐', '小吃快餐']
        }]
      },
      {
        title: '外卖',
        icon: 'takeout',
        children: [{
          title: '外卖',
          children: ['美团外卖']
        }]
      },

      {
        title: '酒店',
        icon: 'hotel',
        children: [{
          title: '星级酒店',
          children: ['经典型', '舒适/三星', '高档/四星', '豪华/五星']
        }]
      }

      ]
    }
  },
  methods: {
    menuEnter (item) {
      console.log(item)
      this.curDetail = item
    },
    menuLeave () {
      var self = this
      this.timer = setTimeout(function () {
        self.curDetail = null
      }, 200)
    },
    detailEnter () {
      clearTimeout(this.timer)
    },
    detailLeave () {
      this.curDetail = null
    }
  }
}
</script>
