<template>
  <main>
    <h1>Short URL</h1>
    <p>ระบบย่อ url เพียงแค่คุณคลิกเดียวก็ย่อลิ้งค์ได้</p>

    <form @submit.prevent="addUrl">
      <div class="create-new">
        <input v-model="longUrl" type="text" placeholder="place your url-link">
        <button>
          Shorten URL
        </button>
      </div>
    </form>

    <div class="tasks">
      <div v-for="item in links" :key="item" class="task">
        <div class="content" style="cursor: pointer" @click="redirect(item)">
          {{ baseApi }}/{{ item }}
        </div>
        <div class="buttons">
          <button @click="redirect(item)">
            go
          </button>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data () {
    return {
      longUrl: '',
      baseApi: 'https://enigmatic-falls-47772.herokuapp.com',
      links: []
    }
  },
  methods: {
    async addUrl () {
      await axios.post(this.baseApi, { longUrl: this.longUrl })
        .then((response) => {
          this.links.push(response.data.shortUrl)
          this.longUrl = ''
        })
        .catch((error) => { throw error })
    },

    redirect (abc) {
      window.location.href = `${this.baseApi}/${abc}`
    }
  }
}
</script>
