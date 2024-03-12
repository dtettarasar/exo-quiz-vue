<template>

    <section class="score">
        Player <span>{{this.playerScore}}</span> x <span>{{this.cpuScore}}</span> Computer
    </section>

</template>

<script>

    export default {
        props: {
            playerScore: Number,
            cpuScore: Number
        }
    }

</script>

<style>

    .score {
        border-bottom: 2px black solid;
        padding: 24px;
        font-size: 20px;
    }

</style>