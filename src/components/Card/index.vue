<script setup lang="ts">
defineProps<{
    expandedCardId: number | null
    card: any
}>()
</script>

<template>
    <div class="group bg-card/40 text-card-foreground rounded-lg shadow-md overflow-hidden cursor-pointer relative transition-all duration-300 ease-in-out border border-border/5 md:hover:border-border/10 md:hover:bg-card/60 md:hover:shadow-xl md:hover:shadow-primary/5"
        :class="[expandedCardId == card.id ? 'row-span-2 col-span-2' : 'pb-10']">
        <div class="card-content h-full md:overflow-visible">
            <div class="p-6 h-full flex flex-col">
                <div class="card-scrollable-content">
                    <div class="flex items-start gap-4">
                        <div class="relative flex-shrink-0">
                            <div
                                class="w-16 h-16 rounded-full overflow-hidden ring-2 ring-gray-300/50 shadow-lg transition-transform duration-200">
                                <img :src="card.image" alt="Aisha's profile" crossorigin="anonymous" loading="lazy"
                                    decoding="async"
                                    class="w-full h-full object-cover transition-opacity duration-300 opacity-100" />
                            </div>
                            <div class="absolute -bottom-1 end-[-0.25rem]">
                                <div class="relative">
                                    <div class="w-5 h-5 rounded-full ring-2 ring-white bg-red-500"
                                        v-if="card.status == 'offline'"></div>
                                    <div class="w-5 h-5 rounded-full ring-2 ring-white bg-green-500"
                                        v-else="card.status == 'online'"></div>
                                    <div
                                        class="absolute end-6 bottom-0 whitespace-nowrap bg-background/60 backdrop-blur-sm px-2 py-1 rounded-full text-xs pointer-events-none transition-all duration-200 border border-border/10 opacity-0 translate-x-2">
                                        غير متواجد
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="flex-1 min-w-0">
                            <div class="flex items-center gap-2">
                                <h3 class="font-bold transition-all duration-300 text-xl">
                                    {{ card.name }}, {{ card.age }}
                                </h3>
                                <span class="px-2 py-1 bg-indigo-200/50 text-indigo-700 rounded-full text-xs">{{
                                    card.gender
                                }}</span>
                            </div>
                            <div class="mt-2 flex items-center text-sm text-muted-foreground">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="lucide lucide-clock w-4 h-4 me-2 flex-shrink-0">
                                    <circle cx="12" cy="12" r="10"></circle>
                                    <polyline points="12 6 12 12 16 14"></polyline>
                                </svg><span class="truncate">{{ card.availability }}</span>
                            </div>
                        </div>
                        <div class="flex-shrink-0">
                            <button title="أبلغني عند التواجد"
                                class="group/btn inline-flex items-center justify-center w-10 h-10 border-2 border-primary text-primary hover:bg-primary hover:text-primary-foreground focus:bg-primary focus:text-primary-foreground rounded-full transition-all duration-200">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="lucide lucide-bell w-5 h-5">
                                    <path d="M6 8a6 6 0 0 1 12 0c0 7 3 9 3 9H3s3-2 3-9"></path>
                                    <path d="M10.3 21a1.94 1.94 0 0 0 3.4 0"></path>
                                </svg>
                            </button>
                        </div>
                    </div>
                    <div class="mt-4 flex flex-wrap gap-1.5">
                        <span class="px-2 py-1 bg-gray-100 text-gray-800 rounded-full text-xs"
                            v-for="(tag, index) in card.tags" :key="index">{{ tag }}</span>
                    </div>
                    <div class="mt-4">
                        <p class="transition-all duration-300 text-sm text-muted-foreground line-clamp-2">
                            {{ card.bio }}
                        </p>
                    </div>
                    <div class="content-transition mt-6 space-y-6 content-collapsed" v-show="expandedCardId == card.id">
                        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                            <div class="bg-gray-100 rounded-lg p-3 text-center border border-gray-100/5">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="lucide lucide-star w-5 h-5 mx-auto mb-2 text-primary">
                                    <polygon
                                        points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2">
                                    </polygon>
                                </svg>
                                <div class="text-sm font-medium text-muted-foreground">Rating</div>
                                <div class="text-lg font-bold text-foreground">{{ card.rating }}</div>
                            </div>
                            <div class="bg-gray-100 rounded-lg p-3 text-center border border-gray-100/5">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="lucide lucide-message-circle w-5 h-5 mx-auto mb-2 text-primary">
                                    <path d="M7.9 20A9 9 0 1 0 4 16.1L2 22Z"></path>
                                </svg>
                                <div class="text-sm font-medium text-muted-foreground">Sessions</div>
                                <div class="text-lg font-bold text-foreground">{{ card.sessions }}+</div>
                            </div>
                            <div class="bg-gray-100 rounded-lg p-3 text-center border border-gray-100/5">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="lucide lucide-heart w-5 h-5 mx-auto mb-2 text-primary">
                                    <path
                                        d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z">
                                    </path>
                                </svg>
                                <div class="text-sm font-medium text-muted-foreground">Helped</div>
                                <div class="text-lg font-bold text-foreground">{{ card.helped }}+</div>
                            </div>
                            <div class="bg-gray-100 rounded-lg p-3 text-center border border-gray-100/5">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="lucide lucide-users w-5 h-5 mx-auto mb-2 text-primary">
                                    <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"></path>
                                    <circle cx="9" cy="7" r="4"></circle>
                                    <path d="M22 21v-2a4 4 0 0 0-3-3.87"></path>
                                    <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
                                </svg>
                                <div class="text-sm font-medium text-muted-foreground">Return Rate</div>
                                <div class="text-lg font-bold text-foreground">{{ card.returnRate }}</div>
                            </div>
                        </div>
                        <div>
                            <h4 class="text-sm font-semibold text-foreground/80 mb-2 flex items-center gap-2">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                    stroke-linejoin="round" class="lucide lucide-calendar w-4 h-4">
                                    <path d="M8 2v4"></path>
                                    <path d="M16 2v4"></path>
                                    <rect width="18" height="18" x="3" y="4" rx="2"></rect>
                                    <path d="M3 10h18"></path>
                                </svg>
                                Available
                            </h4>
                            <div class="grid grid-cols-2 md:grid-cols-3 gap-2">
                                <div class="bg-gray-200 rounded-lg p-2 text-sm border border-gray-100/5"
                                    v-for="([day, hours], index) in Object.entries(card.weekAvailability)" :key="index">
                                    <span class="font-medium">{{ day }}:</span> {{ hours }}
                                </div>
                            </div>
                        </div>
                        <div>
                            <h4 class="text-sm font-semibold text-foreground/80 mb-2">Languages</h4>
                            <div class="flex flex-wrap gap-1.5">
                                <span class="px-2 py-1 bg-gray-100 rounded-full text-xs border border-gray-100/5"
                                    v-for="(lang, index) in card.languages" :key="index">{{ lang }}</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <button
            class="absolute bottom-3 end-3 w-10 h-10 rounded-full bg-background/60 backdrop-blur-sm flex items-center justify-center transition-all duration-200 hover:bg-background hover:shadow-md focus:outline-none focus:ring-2 focus:ring-primary border border-border/10">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                class="lucide lucide-maximize2 w-5 h-5 text-foreground/60 group-hover:text-foreground">
                <polyline points="15 3 21 3 21 9"></polyline>
                <polyline points="9 21 3 21 3 15"></polyline>
                <line x1="21" x2="14" y1="3" y2="10"></line>
                <line x1="3" x2="10" y1="21" y2="14"></line>
            </svg>
        </button>
    </div>
</template>

<style scoped></style>
