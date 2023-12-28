<template>
    <div>
      <!-- Sorted Employees -->
      <div class="employee-section">
        <h1>Employee</h1>
        <div class="card theme-card" v-for="employee in sortedEmployees" :key="employee.id">
          <img :src="employee.image" class="card-img-top" alt="">
          <div class="card-body">
            <h5 class="card-title">{{ employee.first_name }} - {{ employee.last_name }} ({{ employee.gender }})</h5>
            <p class="card-text">{{ employee.description }}</p>
          </div>
        </div>
      </div>

      <!-- Filtered Male Employees -->
      <div class="employee-section">
        <h2>แสดงรายชื่อพนักงาน ที่ชื่อขึ้นต้นด้วย ‘A’ และเป็นเพศชาย (50 คน)</h2>
        <div class="card theme-card" v-for="employee in filteredEmployees" :key="employee.id">
          <div class="card-body">
            <p class="card-text">{{ employee.first_name }} {{ employee.last_name }} ({{ employee.gender }})</p>
          </div>
        </div>
      </div>

      <!-- Filtered Female Employees -->
      <div class="employee-section">
        <h2>แสดงรายชื่อพนักงาน หญิง ที่มีอายุมากกว่า 50 ปี</h2>
        <div class="card theme-card" v-for="employee in filteredEmployeesFemale" :key="employee.id">
          <div class="card-body">
            <p class="card-text">{{ employee.first_name }} {{ employee.last_name }} ({{ employee.gender }}) ({{ calculateAge(employee.birth_date) }} years old)</p>
          </div>
        </div>
      </div>
    </div>
  </template>


  <script setup>
  import { defineProps, computed } from 'vue';

  const props = defineProps(['emp']);

  const sortedEmployees = computed(() => {
    return props.emp.sort((a, b) => a.first_name.localeCompare(b.first_name));
  });

  const filteredEmployees = computed(() => {
    return props.emp
      .filter(employee => employee.first_name.startsWith('A') && employee.gender === 'M')
      .slice(0, 50);
  });

  const filteredEmployeesFemale = computed(() => {
    return props.emp
      .filter(employee => employee.gender === 'F' && employee.birth_date);
  });

  const calculateAge = (birthDateString) => {
    const birthDate = new Date(birthDateString);
    const currentDate = new Date();
    const age = currentDate.getFullYear() - birthDate.getFullYear();
    return age;
  };
  </script>

  <style scoped>
  .theme-card {
    background-color: #f8f9fa; /* Light gray background */
    border: 1px solid #dee2e6; /* Light gray border */
    border-radius: 8px; /* Rounded corners */
    margin-bottom: 20px; /* Spacing between cards */
  }

  .card {
    margin-bottom: 20px; /* Spacing between cards */
  }
  </style>
