<template>
    <div id="main-banner">
        <h1>Monte seu lanche</h1>
    </div>
</template>

<script>
export default {
    name: 'Banner'
}
</script>

<style scoped>
    #main-banner {
        background-image: url('../../public/img/burger.jpg');
        background-position: 0 -250px;
        background-repeat: no-repeat;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background: #222;
        padding: 20px 40px;
        border-radius: 0 20px 20px 0;
    }
</style>