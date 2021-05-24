<template>
    <div class="slider">
        <div class="slider-block" 
            @mousedown="down"
            @mouseup="up"
            @mousemove="mousemove"
            
        >
            <div class="slider-item" data-n="0"
                v-bind:style="  leftSlaid.a "
            >
                <div class="slider-item-link">
                    <a href="">
                        <div class="slider-item-link-r"></div>
                    </a>
                </div>
            </div>

            <div class="slider-item" data-n="1"
                v-bind:style="leftSlaid.b "
            >
                <div class="slider-item-link">
                    <a href="">
                         <div class="slider-item-link-r"></div>
                    </a>
                </div>
            </div>

            <div class="slider-item" data-n="2"
                v-bind:style="leftSlaid.c "
            >
                <div class="slider-item-link"></div>
            </div>
        </div>

        <div class="slider-nav"
            @click="clickNav"
            
        >
                <a href="#" class="circle" 
                    v-for="good in activeNav"
                    :key="good.id"
                    v-bind:data-n=good.id 
                    v-bind:class="{'circle-active':good.q}"
                ></a>
               
        </div>

    </div>
</template>
<script>


export default {
    data() {
        return {
            downPrizn: false,
            widthSlide:0,
            leftSlaid: {a:0,b:0,c:0},
            leftSlaidNull: {a:0,b:0,c:0},
            changeLeft:0,
            leftDown:0,
            activeNav:[{id:0, q:true},{id:1,q:false},{id:2,q:false}],
            activeNavC: 0
        }
    },
    mounted() {
        this.widthSlide = window.innerWidth;
        this.leftSlaidNull = {a: 0, b: this.widthSlide, c: -this.widthSlide};
        this.leftSlaid = {a:{left: 0 + 'px'}, b:{left: this.widthSlide + 'px'}, c:{left: -this.widthSlide + 'px'}};

    },

    methods: {
        down(e)  {
            console.log('нажал кнопку мыши')           
            console.log(window.innerWidth)
            this.downPrizn=true
            this.leftDown=e.offsetX
            console.log(this.leftDown)
            this.leftSlaid.a={
                        left : this.leftSlaidNull.a  +  'px',
                        transition: ''
            }
            this.leftSlaid.b={
                        left : this.leftSlaidNull.b  +  'px',
                        transition: ''
            }
            this.leftSlaid.c={
                        left :this.leftSlaidNull.c  +  'px',
                        transition: ''
            }



        },

        up(){
            console.log('отпустил кнопку мыши')  
            this.downPrizn=false
            
            if (Math.abs(this.changeLeft)>100) {
                 console.log('this.changeLeft')
                 console.log(this.changeLeft)
                 this.activeNav[this.activeNavC].q = !this.activeNav[this.activeNavC].q
         
                if (this.changeLeft < 0) {
                    console.log('leftSlaid < 0') 
                     if (this.activeNavC === this.activeNav.length-1) {
                        this.activeNavC = 0
                    } else {this.activeNavC++}
                    
                    this.activeNav[this.activeNavC].q = !this.activeNav[this.activeNavC].q
                    
                    this.leftSlaid.a={
                        left : this.leftSlaidNull.a - this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    this.leftSlaid.b={
                        left : this.leftSlaidNull.b - this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    this.leftSlaid.c={
                        left :this.leftSlaidNull.c - this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                                       
                    setTimeout(() => {
                        this.leftSlaidNull.a = Number(this.leftSlaid.a.left.slice(0 , -2)) < -this.widthSlide ? this.widthSlide : Number(this.leftSlaid.a.left.slice(0 , -2))
                        this.leftSlaidNull.b = Number(this.leftSlaid.b.left.slice(0 , -2)) < -this.widthSlide ? this.widthSlide : Number(this.leftSlaid.b.left.slice(0 , -2))
                        this.leftSlaidNull.c = Number(this.leftSlaid.c.left.slice(0 , -2)) < -this.widthSlide ? this.widthSlide : Number(this.leftSlaid.c.left.slice(0 , -2))
                    }, 800);
                     console.log(this.leftSlaidNull)
                } else {
                    console.log('leftSlaid>0')
                   
                     if (this.activeNavC === 0) {
                        this.activeNavC = this.activeNav.length-1
                    } else {this.activeNavC--}
                    
                    this.activeNav[this.activeNavC].q = !this.activeNav[this.activeNavC].q

                     this.leftSlaid.a={
                        left : this.leftSlaidNull.a + this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    this.leftSlaid.b={
                        left : this.leftSlaidNull.b + this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    this.leftSlaid.c={
                        left :this.leftSlaidNull.c + this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    
                    
                    setTimeout(() => {
                        this.leftSlaidNull.a = Number(this.leftSlaid.a.left.slice(0 , -2)) > this.widthSlide ? -this.widthSlide : Number(this.leftSlaid.a.left.slice(0 , -2))
                        this.leftSlaidNull.b = Number(this.leftSlaid.b.left.slice(0 , -2)) > this.widthSlide ? -this.widthSlide : Number(this.leftSlaid.b.left.slice(0 , -2))
                        this.leftSlaidNull.c = Number(this.leftSlaid.c.left.slice(0 , -2)) > this.widthSlide ? -this.widthSlide : Number(this.leftSlaid.c.left.slice(0 , -2))
                       
                    }, 800);
                    console.log(this.leftSlaidNull)
                }

                
            }else{
                this.leftSlaid.a.left = this.leftSlaidNull.a +  'px'
                this.leftSlaid.b.left = this.leftSlaidNull.b +  'px'
                this.leftSlaid.c.left = this.leftSlaidNull.c +  'px'

            }
        },

        mousemove(e){
            //console.log(this.downPrizn)
            
            if (this.downPrizn){
               // console.log(e.offsetX)
                this.changeLeft = e.offsetX - this.leftDown
                this.leftSlaid.a.left = this.leftSlaidNull.a + this.changeLeft +  'px'
                this.leftSlaid.b.left = this.leftSlaidNull.b + this.changeLeft +  'px'
                this.leftSlaid.c.left = this.leftSlaidNull.c + this.changeLeft +  'px'
                console.log(this.changeLeft)
                console.log(this.leftSlaid)
            }
        },

        clickNav(e){
            console.dir(e.target.attributes['data-n'].textContent)
            //.attributes.data-n.textContent
            },
        
    },
}
</script>
