<template>
  <div class="container">
    <div v-if="factories.length > 0">
      <ul>
      <li v-for="(f, index) in factories" :key="index">
        <div class="block">
          <h2>{{ f.CityName || "No City Name" }}</h2>
          <p><b>Цех: </b>{{ f.GildName || "No Gild Name" }}</p>
        </div>
        <div class="block">
          <p><b>{{ f.FullName || "No Full Name" }}</b></p>
          <p><b>Бригада: </b>{{ f.BrigadeName || "No Brigade Name" }}</p>
        </div>
        <div class="block" style="align-items: end;">
          <h3>{{ f.ShiftName || "No Shift Name" }}</h3>
        </div>
      </li>
    </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['factories']
}
</script>

<style>
    .container{
      height: 100%;
    }

    .container ul{
      padding-left: 10px;
      padding-right: 10px;
    }

    .container li{
      display: flex;
      justify-content: space-between;
      list-style-type: none;
      margin: 20px auto;
      padding: 10px 20px;
      border-radius: 5px;
      border: 1px solid black;
    }

    .block{
      width: 30%;
      padding: 10px;
      display: flex;
      flex-direction: column;
    }

    .block h2, p, h2{
      margin: 5px 0;
    }
</style>