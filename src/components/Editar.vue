<template>
    <div class="container">

        <div class="card">
            <div class="card-header">
                Editar Nuevo Empleado
            </div>
            <div class="card-body">

                <form v-on:submit.prevent="actualizarRegistro">
                    <div class="form-group">
                      <label for="nombre">Nombre</label>
                      <input type="text"
                        class="form-control" required name="nombre" v-model="empleado.nombre" id="nombre" aria-describedby="helpId" placeholder="Nombre">
                      <small id="helpId" class="form-text text-muted">Nombre del empleado</small>
                    </div>

                    <div class="form-group">
                      <label for="correo">Correo</label>
                      <input type="email"
                        class="form-control" required name="correo" v-model="empleado.correo" id="correo" aria-describedby="helpId" placeholder="Correo Electrónico">
                      <small id="helpId" class="form-text text-muted">Correo del empleado</small>
                    </div>

                    <div class="btn-group" role="group" aria-label="">
                        <button type="submit" class="btn btn-info">Modificar</button>

                        <router-link :to="{name:'Listar'}" class="btn btn-danger">Cancelar</router-link>
                    </div>
                </form>
                
            </div>
        </div>

    </div>
</template>

<script>
export default {
    data(){
        return{
            empleado:{}
        }
    },
    created:function(){
        this.obtenerInformacionID();
    },
    methods:{
        obtenerInformacionID(){
            fetch('http://localhost/practicas/api/empleados/?consultar='+this.$route.params.id)
            .then(resp => resp.json())
            .then((dataResp) => {

                console.log(dataResp)
                this.empleado = dataResp[0];

            })
            .catch(console.log)
        },
        actualizarRegistro(){
            var datosEnviar={id:this.$route.params.id,
                            nombre:this.empleado.nombre,
                            correo:this.empleado.correo}
            fetch('http://localhost/practicas/api/empleados/?actualizar='+this.$route.params.id, {
                method:"POST",
                body:JSON.stringify(datosEnviar)
            })
            .then(resp => resp.json())
            .then((dataResp => {
                console.log(dataResp);
                window.location.href='../listar'
            }))
        }
    }
}
</script>