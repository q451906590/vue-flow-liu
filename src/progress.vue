<template>
  <div class="progress">
    <div class="label" :style="labelstyle" ref="labeitem">
      <img src="./assets/aaa.png" alt="">
      <p class="labeltext">{{label}}</p>
    </div>
    <div class="flow">
      <div class="progressitem" v-for="(item, index) in data" :style="itemstyle.style">
        <p>
          <span :ref="'progressitem' + index" :style="index <= active ? activeclass.circlestyle: ''">{{index + 1}}</span>
        </p>
        <p :style="index <= active ? activeclass.textstyle: ''">
          {{item.title}}
        </p>
        <p>{{item.time}}</p>
      </div>
      <span class="line" v-for="item in line" :style="item.style"></span>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      activeclass: {
        circlestyle: {
          background: '#ff6632',
          color: 'white'
        },
        textstyle: {
          color: '#333333'
        }
      },
      itemstyle: {
        style: {
          width: (100 / this.data.length).toFixed(2) + '%'
        }
      },
      labelstyle: {
        left: 0,
        width: (100 / this.data.length).toFixed(2) + '%'
      },
      line: [
      ]
    }
  },
  mounted () {
    this.$nextTick(() => {
      for (let i = 1; i < this.data.length; i++) {
        let left = (this.$refs['progressitem' + (i - 1)][0].offsetLeft + this.$refs['progressitem' + (i - 1)][0].clientWidth)
        let length = this.$refs['progressitem' + i][0].offsetLeft - left
        this.line.push({
          style: {
            left: (left) + 'px',
            width: (length) + 'px',
            background: i <= this.active ? '#ff6632' : '#eeeeee'
          }
        })
      }
      this.labelstyle.left = this.$refs['progressitem' + this.active][0].offsetLeft - (this.$refs['labeitem'].clientWidth / 2) + (this.$refs['progressitem0'][0].clientWidth / 2) + 'px'
    })
    this.activeclass.circlestyle.background = this.color
    this.activeclass.circlestyle.color = this.textcolor
  },
  watch: {
    active () {
      this.update()
    }
  },
  methods: {
    update () {
      this.$nextTick(() => {
        for (let i = 1; i < this.data.length; i++) {
          let left = (this.$refs['progressitem' + (i - 1)][0].offsetLeft + this.$refs['progressitem' + (i - 1)][0].clientWidth)
          let length = this.$refs['progressitem' + i][0].offsetLeft - left
          this.line.push({
            style: {
              left: (left) + 'px',
              width: (length) + 'px',
              background: i <= this.active ? '#ff6632' : '#eeeeee'
            }
          })
        }
        this.labelstyle.left = this.$refs['progressitem' + this.active][0].offsetLeft - (this.$refs['labeitem'].clientWidth / 2) + (this.$refs['progressitem0'][0].clientWidth / 2) + 'px'
      })
    }
  },
  props: {
    color: {
      type: String,
      default: '#ff6632'
    },
    textcolor: {
      type: String,
      default: 'white'
    },
    data: {
      type: Array,
      default: () => {
        return [{
          title: '1',
          time: 1994
        },
        {
          title: '1',
          time: 1994
        },
        {
          title: '1',
          time: 1994
        },{
          title: '1',
          time: 1994
        }]
      }
    },
    label: {
      type: String,
      default: 'test'
    },
    active: {
      type: Number,
      default: 0
    }
  }
}
</script>
<style scoped>
.progress{
  overflow: hidden;
}
.flow{
  position: relative;
  overflow: hidden;
}
.progressitem{
  float: left;
}
.progressitem p{
    text-align: center;
  }
.progressitem p:nth-child(1) span{
      display: block;
      text-align: center;
      width: 1.5rem;
      height: 1.5rem;
      line-height: 1.5rem;
      margin: 0 auto;
      background-color: #cccccc;
      border-radius: 50%;
      color: white;
}
.progressitem p:nth-child(2){
    margin-top: 0.1778rem;
    font-size: 0.3241rem;
    color: #ababab;
  }
.progressitem p:nth-child(3){
    margin-top: 0.052rem;
    font-size: 0.3148rem;
    color:#ababab;
}
.line{
  height: 0.1rem;
  position: absolute;
  top: 20%;
  left: 0;
  width: 100px;
}
.label{
  top: 0;
  position: relative;
  text-align: center;
}
.label img{
    width: 80%;
    max-width: 150px;
}
.label .labeltext{
    position: absolute;
    width: 100%;
    text-align: center;
    top: 10%;
    color: white;
    font-size: 0.3241rem;
}
</style>
