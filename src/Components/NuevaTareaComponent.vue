<template>
<div class="input-group">
    <input type="text" placeholder="Escribe nueva tarea" v-model="nuevaTarea" class="form-control" v-on:keyup.enter="agregarTarea" />
    <div class="input-group-btn">
        <button class="btn btn-info" @click="agregarTarea">Agregar</button>
    </div>
</div>
</template>

<script>
import {bus} from './../main.js';
export default {
    props: ['tareas'],
    data() {
        return {
            
            nuevaTarea: ''
        }
    },
    methods: {
        agregarTarea: function () {
            var texto = this.nuevaTarea.trim();
            if (texto) {
                this.tareas.push({
                    texto: this.nuevaTarea,
                    terminar: false
                });
               
        bus.actualizarContador(this.tareas.length);
            }
            
            this.nuevaTarea = '';
        }
    },
    created(){
       bus.actualizarContador(this.tareas.length);
    }

}
</script>
