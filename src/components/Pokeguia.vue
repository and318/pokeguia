<template>
<div class="container">
    <div class="row">
        <div class="col-lg-12">

            <img src="src/img/logo.png" alt="logo" class="mx-auto d-block">
        </div>
        <div class="col-lg-12">
            <h1 class="text-center mt-5">Nueva pokeguia</h1>
            <div class="flex-row">
                <p class="text-center mt-4">Ingresa el nombre de tu personaje</p>
                <div class="d-flex justify-content-center ">

                    <div class="input-group mb-3 col-md-4">
                        <input type="text" v-model="personaje.name" @keyup.enter="fetchCharacter" class="form-control" placeholder="Ingrese nueva tarea">
                        <div class="input-group-append">
                            <button @click.prevent="fetchCharacter" class="btn btn-outline-secondary" type="button">Agregar</button>
                        </div>
                    </div>
                </div>
                <img :src="image.front_default" alt="no hay foto" class="mx-auto d-block">
                <h3 class="text-center">Movimientos</h3>
                <ul class="lista">
                    <li v-for="(movimiento,index) in movimientos" :key="index">{{movimiento.move.name}}</li>
                </ul>
                <h3 class="text-center">habilidades</h3>
                <ul class="lista">
                    <li v-for="(habilidad,index) in habilidades" :key="index">{{habilidad.ability.name}}</li>
                </ul>
            </div>

        </div>

    </div>
</div>
</template>

<script>
export default {
    name: 'pokedatos',
    //props: {},
    data: function () {
        return {
            personaje: {
                name: "pikachu",
                moves: "",
                abilities: "",
                sprites: {
                    front_default: "",
                },
            },
        }
    },
    computed: {
        image() {
            return this.personaje.sprites;
        },
        movimientos() {
            return this.personaje.moves;
        },
        habilidades() {
            return this.personaje.abilities;
        }
    },
    methods: {
        fetchCharacter() {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.personaje.name}`)
                .then(response => response.json())
                .then(json => {
                    console.log(json);
                    this.personaje = json;
                })
                .catch(error => {
                    alert("No encontrado");
                    console.log(error);
                })
        },
    },
    // components: {},
    created() {
        this.fetchCharacter();
    }
}
</script>

<style scoped>
.lista {
    column-count: 6;
}
</style>
