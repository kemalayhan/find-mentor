<template>
  <div class="container">
    <ul>
        <li>{{ doc.name }}</li>
        <li><a :href="doc.twitter_handle">Twitter</a></li>
        <li><a :href="doc.github">Github</a></li>
        <li><a :href="doc.linkedin">Linkedin</a></li>
        <li>Interests: {{doc.interests}}</li>
        <li v-if='doc.goals'>Goals: {{doc.goals}}</li>
        <li v-else>Goals: Unspecified</li>
        <li>Mentor: {{doc.mentor}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content, params, error }) {
    const [doc] = await $content('mentees').where({ slug: { $eq: params.slug } }).fetch()
    if (!doc) {
      return error({ statusCode: 404, message: 'Not found' })
    }
    return { doc }
  }
}
</script>
