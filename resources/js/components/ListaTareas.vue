<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Registered tasks</div>

                    <div class="card-body">
                        <ul>
                            <li v-for='tarea in tareas'>{{tarea.title}}</li>
                        </ul>
                        {{errorResp}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                tareas: [],/* pinta los datos recibidos */
                errorResp: ''
            }
        },
        mounted() {
            /*Hacer algo acá cuando el componente de cargue, (no tiene nada q ver con recibir datos)*/
        },
        created() {
            /* primero se carga lo que ya está en la db */
            axios.get('./api/tarea')
                .then(response => this.tareas = response.data);
            /********************************************/

            /*El siguiente evento se encarga de hacer push a este componente (ListaTareas) para no recargar la página */
            EventTarea.$on('tareaCreada', (title) =>{ /* '.$on' se encarga de escuchar el evento */
                this.tareas.push(title);/* se agrega a ListaTareas si se hace nuevo ingreso 'title' */
            });
            
        },
    }
    
</script>
