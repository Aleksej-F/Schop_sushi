<template>
    <div class="navigation"
        v-bind:class="{'navigation-active':burgerAktive}"
    >
        <div class="wrapper">
            <nav >
                <div class="navigation__burger"
                    v-on:click.prevent="myClickKell()"
                >
                    <div class="navigation__burger-burger"
                        v-bind:class="{'navigation__burger-burger-active':burgerAktive}"
                    >
                        <span class="navigation__burger-span"
                            
                        ></span>
                        <span class="navigation__burger-span"
                           
                        ></span>
                        <span class="navigation__burger-span"
                           
                        ></span>
                    </div>
                    <div class="navigation__burger-title">{{burgerTitle}}</div>
                </div>

                <ul class="navigation__menu"
                    v-bind:class="{'navigation__menu-active':burgerAktive}"
                >
                    <li>
                        <a href="">Блюда от шеф-повара</a>
                    </li>
                    <li>
                        <a href="">Паназиатская кухня</a>
                    </li>
                    <li>
                        <a href="">Акции</a>
                    </li>
                    <li>
                        <a href="">Блюда на мангале</a>
                    </li>
                    <li>
                        <a href="">Роллы</a>
                    </li>
                    <li>
                        <a href="">Сеты</a>
                    </li>
                    <li>
                        <a href="">Wok</a>
                    </li>
                    <li>
                        <a href="">Пицца</a>
                    </li>
                    <li>
                        <a href="">Комбо-наборы</a>
                    </li>
                     <li>
                        <a href="">Закуски и салаты</a>
                    </li>
                     <li>
                        <a href="">Горячее</a>
                    </li>
                     <li>
                        <a href="">Напитки и десерты</a>
                    </li>
                     <li>
                        <a href="">Соусы</a>
                    </li>
                     <li>
                        <a href="">Акции</a>
                    </li>
                </ul>
            </nav>
        </div>
    </div>
</template>
<script>


export default {
    data() {
        return {
            burgerTitle: 'Меню',
            burgerAktive:false,
        }
    },
    methods: {
        myClickKell() {
            console.log('меню')
            
            this.burgerAktive = !this.burgerAktive 
            this.burgerTitle = this.burgerAktive ? 'Закрыть': 'Меню'
        }
    }
}
</script>
