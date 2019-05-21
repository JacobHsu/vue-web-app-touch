<template>
    <div class="delete">
        <div class="slider">
            <div class="content" @touchstart='touchStart' @touchmove='touchMove' @touchend='touchEnd' :style="deleteSlider">
                <slot name="img"></slot>
                <slot name="title"></slot>
                <slot name="price"></slot>

                <slot></slot>
            </div>
            <div class="remove" ref='remove' @click="deleteLine">
                删除
            </div>
        </div>

    </div>
</template>


<script>
export default {
    props: ['index'],
    data() {
        return {
            startX: 0,   //觸摸位置
            endX: 0,     //結束位置
            moveX: 0,   //滑動時的位置
            disX: 0,    //移動距離
            deleteSlider: '',//滑動時的效果,使用v-bind:style="deleteSlider"
        }
    },
    methods:{
        touchStart(ev){
            ev = ev || event
            //tounches類數組，等於1時表示此時有只有一隻手指在觸摸屏幕
            if(ev.touches.length == 1){
                // 記錄開始位置
                this.startX = ev.touches[0].clientX;
            }
        },
        touchMove(ev){
            ev = ev || event;
            //獲取刪除按鈕的寬度，此寬度為滑塊左滑的最大距離
            let wd = this.$refs.remove.offsetWidth;
            if(ev.touches.length == 1) {
                // 滑動時距離瀏覽器左側實時距離
                this.moveX = ev.touches[0].clientX
                //起始位置減去 實時的滑動的距離，得到手指實時偏移距離
                this.disX = this.startX - this.moveX;
                //console.log(this.disX)
                // 如果是向右滑動或者不滑動，不改變滑塊的位置
                if (this.disX < 0 || this.disX == 0) {
                    this.deleteSlider = "transform:translateX(0px)";
                } else if (this.disX > 0) {// 大於0，表示左滑了，此時滑塊開始滑動 
                    //具體滑動距離我取的是 手指偏移距離*5。
                    this.deleteSlider = "transform:translateX(-" + this.disX*5 + "px)";
                    // 最大也只能等於刪除按鈕寬度 
                    if (this.disX*5 >= wd) {
                        this.deleteSlider = "transform:translateX(-" +wd+ "px)";
                    }
                }
            }
        },
        touchEnd(ev){
            ev = ev || event;
            let wd = this.$refs.remove.offsetWidth;
            if (ev.changedTouches.length == 1) {
                let endX = ev.changedTouches[0].clientX;
                this.disX = this.startX - endX;
                //console.log(this.disX)
                //如果距離小於刪除按鈕一半,強行回到起點
                if ((this.disX*5) < (wd/2)) {
                    this.deleteSlider = "transform:translateX(0px)";
                }else{
                    //大於一半 滑動到最大值
                    this.deleteSlider = "transform:translateX(-"+wd+ "px)";
                }
            }
        },
        deleteLine (){
            this.deleteSlider = "transform:translateX(0px)";
            this.$emit('deleteLine'); //methods  deleteLine  
        }   
    }
}
</script>

<style scoped>
.slider{
    width: 100%;
    height: 120px;
    margin-bottom: 10px;
    position: relative;
    
}
.content{
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 100;
    transition: 0.3s;
    background-color: #fff;
    border-bottom: 1px solid #d3d3d3;
}
.remove{
    position: absolute;
    width:140px;
    height:120px;
    background-color: #f60;
    right: 0;
    top: 0;
    color:#fff;
    text-align: center;
    font-size: 32px;
    line-height: 120px;
}
</style>