<template>
  <main>
    <section class="flex flex-col items-center self-center justify-center flex-1">
      <h1 class="text-center title">Nuxt — Tailwind Testx — Netlify CMS</h1>
      <h2 class="text-center subtitle">Boilerplate</h2>
    </section>

    <section class="mt-8">
      <h3 class="max-w-5xl mx-auto text-primary-600 dark:text-primary-400">Latest blog post</h3>
      <posts post-type="blog" :amount="1" />
    </section>
  </main>
</template>

<script>export default {
  head() {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
    };
  },
};</script>