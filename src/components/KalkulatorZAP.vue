<template>
    <div class="container mt-5">
      <h1 class="mb-4">Kalkulator Zapotrzebowania Kalorycznego</h1>
  
      <div class="form-group">
        <label for="age">Wiek:</label>
        <input v-model.number="age" id="age" type="number" class="form-control" />
      </div>
  
      <div class="form-group">
        <label for="gender">Płeć:</label>
        <select v-model="gender" id="gender" class="form-control">
          <option value="male">Mężczyzna</option>
          <option value="female">Kobieta</option>
        </select>
      </div>
  
      <div class="form-group">
        <label for="weight">Waga (kg):</label>
        <input v-model.number="weight" id="weight" type="number" class="form-control" />
      </div>
  
      <div class="form-group">
        <label for="height">Wzrost (cm):</label>
        <input v-model.number="height" id="height" type="number" class="form-control" />
      </div>
  
      <div class="form-group">
        <label for="activityLevel">Poziom aktywności fizycznej:</label>
        <select v-model="activityLevel" id="activityLevel" class="form-control">
          <option value="sedentary">Brak aktywności fizycznej</option>
          <option value="light">Światła aktywność (1-3 dni w tygodniu)</option>
          <option value="moderate">Średnia aktywność (3-5 dni w tygodniu)</option>
          <option value="active">Aktywność intensywna (6-7 dni w tygodniu)</option>
          <option value="veryActive">Bardzo intensywna aktywność (codziennie)</option>
        </select>
      </div>
  
      <button @click="calculateCaloricNeeds" class="btn btn-success">Oblicz Zapotrzebowanie Kaloryczne</button>
  
      <div v-if="caloricNeeds !== null" class="mt-4">
        <h2>Twoje zapotrzebowanie kaloryczne:</h2>
        <p class="mb-2">{{ caloricNeeds.toFixed(2) }} kcal/dzień</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        age: null,
        gender: 'male',
        weight: null,
        height: null,
        activityLevel: 'sedentary',
        caloricNeeds: null,
      };
    },
    methods: {
      calculateCaloricNeeds() {
        if (this.age && this.gender && this.weight && this.height && this.activityLevel) {
          let bmr;
  
          if (this.gender === 'male') {
            bmr = 88.362 + (13.397 * this.weight) + (4.799 * this.height) - (5.677 * this.age);
          } else {
            bmr = 447.593 + (9.247 * this.weight) + (3.098 * this.height) - (4.330 * this.age);
          }
  
          switch (this.activityLevel) {
            case 'sedentary':
              this.caloricNeeds = bmr * 1.2;
              break;
            case 'light':
              this.caloricNeeds = bmr * 1.375;
              break;
            case 'moderate':
              this.caloricNeeds = bmr * 1.55;
              break;
            case 'active':
              this.caloricNeeds = bmr * 1.725;
              break;
            case 'veryActive':
              this.caloricNeeds = bmr * 1.9;
              break;
            default:
              this.caloricNeeds = null;
              break;
          }
        }
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
  