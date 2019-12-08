<template>
  <div class="container p-5">
    <h1>Nuxt.js Advent Calendar 2019</h1>
    <p>{{ comment }}</p>

    <b-container class="border">
      <b-row>
        <b-col v-for="dayName in dayNames" :key="dayName" class="p-3 bg-info text-light border week">
          <strong>{{ dayName }}</strong>
        </b-col>
      </b-row>

      <b-row>
        <b-col v-for="day in days.slice(0, 7)" :key="day.date" class="p-3 border week">
          <p class="w-100 p-2 alert-info rounded-lg">
            <strong>{{ day.date }}</strong>
          </p>

          <b-img
            :src="day.authorImageUrl"
            width="50"
            :alt="day.authorName"
            class="rounded-lg"
          ></b-img>
          <a
            :href="`https://qiita.com/${day.authorName}`"
            target="_blank"
            rel="noopener noreferrer"
            class="w-100 d-inline-block text-truncate"
          >
            {{ day.authorName }}
          </a>

          <a v-if="day.articleUrl !== null"
            :href="day.articleUrl"
            rel="noopener noreferrer"
          >
            {{ day.comment }}
          </a>
          <p v-else>
            {{ day.comment }}
          </p>
        </b-col>
      </b-row>

      <b-row>
        <b-col v-for="day in days.slice(7, 14)" :key="day.date" class="p-3 border week">
          <p class="w-100 p-2 alert-info rounded-lg">
            <strong>{{ day.date }}</strong>
          </p>

          <b-img
            :src="day.authorImageUrl"
            width="50"
            :alt="day.authorName"
            class="rounded-lg"
          ></b-img>
          <a
            :href="`https://qiita.com/${day.authorName}`"
            target="_blank"
            rel="noopener noreferrer"
            class="w-100 d-inline-block text-truncate"
          >
            {{ day.authorName }}
          </a>

          <a v-if="day.articleUrl !== null"
            :href="day.articleUrl"
            rel="noopener noreferrer"
          >
            {{ day.comment }}
          </a>
          <p v-else>
            {{ day.comment }}
          </p>
        </b-col>
      </b-row>

      <b-row>
        <b-col v-for="day in days.slice(14, 21)" :key="day.date" class="p-3 border week">
          <p class="w-100 p-2 alert-info rounded-lg">
            <strong>{{ day.date }}</strong>
          </p>

          <b-img
            :src="day.authorImageUrl"
            width="50"
            :alt="day.authorName"
            class="rounded-lg"
          ></b-img>
          <a
            :href="`https://qiita.com/${day.authorName}`"
            target="_blank"
            rel="noopener noreferrer"
            class="w-100 d-inline-block text-truncate"
          >
            {{ day.authorName }}
          </a>

          <a v-if="day.articleUrl !== null"
            :href="day.articleUrl"
            rel="noopener noreferrer"
          >
            {{ day.comment }}
          </a>
          <p v-else>
            {{ day.comment }}
          </p>
        </b-col>
      </b-row>

      <b-row>
        <b-col v-for="day in days.slice(21)" :key="day.date" class="p-3 border week">
          <p class="w-100 p-2 alert-info rounded-lg">
            <strong>{{ day.date }}</strong>
          </p>

          <b-img
            :src="day.authorImageUrl"
            width="50"
            :alt="day.authorName"
            class="rounded-lg"
          ></b-img>
          <a
            :href="`https://qiita.com/${day.authorName}`"
            target="_blank"
            rel="noopener noreferrer"
            class="w-100 d-inline-block text-truncate"
          >
            {{ day.authorName }}
          </a>

          <a v-if="day.articleUrl !== null"
            :href="day.articleUrl"
            rel="noopener noreferrer"
          >
            {{ day.comment }}
          </a>
          <p v-else>
            {{ day.comment }}
          </p>
        </b-col>

        <b-col v-for="date in [26, 27, 28]" :key="date" class="p-3 border text-muted week">
          <p class="p-2">
            <strong>{{ date }}</strong>
          </p>
        </b-col>
      </b-row>
    </b-container>

    <p class="pt-3">
      ※ このページはレスポンシブ対応していません。デスクトップでご覧ください。
    </p>
  </div>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    return {
      comment: root.querySelector('.markdownContent').text,
      dayNames: root.querySelectorAll('.adventCalendarCalendar_dayName').map(dayName => dayName.text),
      days: root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
        const articleUrl = day.querySelector('.adventCalendarCalendar_comment').querySelector('a') ?
          day.querySelector('.adventCalendarCalendar_comment').querySelector('a').attributes['href'] :
          null

        return {
          date: day.querySelector('.adventCalendarCalendar_date').text,
          authorName: day.querySelector('.adventCalendarCalendar_author').text.replace(/\s|&nbsp;/g, ''),
          authorImageUrl: day.querySelector('.adventCalendarCalendar_authorIcon').attributes['src'],
          comment: day.querySelector('.adventCalendarCalendar_comment').text,
          articleUrl: articleUrl
        }
      })
    }
  }
}
</script>

<style>
.week {
  width: calc(100% / 7);
}
</style>
