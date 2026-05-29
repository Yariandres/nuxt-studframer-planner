<script setup lang="ts">
const route = useRoute()

const { data: post } = await useAsyncData(`blog-${route.path}`, () =>
  queryCollection('blog').path(route.path).first()
)

if (!post.value) {
  throw createError({ statusCode: 404, statusMessage: t('blog.postNotFound') })
}

function formatDate(dateStr: string): string {
  return new Date(dateStr).toLocaleDateString(undefined, {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  })
}

useHead({
  title: post.value?.title,
})
</script>

<template>
  <article v-if="post" >
    <div class="post-container">
      <NuxtLink :to="'/blog'" >
          back to blog
      </NuxtLink>

      <header >
        <div>
          <time :datetime="post.date">
            {{ post.date }}
          </time>
          <div>
            <span v-for="tag in post.tags" :key="tag">
              {{ tag }}
            </span>
          </div>
        </div>
        <h1>{{ post.title }}</h1>
        <p>{{ post.description }}</p>
      </header>

      <div>
        <ContentRenderer :value="post" />
      </div>
    </div>
  </article>
</template>