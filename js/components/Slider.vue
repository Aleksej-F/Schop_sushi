<template>
    <div class="slider">
        <div class="slider-block" 
            @mousedown="down"
            @mouseup="up"
            @mousemove="mousemove"
            
        >
            <div class="slider-item" data-n="0"
                v-bind:style="leftSlaid.a"
            >
                <div class="slider-item-link">
                    <a href="">
                        <div class="slider-item-link-r"></div>
                    </a>
                </div>
            </div>

            <div class="slider-item" data-n="1"
                v-bind:style="leftSlaid.b"
            >
                <div class="slider-item-link">
                    <a href="">
                         <div class="slider-item-link-r"></div>
                    </a>
                </div>
            </div>

            <div class="slider-item" data-n="2"
                v-bind:style="leftSlaid.c"
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
            activeNavC: 0,
            slidePosition:[]  
        }
    },
    mounted() {
        this.widthSlide = window.innerWidth;
        this.leftSlaidNull = {a: 0, b: this.widthSlide, c: -this.widthSlide};
        this.leftSlaid = {a:{left: 0 + 'px'}, b:{left: this.widthSlide + 'px'}, c:{left: -this.widthSlide + 'px'}};
        this.slidePosition = [
            [0,this.widthSlide,-this.widthSlide],
            [-this.widthSlide,0,this.widthSlide],
            [this.widthSlide,-this.widthSlide,0]
        ]
    },

    methods: {
        down(e)  {
            
            //console.log(e)  

           // console.log(window.innerWidth)
            
                console.log('нажал кнопку мыши')  
                if (e !== undefined){
                    this.downPrizn = true
                    this.leftDown=e.offsetX
                    console.log(this.leftDown)
                }

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
            
            if (Math.abs(this.changeLeft)>150) {
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

                   
                }

                
            }else{
                this.leftSlaid.a={
                    left:this.leftSlaidNull.a +  'px',
                    transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'}
                this.leftSlaid.b={
                    left:this.leftSlaidNull.b +  'px',
                    transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'}
                this.leftSlaid.c={
                    left:this.leftSlaidNull.c +  'px',
                    transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'}

            }
            this.changeLeft = 0
        },

        mousemove(e){
            if (this.downPrizn){
                this.changeLeft = e.offsetX - this.leftDown
                this.leftSlaid.a.left = this.leftSlaidNull.a + this.changeLeft +  'px'
                this.leftSlaid.b.left = this.leftSlaidNull.b + this.changeLeft +  'px'
                this.leftSlaid.c.left = this.leftSlaidNull.c + this.changeLeft +  'px'
            }
        },

        clickNav(e){
            console.dir(e.target.attributes['data-n'].textContent)
            const aktive = e.target.attributes['data-n'].textContent
            //.attributes.data-n.textContent
            if ( !this.activeNav[aktive].q) {  
                switch(aktive) {
                    case '0':
                        console.log('нажал 0');
                        if ( this.activeNav[1].q) {
                            console.log('да');
                            this.leftSlaidNull.a = this.widthSlide;
                            this.leftSlaidNull.c = -this.widthSlide;
                        }


                        
                        break;
                    case '1':
                        console.log('нажал 1');
                        if ( this.activeNav[2].q) {
                            console.log('да');
                            this.leftSlaidNull.b = this.widthSlide;
                            this.leftSlaidNull.a = -this.widthSlide;}
                        break;
                    case '2':
                        console.log('нажал 2');
                        if ( this.activeNav[0].q) {
                            console.log('да');
                            this.leftSlaidNull.c = this.widthSlide;
                            this.leftSlaidNull.b = -this.widthSlide;
                        }
                        break;
                    

                }
                
                
                this.activeNav[this.activeNavC].q = !this.activeNav[this.activeNavC].q
                this.activeNavC = Number(aktive)
                this.activeNav[this.activeNavC].q = !this.activeNav[this.activeNavC].q
                console.log(this.leftSlaid)
                   
                
                const p =  new Promise((resolve)=>{
			        this.down()
				    setTimeout(() => {resolve()}, 100)
			
		        })
                p.then(()=>{ 
                    this.leftSlaid.a={
                        left : this.leftSlaidNull.a - this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    this.leftSlaid.b={
                        left : this.leftSlaidNull.b - this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }
                    this.leftSlaid.c={
                        left : this.leftSlaidNull.c - this.widthSlide +  'px',
                        transition: 'left .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)'
                    }

                     setTimeout(() => {
                        this.leftSlaidNull.a = this.slidePosition[aktive][0]
                        this.leftSlaidNull.b = this.slidePosition[aktive][1]
                        this.leftSlaidNull.c = this.slidePosition[aktive][2]
                    }, 800);
                })
            }
        },
        
    },
}
</script>
