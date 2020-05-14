<template>
  <div id="gallery">
        <button class="prev" @click.stop="goprev()">&lt;</button>
        <div class="img_container" ref="img_container" :style="styleObject">
            <div class="img_wrapper" v-for="(item, index) in imgArr" :key="index">
                <img :src="item.imgsrc">
                <div class="cover">
                    <p>作者：{{item.name}}</p>
                    <p>日期：{{item.time}}</p>
                </div>       
            </div>
        </div>
        <button class="next" @click.stop="gonext()">&gt;</button>
        <div class="bar" @mousemove="move">
            <div class="bar_container" 
                 @mousedown="flag = true" 
                 @mouseup="flag = false" 
                 :style="barStyleObject"></div>
        </div>
    </div>
</template>

<script>


export default {
  data () {
    return {
      count: 0,
      flag: false,
      styleObject: {
          'left' : '0px',
          'transition': 'all 0.3s ease-in-out'
      },
      barStyleObject: {
          'left' : '0px',
          'transition': 'all 0.3s ease-in-out'
      },
      imgArr: [
          {imgsrc: require('../assets/images/img-1.jpg'), name:'author1', time:'2019-01-25'},
          {imgsrc: require('../assets/images/img-2.jpg'), name:'author2', time:'2020-07-25'},
          {imgsrc: require('../assets/images/img-3.jpg'), name:'author3', time:'2014-01-25'},
          {imgsrc: require('../assets/images/img-4.jpg'), name:'author4', time:'2022-01-25'},
          {imgsrc: require('../assets/images/img-1.jpg'), name:'author1', time:'2019-01-27'},
          {imgsrc: require('../assets/images/img-2.jpg'), name:'author2', time:'2020-07-25'},
          {imgsrc: require('../assets/images/img-3.jpg'), name:'author3', time:'2014-01-16'},
          {imgsrc: require('../assets/images/img-4.jpg'), name:'author4', time:'2022-01-25'},
          {imgsrc: require('../assets/images/img-1.jpg'), name:'author1', time:'2019-01-25'},
          {imgsrc: require('../assets/images/img-2.jpg'), name:'author2', time:'2020-07-25'},
          {imgsrc: require('../assets/images/img-3.jpg'), name:'author3', time:'2014-01-25'},
          {imgsrc: require('../assets/images/img-4.jpg'), name:'author4', time:'2022-01-25'},
          {imgsrc: require('../assets/images/img-1.jpg'), name:'author1', time:'2019-01-05'},
          {imgsrc: require('../assets/images/img-2.jpg'), name:'author2', time:'2020-07-25'},
          {imgsrc: require('../assets/images/img-3.jpg'), name:'author3', time:'2014-01-17'},
          {imgsrc: require('../assets/images/img-4.jpg'), name:'author4', time:'2022-01-21'}
      ]
    }
  },
  methods: {
    buttonInitActions(){
        this.styleObject['transition'] = 'all 0.3s ease-in-out';
        this.barStyleObject['transition'] = 'all 0.3s ease-in-out';
        this.styleObject['left'] = this.count + 'px';
        this.barStyleObject['left'] = -this.count/1.67 + 'px';
    },
    goprev(){
        if(this.count >= 0) return;
        this.count += 490;
        this.buttonInitActions();
    },
    gonext(){
        this.count -= 490;
        if(this.count <= -1960) this.count = 0;
        this.buttonInitActions();
    },
    move(e){
        this.styleObject['transition'] = '';
        this.barStyleObject['transition'] = '';
        var reg = /[^px]+/g;
        var num = this.barStyleObject['left'].match(reg)[0];
        if(num >= 0 && num < 293){
            this.count = -490;
        }else if(num < 586){
            this.count = -980;
        }else if(num < 880){
            this.count = -1470;
        }
        if(num < 0) {
            this.styleObject['left']  = '0px';
            this.barStyleObject['left'] = '0px';
            this.flag = false;
        }else if(this.flag && num >= 0){
            this.barStyleObject['left'] = e.clientX - 225 + 'px';
            this.styleObject['left']  = -num*2 + 'px';
            if(num > 880){
                this.barStyleObject['left'] = '880px';
                this.flag = false;
            }
        }
    }
}
}
</script>
