<script>
    export default{
        props:['numeroProyectos', 'proyectos', 'cambiarUrgencia'],
    }
</script>

<template>
    <h3 class="my-4"> Total de proyectos: {{numeroProyectos}}</h3>
    <div class="table-responsive">
        <table class="table table-dark ">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Proyecto</th>
                    <th>Tipo</th>
                    <th>Urgente</th>
                    <th>Completado</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(proyect, index) in proyectos">
                    <td>{{index+1}}</td>
                    <td>{{proyect.proyecto}}</td>
                    <td>{{proyect.tipo}}</td>
                    <td @click="cambiarUrgencia(proyect, 'urgente')"
                        :class="proyect.urgente ? 'bg-success':'bg-danger'">{{proyect.urgente ? "Si":"No"}}</td>
                    <td @click="cambiarUrgencia(proyect, 'completado')"
                        :class="proyect.completado ?  'bg-success':'bg-danger' "> {{proyect.completado ?
                        "Completado" : "Incompleto" }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>