<script>
    export const prerender = true;
    import LorenzAttractor from "../LorenzAttractor.svelte";
</script>

<main>
    <h1 class="title">Chaos Theory: Lorenz Attractor</h1>
    <LorenzAttractor />
</main>

<style>
    .title {
        margin-top: 50px;
        margin-bottom: 80px;
        color: #ffffff;
        text-align: center;
    }
</style>
