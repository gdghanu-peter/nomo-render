<script setup lang="ts">
import type { FormError, FormErrorEvent, FormSubmitEvent } from '#ui/types'

const state = reactive({
    name: undefined,
    email: undefined,
    description: undefined
})

const validate = (state: any): FormError[] => {
    const errors = []
    if (!state.email) errors.push({ path: 'email', message: 'Required' })
    if (!state.name) errors.push({ path: 'name', message: 'Required' })
    return errors
}

async function onSubmit(event: FormSubmitEvent<any>) {
    console.log(event.data)
}

// const state = reactive({
//     name: undefined,
//     email: undefined,
//     description: undefined,
//     agree: false
// })

async function onError(event: FormErrorEvent) {
    const element = document.getElementById(event.errors[0].id)
    element?.focus()
    element?.scrollIntoView({ behavior: 'smooth', block: 'center' })
}
</script>

<template>
    <div class="bg-[#D9D9D9] py-10 md:pt-20">
        <div class="md:px-8 flex items-center justify-center">
            <div class="w-[1072px]">
                <div>
                    <p class="text-center text-xl md:text-3xl uppercase">contact</p>
                    <div
                        class="text-center font-semibold text-3xl md:text-[64px] leading-[100%] mb-5 md:mb-20 text-[#8D7662] px-6 md:px-20">
                        Let’s bring your vision to life!
                    </div>
                </div>
                <div class="block lg:flex lg:gap-[100px]">
                    <div class="lg:w-[50%]">
                        <p
                            class="text-justify font-[300] italic text-[15px] md:text-[25px] leading-[180%] md:leading-[150%] px-7 md:px-0 max-w-4xl mx-auto">
                            Have a project in mind? Whether you need stunning 3D renderings, detailed architectural
                            visuals,
                            or custom design solutions, we’re here to help. Contact us, and let’s discuss how we can
                            transform your ideas into reality.
                        </p>
                        <div
                            class="grid grid-cols-2 gap-2 mt-10 place-items-center md:place-items-start w-full px-0 mx-0">
                            <NuxtImg src="/Contact1.png"
                                class="w-full max-w-[190px] h-auto md:max-w-[335px] object-cover" />
                            <NuxtImg src="/Contact2.png"
                                class="w-full max-w-[190px] h-full md:max-w-[335px] object-cover" />
                        </div>
                    </div>

                    <div class="lg:w-[50%] mt-6 lg:mt-0">
                        <UForm id="contactForm" :validate="validate" :state="state" class="space-y-4 px-4 md:px-0"
                            @submit="onSubmit" @error="onError">
                            <UFormGroup>
                                <UInput padded required color="white" variant="none" placeholder="Name (required)"
                                    v-model="state.name" size="xl"
                                    class="bg-[#C6C6C6] px-2 rounded-[8px] shadow-lg w-full"
                                    :ui="{ placeholder: 'placeholder-black font-[300] text-[20px] md:text-[25px] leading-[200%]' }" />
                            </UFormGroup>

                            <UFormGroup>
                                <UInput padded required color="white" variant="none" placeholder="Email (required)"
                                    v-model="state.email" size="xl"
                                    class="bg-[#C6C6C6] px-2 rounded-[8px] shadow-lg w-full"
                                    :ui="{ placeholder: 'placeholder-black font-[300] text-[20px] md:text-[25px] leading-[200%]' }" />
                            </UFormGroup>

                            <UFormGroup>
                                <UTextarea padded required color="white" variant="none"
                                    placeholder="Describe your project" v-model="state.description" size="xl"
                                    class="bg-[#C6C6C6] px-2 rounded-[8px] shadow-lg w-full"
                                    :ui="{ placeholder: 'placeholder-black font-[300] text-[20px] md:text-[25px] leading-[200%]' }"
                                    :rows="10" md:rows="20" />
                            </UFormGroup>

                            <div class="px-4 md:px-0 mx-auto flex justify-center lg:block">
                                <!-- <UCheckbox
                                    label="I agree to the Terms of Use and the Privacy Policy *" required
                                    class="text-[12px] italic lg:text-[20px] text-gray-700 mt-9" /> -->
                                <UButton color="gray" variant="solid" type="submit" form="contactForm"
                                    class="bg-gradient-to-r from-[#8D7662] to-[#27211B] lg:px-8 lg:py-5 px-10 hover:bg-[#90755e] mt-6 lg:mt-8 rounded-[8px] w-[390px] md:w-auto">
                                    <div
                                        class="w-full flex justify-center items-center uppercase text-[#F5F5F5] leading-[16px] text-[16px] md:text-[28px]">
                                        let’s work together!
                                    </div>
                                </UButton>
                            </div>
                        </UForm>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>