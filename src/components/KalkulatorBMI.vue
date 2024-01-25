<template>
    <div class="container mt-5">
      <h1 class="mb-4">Kalkulator BMI</h1>
  
      <div class="form-group">
        <label for="weight">Waga (kg):</label>
        <input v-model.number="weight" id="weight" type="number" class="form-control" />
      </div>
  
      <div class="form-group">
        <label for="height">Wzrost (cm):</label>
        <input v-model.number="height" id="height" type="number" class="form-control" />
      </div>
  
      <button @click="calculateBMI" class="btn btn-success">Oblicz BMI</button>
  
      <div v-if="bmi !== null" class="mt-4">
        <h2>Twoje BMI:</h2>
        <p class="mb-2">{{ bmi.toFixed(2) }}</p>
        <p>{{ getBMICategory(bmi) }}</p>
  
        <!-- Dodane szczegóły BMI -->
        <div v-if="showDetails" class="mt-3">
          <h3>Szczegóły:</h3>
          <p>{{ getBMIDetails(bmi) }}</p>
        </div>
        <router-link v-if="bmi > 29.9" to="/a" class="btn btn-danger mt-3">
        Przejdź do strony dla BMI > 29.9
      </router-link>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        weight: null,
        height: null,
        bmi: null,
        showDetails: false,
      };
    },
    methods: {
      calculateBMI() {
        if (this.weight && this.height) {
          const heightInMeters = this.height / 100;
          this.bmi = this.weight / (heightInMeters * heightInMeters);
          this.showDetails = true; // Pokaż szczegóły po obliczeniu BMI
        }
      },
      getBMICategory(bmi) {
        if (bmi < 18.5) return 'Niedowaga';
        else if (bmi < 24.9) return 'W normie';
        else if (bmi < 29.9) return 'Nadwaga';
        else return 'Otyłość';
      },
      getBMIDetails(bmi) {
        if (bmi < 18.5)
          return 'Masz niedowagę. Zalecamy skonsultowanie się z lekarzem w celu ustalenia odpowiednich działań.';
        else if (bmi < 24.9) return 'Twoja waga jest w normie. Tak trzymaj!';
        else if (bmi < 29.9) return this.$router.push('/a'), 'Masz nadwagę. Zalecamy skonsultowanie się z lekarzem w celu ustalenia odpowiednich działań.';
        else return this.$router.push('/a'), 'Masz otyłość. Skonsultuj się z lekarzem w celu ustalenia odpowiednich działań.';
      },
    },
  };
  
  </script>
  
  <style scoped>
  @import '~bootstrap/dist/css/bootstrap.min.css';
  
  .container {
    max-width: 400px;
  }
  
  h1 {
    color: #28a745;
  }
  
  .btn-success {
    background-color: #28a745;
    border-color: #28a745;
  }
  
  .btn-success:hover {
    background-color: #218838;
    border-color: #1e7e34;
  }
  </style>
  