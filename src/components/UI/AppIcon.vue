<template>
    <div class="icon">
        <img :src="src" :class="class">
    </div>
</template>

<script>
export default {
    name: 'app-icon',
    props: {
        src: {
            type: String,
            required: true
        },
        class: {
            type: String, 
            required: false,
            default: 'small'
        }
    }
}
</script>

<style scoped>
.large {
    width: 100%;
    max-width: 200px;
}
.small {
    width: 40px;
}

@media screen and (max-width: 767px) {
    .large {
    max-width: 150px;
    }

    .small {
    width: 30px;
    }

}
</style>