<script setup>
import {ref, onMounted, defineEmits} from "vue"

const observer = ref(null)
const root = ref(null)

const emits = defineEmits(["intersect"])

onMounted(() => {
    observer.value = new IntersectionObserver(([entry]) => {
        if (entry && entry.isIntersecting) {
            emits("intersect")
        }
    })

    observer.value.observe(root.value)
})
</script>

<template>
    <div class="observer h-px w-16 bg-black" ref="root">
        
    </div>
</template>

<style scoped>
/* .observer {
    height: 1px;
    width: 60px;
    background-color: black
} */

</style>