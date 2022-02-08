<template>
    <header class="heading">
        <div class="img-wrapper">
            <img src="../assets/note.svg" alt="Logo of to-do list">
        </div>
        <div class="title">To-do List</div>
    </header>
</template>


<script>
export default {
    data(){
        return {

        }
    }
}
</script>


<style scoped>
    .heading {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .img-wrapper{
        width: 55px;
        margin-right: 10px;
    }

    .title{
        transform: rotate(3deg);
        padding: 0.25em 0.8em 0.15em;
        font-size: 20px;
        border-radius: 20% 5% 20% 5%/25% 20% 25% 20%;
        background: #7395ae;
        color: white;

    }
</style>