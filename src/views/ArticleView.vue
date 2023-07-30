<!-- IndividualArticlePage.vue -->
<template>
  <div class="individual-article-page">
    <h1>{{ article.title }}</h1>
    <p>{{ article.date }}</p>
    <div class="article-banner">
      <img :src="getCompleteImageUrl(article.banner)" alt="Article Banner">
    </div>
    <p>{{ article.content }}</p>
    <!-- Additional details from the API can be displayed here -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      article: {}, // Initialize article as an empty object
      comments: [], // Initialize comments as an empty list
      comment_count: 0, // Initialize comment_count as 0
      likes: 0, // Initialize likes as 0

      api_main_url: 'https://tech-bytes.onrender.com',
    };
  },
  methods: {
    // Method to fetch article data from the API based on the slug
    fetchArticleData(slug) {
      // Replace 'article_api_endpoint' with the actual API endpoint to fetch article data
      fetch(`https://tech-bytes.onrender.com/news/get-article-details/${slug}`)
        .then(response => response.json())
        .then(data => {
          this.article = data.article; // Update the 'article' data with the fetched article data
          this.comments = data.comments; // Update the 'comments' data with the fetched comments data
          this.comment_count = data.comment_count; // Update the 'comment_count' data with the fetched comment_count data
          this.likes = data.likes; // Update the 'likes' data with the fetched likes data
          console.log(this.article);
        })
        .catch(error => {
          console.error('Error fetching article data:', error);
        });
    },
    // Method to get complete image URL
    getCompleteImageUrl(fileName) {
      // Replace with your main URL as needed
      return this.api_main_url + fileName;
    }
  },
  created() {
    // Retrieve the slug from Vue Router's route params
    const slug = this.$route.params.slug;

    // Fetch the article data using the slug
    this.fetchArticleData(slug);
  }
};
</script>

<style>
/* Individual article page styles */
.individual-article-page {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.article-header {
  text-align: center;
  margin-bottom: 20px;
}

.article-header h1 {
  font-size: 24px;
  margin-bottom: 5px;
}

.date {
  color: #777;
}

.article-banner img {
  width: 100%;
  max-height: 300px;
  object-fit: cover;
  border-radius: 4px;
  margin-bottom: 20px;
}

.article-content {
  line-height: 1.6;
}
</style>
