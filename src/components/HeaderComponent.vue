<script>
    import axios from 'axios';

    export default {
        name: "HeaderComponent",
        data() {
            return {
                randomFact: null,
            }
        },
        methods: {
            getRandomFact() {
                    axios
                        .get('https://api.chucknorris.io/jokes/random')
                        .then((response) => {
                            this.randomFact = response.data && response.data.value;
                        })
                        .catch((error) => {
                            console.error(error);
                        });
                },
        }
    }
</script>

<template>
    <header>
        <nav class="navbar navbar-expand-lg bg-body-tertiary py-3">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">
                    <h2 class="m-0 p-0 text-warning">
                        Chuck Facts
                    </h2>
                </a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse justify-content-end" id="navbarNavAltMarkup">
                <div class="navbar-nav">
                    <button type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal"
                    @click="getRandomFact()"
                    >
                        Random Fact
                    </button>
                </div>
                </div>
            </div>
        </nav>
    </header>

    <!-- Button trigger modal -->
    

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
            <div class="modal-header">
                <h1 class="modal-title fs-5" id="exampleModalLabel">Chuck Fact</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <p>
                    {{ randomFact }}
                </p>
                <div class="row justify-content-center py-5">
                <div class="col-12 text-center">
                    <img src="chuck.png" alt="" class="w-50">
                </div>
            </div>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    .container-fluid {
        width: 80%;
    }
    @media screen and (max-width: 992px) {
        .container-fluid {
            width: 100%;
        }
    }
</style>