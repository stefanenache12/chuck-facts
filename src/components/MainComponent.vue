<script>
    import axios from 'axios';

    export default {

        name: "MainComponent",
        
        data() {
            return {
                categories: [],
                facts: [],
                chuckPng: true,
                fact: null,
            }
        },

        created () {
            this.getCategories();
        },

        methods: {

            getCategories() {
                axios
                    .get('https://api.chucknorris.io/jokes/categories')
                    .then((response) => {
                        this.categories = response.data;
                    })
                    .catch((error) => {
                        console.error(error);
                    });
            },

            async getFacts(category) {
                //Inizia la chiamata con Facts[] vuoto
                this.facts = [];
                this.chuckPng = false;
                while (this.facts.length < 4) {
                    let response = await axios.get(`https://api.chucknorris.io/jokes/random?category=${category}`);
                    this.fact = response.data && response.data.value;
                    if (!this.facts.includes(this.fact) && this.facts.length < 4) {
                        this.facts.push(this.fact);
                    }
                }
            },

        }
    }
</script>

<template>
    <main>
        <div class="container py-5">

            <h1 class="py-2 text-center ">
                Choose a category to see the best Chuck Noris facts!
            </h1>

            <div class="accordion py-2" id="accordionExample">
                <div class="accordion-item text-center">
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                        <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
                            Categories
                        </button>
                        </h2>
                        <div id="collapseTwo" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
                        <div class="accordion-body">
                            <div class="row gx-2 justify-content-center">
                                <div class="col-5 col-md-4 col-lg-3" v-for="category in categories">
                                    <button class="btn btn-primary mb-2" @click="getFacts(category)">
                                        {{ category }}
                                    </button>
                                </div>
                            </div>
                        </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col-12 col-md-6 col-lg-3 py-3" v-for="fact in facts">
                    <div class="card">
                        <div class="card-body">
                            {{ fact }}
                        </div>
                    </div>
                </div>
            </div>

            <div class="row justify-content-center py-5" v-if="chuckPng">
                <div class="col-12 text-center">
                    <img src="chuck.png" alt="" class="w-25">
                </div>
            </div>

        </div>
    </main>
</template>

<style lang="scss" scoped>
@use "../assets/scss/partials/variables.scss" as *;

    .container {
        width: 80%;
        margin: auto;

        .btn {
            width: 80px;
        }
    }
    @media screen and (max-width: 992px) {
        .container {
            width: 100%;
        }
    }
</style>