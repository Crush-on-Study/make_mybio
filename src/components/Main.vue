<template>
    <div>
      <h1>Welcome to My Profile</h1>
      <p>This is my profile page.</p>
      <h2>About Me</h2>
      <p>
        My name is {{ profile.name }}. I have a background in {{ profile.companyHistory }}.
        I attended {{ profile.schoolHistory }}.
      </p>
      <h2>Technical Skills</h2>
      <ul>
        <li v-for="tech in profile.language_techStack" :key="tech">{{ tech }}</li>
      </ul>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref, onMounted } from 'vue';
  import axios from 'axios';
  
  export default defineComponent({
    name: 'Main',
    data() {
      return {
        profile: {
          name: 'Crush-on-Study!',
          companyHistory: 'LG Display',
          schoolHistory: 'Chung Ang Univ Seoul Campus',
          language_techStack: ['Python' , 'C/C++' , 'JavaScript']
        }
      };
    },
    methods: {
      fetchProfileData() {
        axios.get('http://localhost:8080/api/profile') // API 엔드포인트에 맞게 URL을 변경하세요.
          .then(response => {
            this.profile = response.data;
          })
          .catch(error => {
            console.error('Error fetching profile data:', error);
          });
      }
    },
    created() {
      this.fetchProfileData();
    }
  });
  </script>
  