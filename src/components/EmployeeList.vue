<template>
  <div>
    <div class="user-wrapper">
      <ul v-for="user in list" :key="user.id" class="user-card">
        <li><img :src="user.avatar" /></li>
        <li class="bold-text">{{ user.first_name }} {{ user.last_name }}</li>
        <li><a :href="`mailto:${user.email}`" class="text-wrapper">
            <fa icon='envelope' class="mail-icon" />{{ user.email }}
          </a></li>

      </ul>
    </div>

    <div v-if="error">{{ error }}</div>


    <div class="pagination">
      <ul class="page-links">
        <li v-for="page in totalPages" :key="page" :class="{ 'active': page === currentPage }" @click="fetchPage(page)">
          {{ page }}
        </li>
      </ul>
    </div>


  </div>
</template>
  
<script>


export default {
  name: 'EmployeeList',
  data() {
    return {
      list: undefined,
      error: null,
      baseUrl: 'https://reqres.in/api/users',
      currentPage: 1,
      totalPages: null
    };
  },
  mounted() {
    this.fetchPage();
  },
  methods: {
    fetchPage(page) {
      const url = page ? `${this.baseUrl}?page=${page}` : this.baseUrl;
      fetch(url)
        .then((response) => {
          if (!response.ok) {
            throw new Error('Failed to fetch.');
          }
          return response.json();
        })
        .then((data) => {
          this.list = data.data;
          this.currentPage = data.page;
          this.totalPages = data.total_pages;
        })
        .catch((error) => {
          this.error = error.message;
          console.error(error);
        });
    }


  }
};
</script>
  

  
  
  


