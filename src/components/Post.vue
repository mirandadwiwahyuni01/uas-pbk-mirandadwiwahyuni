<template>
    <div class="container">
      <h2>Post</h2>
      <select v-model="selectedUser" @change="fetchPosts" class="select-user">
        <option value="">Select User</option>
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
      <ul v-if="posts.length" class="post-list">
        <li v-for="post in posts" :key="post.id" class="post-item">
          <h3>{{ post.title }}</h3>
          <p>{{ post.body }}</p>
        </li>
      </ul>
      <p v-else-if="selectedUser" class="no-posts">No posts available for this user</p>
      <p v-else class="no-posts">No posts available</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const users = ref([]);
  const selectedUser = ref('');
  const posts = ref([]);
  
  const fetchUsers = async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await response.json();
    users.value = data;
  };
  
  const fetchPosts = async () => {
    if (!selectedUser.value) return;
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
    const data = await response.json();
    posts.value = data;
  };
  
  onMounted(() => {
    fetchUsers();
  });
  </script>
  
  <style scoped>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #e6c9a9;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 50%;
    margin: auto;
  }
  
  h2 {
    color: #757b32;
    font-family: 'Mulish', sans-serif;
  }
  
  .select-user {
    margin: 20px 0;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #5b6f14;
    font-size: 16px;
    font-family: 'Mulish', sans-serif;
  }
  
  .post-list {
    list-style-type: none;
    padding: 0;
    width: 100%;
  }
  
  .post-item {
    background-color: #e3c5c5;
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 20px;
    margin: 10px 0;
    transition: background-color 0.3s;
  }
  
  .post-item:hover {
    background-color: #9bc6e9;
  }
  
  .no-posts {
    color: #888;
    font-family: 'Mulish', sans-serif;
  }
  </style>
  