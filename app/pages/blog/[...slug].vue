<template>
    <article
        class="prose dark:prose-invert max-w-none prose-pre:bg-white dark:prose-pre:bg-gray-800 prose-pre:text-gray-700 dark:prose-pre:text-gray-300">
        <ContentDoc>
            <template #not-found>
                <h2>Document not found (404)</h2>
                <p>This blog post could not be found</p>
            </template>
            <template v-slot="{doc}">
                <div class="grid grid-cols-6 gap-16">
                    <div :class="{'col-span-6 md:col-span-4': doc.toc, 'col-span-6': !doc.toc}">
                        <ContentRenderer :value="doc"/>
                    </div>
                    <div class="hidden md:col-span-2 md:block not-prose" v-if="doc.toc">
                        <aside class="sticky top-8">
                            <div class="font-semibold mb-2">
                                Table of Contents
                            </div>
                            <nav>
                                <TocLinks :links="doc.body.toc.links" :active-id="activeId"/>
                            </nav>

                        </aside>
                    </div>
                </div>
            </template>


        </ContentDoc>
    </article>
</template>
<script setup>
const activeId = ref(null);
onMounted(() => {
    const callback = (entries) => {
        entries.forEach((entry) => {
            if (entry.isIntersecting) {

                activeId.value = entry.target.id;

            }
        });

    };
    const observer = new IntersectionObserver(callback, {
        root: null,
        threshold: 0.5,
    });
    const elements = document.querySelectorAll("h2, h3");

    for (const element of elements) {
        observer.observe(element);
    }

    onBeforeUnmount(() => {
        for (const element of elements) {
            observer.unobserve(element);
        }
    });

});


</script>