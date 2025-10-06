<script setup lang="ts">
import { definePageMeta, useRoute, useI18n } from '#imports'

const { $getLocale, $switchLocale, $getLocales, $t } = useI18n()

definePageMeta({
  name: 'custom-routes',
  alias: ['/:slug/:name/:id/'],
})

const route = useRoute()
const { slug, name, id } = route.params
</script>

<template>
    <h1>
      Custom routes with definePageMeta alias
    </h1>
    <p>Current Locale: {{ $getLocale() }}</p>
    <p>Translated string: {{ $t('lang') }}</p>

    <p>Route params:</p>
    <ul>
      <li>slug: <strong>{{ slug }}</strong></li>
      <li>name: <strong>{{ name }}</strong></li>
      <li>id: <strong>{{ id }}</strong></li>
    </ul>

    <hr />
    <p>$switchLocale ignores other parts of path</p>
    <div>
      <button
        v-for="locale in $getLocales()"
        :key="locale.code"
        :disabled="locale.code === $getLocale()"
        @click="() => $switchLocale(locale.code)"
      >
        Switch to {{ locale.code }}
      </button>
    </div>

    <hr />
    <p>Links to fully localized routes leads to 404</p>
    <div>
      <p
        v-for="locale in $getLocales()"
        :key="locale.code"
      >
        Link to <a :href="`${ locale.code === 'en' ? '': `/${locale.code}`}/custom-routes/page-name/page-id`">full custom route - {{ locale.code }}</a>
      </p>
    </div>


</template>
