<template>
    <div class="">
        <DashboardGalleryUpload />
    </div>
</template>

<script setup>
definePageMeta({
    middleware: 'auth',
    layout: 'dashboard',
})
useHead({
    title: `Storage Admin | Nomo Render | 3D visualization
studio`,
    meta: [
        {
            name: "description",
            content: `Nomadic Creativity, Timeless Renders, More than just blueprints, it’s about storytelling`,
        },
    ],
});
</script>