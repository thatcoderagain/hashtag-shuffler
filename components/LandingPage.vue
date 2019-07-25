<template>
    <nb-container class="container">
        <nb-card class="card">
            <nb-h1 class="hash">HASHTAG SHUFFLER</nb-h1>
            <nb-card-item cardBody class="image">
                <image :source="require('./../assets/shuffle.png')" class="card-item-image"/>
            </nb-card-item >
        </nb-card>
    </nb-container>
</template>

<script>
    export default {

    }
</script>

<style scoped>
    .container {
        flex: 1;
        background-color: #41b883;
        padding: 0px 0px 0px 0px;
    }
    .card {
        flex: 1;
        flex-wrap: wrap;
        flex-direction: column;
        background-color: #41b883;
        margin: 0px 0px 0px 0px;
    }
    .hash {
        top: 150px;
        color: #fff;/*#34495e;*/
        font-family: serif;
        font-weight: 800;
        font-size: 72px;
        line-height: 1.5;
        line-height: 80px;
        text-align: center;
        align-items: center;
        justify-content: center;

    }
    .image {
        background-color: #41b883;
        top: 250px;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;
    }
    .card-item-image {
        width: 250px;
        height: 250px;
        border-radius: 40px;
    }
</style>
