<script>
import passwordunhide from "../components/passwordHide.vue";

export default {
    components: { passwordunhide },
    data() {
        return {
            //icons or images
            dog: require('@/assets/images/animalshelterdog.png'),
            // for password hide
            passwordError: false,
            showPassword: false,
            // Multiple Images
            files: [],
            otherPhotos: null

        }
    },
    methods: { // navigation na dele mo load
        navigateTo(path) {
            this.$router.push(path);
        },
        // For Multiple Images
        handleMultipleFileChange(event) {
            const filesArray = event.target.files
            for (let i = 0; i < filesArray.length; i++) {
                const file = filesArray[i]
                const reader = new FileReader()
                reader.onload = (event) => {
                    this.files.push({ source: file.name, url: event.target.result })
                }
                reader.readAsDataURL(file)
            }
        },
        removeImage(index) {
            this.files.splice(index, 1)
        }
    },
}
</script>

<template>
    <div class="w-full h-screen flex items-center justify-center">
        <div class="border w-screen md:flex md:items-center">
            <div class="w-screen sm:p-[2rem] md:p-[3rem] lg:p-[4rem] xl:p-[7rem]">
                <form action="">
                    <div class="mb-20 sm:text-[10.9px] md:text-[13px] lg:text-[15px]">
                        <router-link to="/" class="flex items-center">
                            <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 19l-7-7 7-7" />
                            </svg>
                            <span class="text-gray-700 sm:pl-[10px]">Back</span>
                        </router-link>
                    </div>
                    <div
                        class="field grid font-medium sm:text-[10px] sm:pt-5 sm:space-y-2 md:text-[12px] md:space-y-3 lg:text-[15px]">
                        <label for="sheltername">Shelter Name </label>
                        <input type="text" id="sheltername" placeholder="Shelter Name"
                            class="border rounded-lg py-2 px-5">
                    </div>
                    <div
                        class="field grid font-medium sm:text-[10px] sm:pt-5 sm:space-y-2 md:text-[12px] md:space-y-3 lg:text-[15px]">
                        <label for="email">Email </label>
                        <input type="text" id="email" placeholder="Email" class="border rounded-lg py-2 px-5">
                    </div>
                    <div
                        class="field font-medium grid sm:text-[10px] sm:pt-5 sm:space-y-2 md:text-[12px] md:space-y-3 lg:text-[15px]">
                        <passwordunhide />
                    </div>
                    <div class="mt-[1rem]">
                        <label for="otherPhotos" class="font-medium sm:text-[10px] md:text-[12px] lg:text-[15px]">Upload
                            Documents</label>
                        <div class="px-[1rem] py-[1rem]">
                            <div class="px-4 sm:col-span-2 sm:px-0">
                                <ul role="list"
                                    class="grid grid-cols-2 gap-x-4 gap-y-8 sm:grid-cols-3 sm:gap-x-6 lg:grid-cols-4 xl:gap-x-8">
                                    <li v-for="(file, index) in files" :key="file.source" class="relative">
                                        <div
                                            class="group aspect-h-7 aspect-w-10 block w-full overflow-hidden rounded-lg bg-gray-100 focus-within:ring-2 focus-within:ring-teal-500 focus-within:ring-offset-2 focus-within:ring-offset-gray-100">
                                            <img :src="file.url" alt="" class="pointer-events-none object-cover" />
                                            <button @click="removeImage(index)"
                                                class="absolute top-0 right-0 p-1 text-gray-600 hover:text-red-600">
                                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                                                    stroke="currentColor" stroke-width="2" class="w-4 h-4">
                                                    <path stroke-linecap="round" stroke-linejoin="round"
                                                        d="M6 18L18 6M6 6l12 12" />
                                                </svg>
                                            </button>
                                        </div>
                                    </li>
                                </ul>
                            </div>
                            <div class="mt-3">
                                <label for="otherPhotos" class="cursor-pointer flex items-center gap-x-2">
                                    <input type="file" multiple @change="handleMultipleFileChange" id="otherPhotos"
                                        ref="otherPhotos" class="hidden" />
                                    <img width="24" height="24"
                                        src="https://img.icons8.com/fluency/48/stack-of-photos.png"
                                        alt="stack-of-photos" />
                                    <span
                                        class="font-medium text-gray-700 sm:text-[10px] md:text-[12px] lg:text-[15px]">Add
                                        more documents</span>
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="flex justify-center mt-[3rem]">
                        <button @click="navigateTo('')"
                            class="px-6 bg-slate-900 rounded-lg p-2 text-white w-full sm:text-[10px] md:text-[12px] lg:text-[15px]">
                            Register
                        </button>
                    </div>
                </form>
            </div>
            <div
                class="flex bg-sky-50 pt-[3rem] px-[3rem] sm:hidden md:hidden lg:pl-[3rem] md:pt-[5rem] lg:block lg:pt-[8rem] xl:pl-[7rem]">
                <img :src="dog" alt="animalshelterdog" class="lg:w-[1950px] xl:w-[1550px]">
            </div>
        </div>
    </div>
</template>
