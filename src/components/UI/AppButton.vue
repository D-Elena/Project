<template>
    <button class="button">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'app-button'
}
</script>

<style scoped>
.button {
    display: block;
    margin: auto;
    padding: 10px 15px;
    border-radius: 10px;
    font-family: 'Courier New', Courier, monospace;
    font-size: 20px;
    color: #fff;
    font-weight: bold;
    cursor: pointer;
    border: none;
    box-shadow: 0px 0px 8px rgba(0,0,0,.25);
    background: -webkit-linear-gradient(0deg, #7c6c99,#50acda,#59e9de);
    background: linear-gradient(0deg, #7c6c99,#50acda,#59e9de);
}

.button:hover {
    transform: scale(1.1);
    transition: all .3s ease;
}
</style>