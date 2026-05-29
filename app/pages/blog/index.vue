<script setup lang="ts">

const { data: posts } = await useAsyncData('blog-list', () =>
  queryCollection('blog')
    .order('date', 'DESC')
    .select('path', 'title', 'description', 'date', 'tags')
    .all()
)

function formatDate(dateStr: string): string {
  return new Date(dateStr).toLocaleDateString(undefined, {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  })
}

useHead({
  title: () => posts.value ? posts.value[0].title : 'Blog',
})
</script>

<template>
  <div>
    <header>
      <h1>Welcome to My Blog</h1>
      <p>
        Sharing insights, stories, and updates on web development, technology,
        and more.   
      </p>
    </header>

    <div>
      <NuxtLink
        v-for="post in posts"
        :key="post.path"
        :to="post.path"
      >
        <div>
          <time :datetime="post.date">
            {{ formatDate(post.date) }}
          </time>
          <h2>{{ post.title }}</h2>
          <p>{{ post.description }}</p>
          <div>
            <span v-for="tag in post.tags" :key="tag">
              {{ tag }}
            </span>
          </div>
        </div>
        <span>Read more</span>
      </NuxtLink>
    </div>
  </div>
</template>