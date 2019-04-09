<template>
<div class="cover" ref="cover">
    <div class="pop" :style="{left: leftx, top: topy}" ref="pop"
    @mousedown="touchdown" @mousemove="touchmove" @mouseup="touchup">
        <span class="close" @click="hidden">X</span>
        <slot></slot>
        <div class="action">
            <button class="comfirm" @click="confirm">确认</button>
            <button class="cancel">取消</button>
        </div>
    </div>
</div>    
</template>

<script>
export default {
    data(){
       return {
           leftx: 0,
            topy: 0,
            ismove: false,
            distanceX: 0,
            distanceY: 0,
       }
    },
    props:{
        father:{
            type: Array,
            required: true
        }
    },
    created(){
       
    },
    mounted(){
        this.leftx = (this.$refs.cover.clientWidth - this.$refs.pop.clientWidth)/2 +'px';
        this.topy = (this.$refs.cover.clientHeight - this.$refs.pop.clientHeight)/2 + 'px';
    },
    methods:{
        touchdown(e){
            this.ismove = true;
            this.distanceX =e.clientX - this.$refs.pop.offsetLeft;
            this.distanceY = e.clientY - this.$refs.pop.offsetTop;
        },
        touchmove(e){
            if(this.ismove){
              setTimeout(()=>{
                  this.leftx = e.clientX - this.distanceX + 'px';
                  this.topy = e.clientY - this.distanceY + 'px';
              },50)
           }
        },
        touchup(){
          this.ismove = false
        },
        hidden(){
            this.father[0][this.father[1]] = false;
        },
        confirm(){
            this.hidden()
            this.$emit('myway')
        }
    }
}
</script>

<style scoped>
.cover{
    position: fixed;
    top: 0 ; 
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.6);
  
}
 .pop{
    max-width: 800px;
    min-width: 180px;
    border: 1px solid #ccc;
    position: absolute;
    background-color: #fff;
    padding-left: 10px;
}
.close{
    display: block;
    text-align: right;
    padding-right: 15px;
}
.action{
    line-height: 40px;
}
</style>

