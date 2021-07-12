<template>
    <div class="container">

        <router-link to="/crear" class="btn btn-success">Agregar Nuevo empleado</router-link>
        <br><br>

        <div class="card">
            <div class="card-header">
                Empleados
            </div>
            <div class="card-body">

                <table class="table">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Correo</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>

                        <tr v-for="empleado in empleados" :key="empleado.id">
                            <td> {{ empleado.id}} </td>
                            <td> {{ empleado.nombre}} </td>
                            <td> {{ empleado.correo}} </td>
                            <td>
                                <div class="btn-group" role="group" aria-label="">

                                    <router-link :to="{name:'Editar', params:{id:empleado.id}}" class="btn btn-info">Editar</router-link>
                                    <button type="button" v-on:click="borrarEmpleado(empleado.id)" class="btn btn-danger">Borrar</button>

                                </div>
                            </td>
                        </tr>

                    </tbody>
                </table>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    data(){
        return{
            empleados:[]
        }
    },

    created:function(){

        this.consultarEmpleados();
    },
    methods:{
        consultarEmpleados(){
            fetch('http://localhost/practicas/api/empleados/')
            .then(resp => resp.json())
            .then((dataResp) => {
                console.log(dataResp)
                this.empleados=[]
                if(typeof dataResp[0].success === 'undefined'){
                    this.empleados = dataResp;
                }
            })
            .catch(console.log)
        },
        borrarEmpleado(id){
            console.log(id);

            fetch('http://localhost/practicas/api/empleados/?borrar='+id)
            .then(resp => resp.json())
            .then((dataResp) => {

                console.log(dataResp)
                window.location.href="listar"
            })
            .catch(console.log)
        }
    }
}
</script>