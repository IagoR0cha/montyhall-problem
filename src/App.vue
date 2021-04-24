<template>
  <div id="app">
      <h1>Problema de Monty Hall</h1>
      <div class="form" @keyup.enter="started = true">
          <div v-if="!started">
              <label for="portsAmount">Quantas portas?</label>
              <input type="text" id="portsAmount" size="3" v-model.number="portsAmount">
          </div>
          <div v-if="!started">
              <label for="selectedPort">Qual porta é premiada?</label>
              <input type="text" id="selectedPort" size="3" v-model.number="selectedPort">
          </div>
          <span class="validate" v-if="verify = selectedPort > portsAmount">Porta inválida</span>
          <button v-if="!started" :disabled="verify || !selectedPort" @click="started = true">Iniciar</button>
          <button v-else @click="started = false">Reiniciar</button>
      </div>
      <div class="doors" v-if="started">
          <div v-for="port in portsAmount" :key="port">
              <Door :hasGift="port === selectedPort" :number="port"></Door>
          </div>
      </div>
  </div>
</template>

<script>
import Door from './components/Door'
export default {
    name: 'App',
    components: {
        Door
    },
    data(){
        return{
            started: false,
            portsAmount: 3,
            selectedPort: null,
            verify: true
        }
    }

}
</script>

<style>
*{
    box-sizing: border-box;
    font-family: 'Montserrat', 'sans-serif';
}

body{
    color: #ffffff;
    background: linear-gradient(to right, #7F7FD5, #86A8E7, #91EAE4);
}
#app{
    display: flex;
    flex-direction: column;
    /* align-items: center; */
    
}

h1{
    border: 1px solid #000000;
    background-color: #0004;
    padding: 20px;
    margin-bottom: 60px;
    align-self: center;
}

.form{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 10px;
}

.form, .form input, .form button{
    margin-bottom: 5px;
    font-size: 2rem;
}

.doors{
    display: flex;
    flex-wrap: wrap;
    align-items: stretch;
    justify-content: space-around;
}

.validate{
    color: red;
}
</style>