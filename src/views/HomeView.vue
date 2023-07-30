
<template>
  <main>
    <h1>HomePage</h1>
    <div class="news-list">
      <ul>
        <li v-for="(news, index) in newsList" :key="index" class="news-item">
          <div class="news-banner">

            <router-link :to="`/article/${news.slug}`" class="news-link">
              <img :src="getCompleteImageUrl(news.banner)" alt="News Banner">
            </router-link>
          </div>
          <div class="news-content">
            <div class="news-title">{{ news.title }}</div>
            <div class="news-date">{{ news.date_time_created }}</div>
          </div>
        </li>
      </ul>
    </div>
  </main>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      newsList: [],
      api_main_url: 'https://tech-bytes.onrender.com',
    };
  },
  mounted() {
    this.fetchNewsData();
    setInterval(() => {
      this.fetchNewsData();
    }, 60 * 1000);
  },
  methods: {
    fetchNewsData() {
      const apiUrl = 'https://tech-bytes.onrender.com/news/get-articles'; // Replace this with your actual API endpoint
      axios.get(apiUrl)
        .then(response => {
          this.newsList = response.data['articles'];
        })
        .catch(error => {
          console.error('Error fetching news data:', error);
        });
    },
    getCompleteImageUrl(fileName) {
      return this.api_main_url + fileName;
    },
    // createArticleLink(slug) {
    //   console.log(slug);
    //   return this.api_main_url + "/" + slug;
    // },
  },
};
</script>

<style>
.news-list {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.news-item {
  border-bottom: 1px solid #ccc;
  padding: 10px;
}

.news-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 5px;
}

.news-date {
  color: #666;
  font-size: 14px;
}

.news-content {
  margin-top: 5px;
}

.news-banner {
  max-width: 100%;
  overflow: hidden;
  border-radius: 4px;
  margin-bottom: 10px;
}

.news-banner img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
}

.news-item {
  list-style: none;
  /* Remove list dots */
}

.news-item {
  margin-bottom: 20px;
  /* Add some spacing between news items */
}

.news-link {
  text-decoration: none;
  /* Remove default link underline */
  color: #333;
  /* Change link color if needed */
}

.news-banner {
  max-width: 100%;
  overflow: hidden;
  border-radius: 4px;
  margin-bottom: 10px;
}

.news-banner img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
}
</style>