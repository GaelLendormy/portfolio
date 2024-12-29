<template>
    <div>
        <NuxtLayout>
            <NuxtRouteAnnouncer/>
            <NuxtPage/>
        </NuxtLayout>
    </div>
</template>
<script setup lang="ts">
</script>

<style>
.page-enter-active,
.page-leave-active {
    transition: all 0.5s;
}

.page-enter-from,
.page-leave-to {
    opacity: 0.1;
    filter: grayscale(1);
}

</style>