<template>
  <div class="wrapper">
    <header-bg image="favorites" />
    <div class="wrapper__content">
      <section class="favorite">
        <div class="container">
          <div class="row">
            <div class="col-md-8 offset-md-2">
              <h2 class="section__title">Избранное</h2>
              <div class="courses-list">
                <courses-list v-if="courses.length" :courses="courses" />
                <div v-else class="alert alert-info">
                  Вы еще ничего не добавляли в избранное
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import CoursesList from '../../components/courses-list'
import HeaderBg from '../../components/header-bg'

export default {
  auth: true,
  components: {
    'courses-list': CoursesList,
    'header-bg': HeaderBg,
  },
  asyncData({app}) {
    return app.$axios.get('user/favorites', {params: {limit: 0}}).then((res) => {
      return {courses: res.data.rows}
    })
  },
  created() {
    this.$app.header_image.set(true)
  },
  head() {
    return {
      title: 'Крафти / Личный кабинет / Избранное',
    }
  },
}
</script>
