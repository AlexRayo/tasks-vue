<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Add some task</div>

                    <div class="card-body">
                        <form action="./api/tarea" method="POST" @submit.prevent="agregarTarea()">
                            <div class="form-group">
                              <label for=""></label>
                              <input type="text" name="title" v-model="title" placeholder="Title here" class="form-control">
                            </div>
                            <div class="form-group">
                              <input type="submit" value="Add task" class="btn btn-info">
                            </div>

                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        methods: {
            agregarTarea(){
                if(this.title != ''){
                axios.post('./api/tarea',{title:this.title});/* manda los datos al codigo backend; en este caso el título */
                EventTarea.$emit('tareaCreada', {title: this.title});/*'EventTarea' nombre del evento que hace posible mostrar los nuevos datos ingresados mediate un elace entre componentes (FormTarea-ListaTareas) */
                /* 'tareaCreada' nombre personalizado del evento; se recibe en el otro componente */
                /* {title: this.title} es el segundo parámetro q se envía al otro compotente */
                }
                else{
                    alert('El título es requerido');
                }

            }
        },
    }
</script>
