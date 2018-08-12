<template>
<div>
    <h1>{{tituloEnMayusculas()}}</h1>
    <h3>Tareas por hacer :{{totalTareas}}</h3>
</div>
</template>

<script>
import {bus} from './../main.js';
export default {
    props: ['titulo'],
    data(){
        return{
       totalTareas:0
        }
    },
    methods: {
        tituloEnMayusculas() {
            return this.titulo.toUpperCase();
        }
    },
    created(){
        bus.$on('actualizarContador',(num)=>{
            this.totalTareas=num;
        });
    }

}
</script>
