<script>
export default {
    data: () => ({
        proyecto: "",
        tipo: "",
        urgente: false,
        proyectos: [],
        numeroProyectos: 0,
    }),
    methods: {
        cambiarUrgencia(proyecto, campo) {
            console.log(proyecto, campo);
            proyecto[campo] = !proyecto[campo];

        },
        regsitrarProyecto() {
            const proyecto = {
                proyecto: this.proyecto,
                tipo: this.tipo,
                urgente: this.urgente,
                completado: false,
            };
            this.proyectos.push(proyecto);
            console.warn("Proyecto regsitrado\n", this.proyectos);

            this.proyecto = "";
            this.tipo = "";
            this.urgente = false;
        },
    },
    computed: {
        numeroProyectos() {
            return this.proyectos.length;
        }
    }
};
</script>

<template>
    <div class="row">
        <div class="col-12 col-md-4">
            <form @submit.prevent="regsitrarProyecto" class="mt-4">
                <div class="mb-3">
                    <label class="form-label"> Proyecto </label>
                    <input class="form-control" type="text" v-model.trim="proyecto" placeholder="Nombre de Proyecto"
                        required />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Actividades</label>
                    <select name="" id="" class="form-select" v-model="tipo" required>
                        <option selected disabled value="">Seleciona un tipo de actividad</option>
                        <option>Aplicaciones Web con Vue.js</option>
                        <option>Backend Services con Node.js</option>
                        <option>App movil con React Native</option>
                    </select>
                </div>
                <div class="mb-3">
                    <label class="form-check-label">Urgente </label>
                    <input v-model="urgente" class="form-check-input" type="checkbox" />
                </div>
                <button class="btn btn-success btn-block" type="submit">Enviar</button>
            </form>
        </div>
        
        <div class="col-12 col-md-8">
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
        </div>
    </div>
    <pre>
        {{proyecto}}
        {{tipo}}
        {{urgente}}
    </pre>
</template>

<style scoped>
.form-check-label {
    margin-right: 0.5rem !important;
}

td.bg-success,
td.bg-danger {
    cursor: pointer;
}
</style>