<template>
    <div class="md:my-20 my-10">
        <div class="relative h-fit w-full md:pb-[50px] md:pt-[55px] pt-[40px] pb-[40px] bg-[#FAF8F5]">
            <div class="flex flex-col items-center justify-center md:mb-[30px] mb-0">
                <div class="font-[400] lg:text-[32px] md:text-[25px] text-[16px] md:leading-[150%] text-[#000000]">
                    Who can benefit from
                </div>
                <div
                    class="text-center font-[600] lg:text-[64px] md:text-[50px] text-[30px] md:leading-[150%] text-[#8D7662]">
                    3D Interior Rendering Service?
                </div>
            </div>
            <div class="lg:flex hidden gap-8 items-center justify-center">
                <div class="relative w-full h-[420px] flex justify-center items-center mt-[10rem]">
                    <div v-for="(slide, slideIndex) in orderedSlides" :key="slide.id"
                        class="absolute w-[calc(82.5vw)] max-w-[1200px] rounded-[8px] h-full shadow-[0_4px_13.5px_rgba(0,0,0,0.42)] transition-all duration-300 ease-in-out"
                        :style="{
                            zIndex: slide.zIndex,
                            opacity: 1,
                            transform: `translate(-50%, ${-(slides.length - 1 - slide.zIndex) * 30}px)`,
                        }" :class="['left-1/2']">
                        <div class="flex justify-center items-center h-full bg-white rounded-[8px]">
                            <div class="w-1/2 px-[calc(2vw+1rem)] py-[calc(3vw+1rem)] sm:px-[50px] sm:py-[60px]">
                                <div class="text-[32px] font-semibold text-[#8D7662]">{{ slide.name }}</div>
                                <div class="text-[25px] leading-[200%] font-light text-justify mt-6">{{ slide.desc }}
                                </div>
                            </div>
                            <div class="w-1/2">
                                <NuxtImg format="webp" :src="slide.img" :alt="slide.name"
                                    class="w-full h-[420px] object-cover object-center rounded-[8px]" loading="lazy"
                                    placeholder="/placeholder.jpg" @load="onImageLoad" />
                            </div>
                        </div>
                    </div>
                    <!-- Button Next and Prev -->
                    <div class="z-[10] flex flex-col justify-center items-center absolute top-1/2 -translate-y-1/2"
                        :class="{
                            'gap-[calc(0.5vw+0.5rem)]': true,
                            'md:gap-[calc(1vw+0.75rem)]': true,
                        }" :style="{
                            left: `calc(50% - min(40vw, 600px) - 7rem)`,
                            top: 'calc(50% - 80px)'
                        }">
                        <UButton @click="nextSlide" variant="ghost" id="watch-next-project"
                            class="flex items-center justify-center bg-white hover:bg-white shadow-2xl rounded-full p-[calc(0.75rem+0.5vw)] sm:p-[18px]"
                            :disabled="isAnimating">
                            <Icon id="watch-next-project" name="material-symbols:arrow-upward-rounded"
                                class="size-5 sm:size-6 text-[#8D7662]" />
                        </UButton>
                        <UButton @click="prevSlide" variant="ghost" id="watch-previous-project"
                            class="flex items-center justify-center bg-[#8D7662] disabled:bg-[#947b65] hover:bg-[#8D7662] shadow-2xl rounded-full p-[calc(0.75rem+0.5vw)] sm:p-[18px]"
                            :disabled="isAnimating">
                            <Icon id="watch-previous-project" name="material-symbols:arrow-downward-rounded"
                                class="size-5 sm:size-6 text-white" />
                        </UButton>
                    </div>
                </div>
            </div>

            <!-- Slide for Mobile -->
            <div class="lg:hidden md:block block">
                <div class="relative pt-5 mx-auto">
                    <UCarousel :items="slides" arrows :ui="{
                        item: 'basis-full px-3',
                        arrows: {
                            wrapper: 'flex items-center justify-center md:mt-2 md:gap-[40px] gap-[15px] md:pb-0'
                        }
                    }" ref="carousel">
                        <template #default="{ item }">
                            <div
                                class="flex justify-center w-full md:mx-20 lg:mx-0 mx-0  bg-[#ffffff] rounded-[8px] shadow-[0_4px_4px_rgba(0,0,0,0.25)] mb-10">
                                <div class="">
                                    <div class="w-full md:mb-0 mb-[40px]">
                                        <NuxtImg format="webp" :src="item.img" :alt="item.name"
                                            class="w-full md:h-[380px] lg:h-[280px] h-[280px] rounded-[8px] object-cover object-center"
                                            draggable="false" />
                                    </div>
                                    <div class="md:mx-10 lg:mx-5 mx-5 md:mt-10 lg:mt-0 mt-0 flex gap-5">
                                        <div>
                                            <div
                                                class="md:text-[30px] lg:text-[18px] text-[18px] text-[#8D7662] font-[600]">
                                                {{ item.name }}
                                            </div>
                                        </div>
                                    </div>
                                    <div class="md:mx-10 lg:mx-5 mx-5 mt-[15px] mb-[35px]">
                                        <div
                                            class="text-justify md:text-[25px] lg:text-[15px] text-[15px] leading-[180%] font-[300]">
                                            {{ item.desc }}
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </template>
                        <template #prev="{ onClick, disabled }">
                            <UButton :disabled="disabled" id="watch-previous-project"
                                class="shadow-[0_4px_4px_rgba(0,0,0,0.25)] !ring-0 !focus:ring-0 !focus-visible:ring-0 rounded-full outline-none border-0 bg-[#FFFFFF] hover:bg-white text-[#8D7662] text-2xl p-2 md:h-[80px] md:w-[80px] h-[41px] w-[41px] flex items-center justify-center"
                                color="white" @click="onClick" square>
                                <UIcon id="watch-previous-project" name="mingcute:arrow-left-fill"
                                    class="md:size-10 size-5" />
                            </UButton>
                        </template>
                        <template #next="{ onClick, disabled }">
                            <UButton :disabled="disabled" id="watch-next-project"
                                class="shadow-[0_4px_4px_rgba(0,0,0,0.25)] !ring-0 !focus:ring-0 !focus-visible:ring-0 rounded-full outline-none border-0 bg-[#8D7662] disabled:text-[#8D7662] hover:bg-[#8D7662] text-[#FFFFFF] p-2 md:h-[80px] md:w-[80px] h-[41px] w-[41px] flex items-center justify-center"
                                color="white" @click="onClick" square>
                                <UIcon id="watch-next-project" name="mingcute:arrow-right-fill"
                                    class="md:size-10 size-5" />
                            </UButton>
                        </template>
                    </UCarousel>
                </div>
            </div>

            <div class="flex justify-center items-center md:pt-[70px] pt-[25px]">
                <div
                    class="md:w-[calc(80vw)] md:max-w-[1200px] md:text-[25px] text-[15px] font-[300] md:leading-[200%] leading-[180%] text-justify md:px-0 px-9">
                    With the right 3D interior rendering, you’re not just imagining a space, you’re <span
                        class="font-[500]">experiencing</span> it.
                    From concept to
                    completion, these tools help <span class="font-[500]">make every detail shine, ensuring your vision
                        is seen,
                        understood, and
                        loved.</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const slides = ref([
    {
        id: 1,
        name: 'Architects & Designers',
        desc: 'A great design deserves a great presentation! Interior renderings help convey concepts clearly, ensuring clients and stakeholders see the full potential of a space before construction even begins.',
        img: '/Interior/Pic43.png',
        zIndex: 4,
    },
    {
        id: 2,
        name: 'Real Estate Developers',
        desc: 'Showcasing an empty property with high-quality interior renderings help buyers and investors picture a fully furnished, stylish space, making properties more appealing and easier to sell.',
        img: '/Interior/Pic41.jpg',
        zIndex: 3,
    },
    {
        id: 3,
        name: 'Construction & Engineering Agency',
        desc: 'Accuracy is key when bringing a design to life. Technical renderings provide detailed visuals for material selection, layout planning, and seamless execution, reducing costly errors along the way.',
        img: '/Interior/Pic44.jpg',
        zIndex: 2,
    },
    {
        id: 4,
        name: 'Marketing & Advertising Prof',
        desc: 'Beautiful interiors deserve stunning visuals! Whether for real estate promotions, hotel brochures, or digital campaigns, 3D renderings create eye-catching content that draws in potential buyers and guests.',
        img: '/Interior/Pic42.jpg',
        zIndex: 1,
    },
    {
        id: 5,
        name: 'Entertainment & Hospitality Industry',
        desc: 'From movie sets to luxury hotels, 3D renderings turn creative visions into reality - an essential tool for travel, events, and production teams.',
        img: '/services/4.png',
        zIndex: 0,
    },
]);

const isAnimating = ref(false);
const imagesLoaded = ref(false);

const orderedSlides = computed(() => {
    return [...slides.value].sort((a, b) => b.zIndex - a.zIndex);
});

const nextSlide = () => {
    if (isAnimating.value || !imagesLoaded.value) return;
    isAnimating.value = true;

    const maxZIndexSlide = slides.value.find((slide) => slide.zIndex === slides.value.length - 1);
    maxZIndexSlide.zIndex = 0;
    slides.value.forEach((slide) => {
        if (slide.id !== maxZIndexSlide.id) {
            slide.zIndex += 1;
        }
    });

    setTimeout(() => {
        isAnimating.value = false;
    }, 300);
};

const prevSlide = () => {
    if (isAnimating.value || !imagesLoaded.value) return;
    isAnimating.value = true;

    const minZIndexSlide = slides.value.find((slide) => slide.zIndex === 0);
    minZIndexSlide.zIndex = slides.value.length - 1;
    slides.value.forEach((slide) => {
        if (slide.id !== minZIndexSlide.id) {
            slide.zIndex -= 1;
        }
    });
    setTimeout(() => {
        isAnimating.value = false;
    }, 300);
};

const onImageLoad = () => {
    imagesLoaded.value = true;
};
</script>