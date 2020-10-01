<template>
  <form class="body">
    <div class="column-left">
      <div class="column-group">
        <label for="INSS">INSS:</label>
        <input readonly v-model="inss" name="inss" id="INSS"/>
      </div>
      <div class="column-group">
        <label for="IRRF">IRRF:</label>
        <input readonly v-model="irrf" name="irrf" id="IRRF"/>
      </div>
      <div class="column-group">
        <label for="SALARIO_COM_DESCONTOS">Total:</label>
        <input readonly v-model="salarioComDesconto" name="salarioComDesconto" type='number' id="SALARIO_COM_DESCONTOS"/>
      </div>
    </div>

    <div class="column-right">
      <label for="SALARIO">SALARIO:</label>
      <input autofocus @keyup="onKeyPress($event.target.value)" type='number' id="SALARIO"/>
    </div>

  </form>
</template>


<script>
  export default {
    name: 'HelloWorld',
    data (){
      return {
        inss: 0,
        irrf: 0,
        salarioComDesconto: 0,
      }
    },
    methods: {
      onKeyPress: function(salario){
        console.log(salario)
        let inssSubt = 0;
        let irrfSubt = 0;
        let result = 0;

        if(salario <= 1045 ){
          inssSubt = salario * 0.075
        }else if (salario >= 1045.01 && salario <= 2089.60	) {
          inssSubt = salario * 0.09
        }else if (salario >= 2089.61 && salario <= 3134.40) {
          inssSubt = salario * 0.12
        }else if (salario >= 3134.41 && salario >= 6101.06) {
          inssSubt = Math.round((salario * 0.14) * 100) / 100
        }

        if(salario <= 1903.98 ){
          irrfSubt = 0
        }else if (salario >= 1903.99 && salario <= 2826.65	) {
          irrfSubt = salario * 0.075
        }else if (salario >= 2826.66 && salario <= 3751.05) {
          irrfSubt = salario * 0.15
        }else if (salario >= 3751.06 && salario <= 4664.68) {
          irrfSubt = salario * 0.225
        }else if (salario >= 4664.69){
          irrfSubt = Math.round((salario * 0.275) * 100) / 100
        }

        result = salario - irrfSubt - inssSubt;
        this.inss = inssSubt;
        this.irrf = irrfSubt;
        this.salarioComDesconto = Math.round(result * 100) / 100
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.body{
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.column-left{
  display: flex;
  flex-direction: column;
  flex-flow: column wrap;
}

.column-group{
  align-items: flex-start;
}
</style>
