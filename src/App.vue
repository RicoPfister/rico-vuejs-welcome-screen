<template>
  <div id="app">
    
    <h1 :style=heading>{{ title }}</h1>
    <h1 :style=date>{{ date_function }}</h1>

    <p>{{ entries }}</p>

    <div :style='[entryContainer, entrySeparator]'>
    
      <h1 :style=entryTime>8:30 Uhr</h1>
      <h1 :style=entryTitle>Projekt Start: Welcome Screen</h1>
      <p :style=entryContent>Das Layout und das Design des Welcome Screens wird umgesetzt</p>

    </div>

    <div :style='[entryContainer, entrySeparator]'>
    
      <h1 :style=entryTime>8:30 Uhr</h1>
      <h1 :style=entryTitle>Projekt Start: Welcome Screen</h1>
      <p :style=entryContent>Das Layout und das Design des Welcome Screens wird umgesetzt</p>

    </div>

    <div :style='[entryContainer, entrySeparator]'>
    
      <h1 :style=entryTime>8:30 Uhr</h1>
      <h1 :style=entryTitle>Projekt Start: Welcome Screen</h1>
      <p :style=entryContent>Das Layout und das Design des Welcome Screens wird umgesetzt</p>

    </div>
    
    <div :style=logoBar>
    
    <img :src=logo1 alt="Logo1" :style='{ height: assetHeight }'>
    <img :src=logo2 alt="Logo2" :style='{ height: assetHeight }'>
    <img :src=logo3 alt="Logo3" :style='{ height: assetHeight }'>

    </div>         

  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  data(){
    return {
      sheet_id: "1a81aI0Y8ViZO0tI92h2YSMqVQJ8hmNNMyMylXgvwiU4",
      api_token: "AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU",
      entries: [],
      title: 'Welcome to Opportunity',
      logoBar: {
          display: 'flex',
          'justify-content': 'space-between',
          background: 'white',
          width: '1000px',
          position: 'fixed',
          bottom: '0',
      },
      justifyContentBetween: 'space-between',
      alignContent: 'space-between',
      containerWidth: '1000px',
      logo1: require('../src/assets/STZH_SEB_Logo.png'),
      logo2: require('../src/assets/Opportunity.png'),
      logo3: require('../src/assets/SAG_Logo_De.png'),
      assetHeight: '50px',
      backgroundWhite: 'white',
      heading: {
      'font-weight': '900',
      color: '#323D4A',
      'font-size': '62px',
      padding: 0,
      margin: 0,      
      },
      date: {
      'font-weight': '500',
      color: '#9AA7B1',
      'font-size': '62px',
      padding: '40px 0',
      margin: 0,
      },
      entryContainer: {
      background: '#0F05A0',
      'padding-top': '28px',
      'padding-left': '30px',
      width: '970px',
      height: '130px',
      },
      entrySeparator: {
        'margin-bottom': '20px',
      },
      entryTime: {
      'font-weight': '900',
      color: '#EB5E00',
      'font-size': '28px',
      padding: 0,
      margin: 0,
      },
      entryTitle: {
      'font-weight': '900',
      color: '#FFBFAB',
      'font-size': '28px',
      padding: 0,
      margin: 0,
      },
      entryContent: {
      'font-weight': '500',
      color: '#FFBFAB',
      'font-size': '28px',
      padding: 0,
      margin: 0,
      },           
    }
  },

  methods: {

    getData() {
      axios.get(this.gsheet_url).then((response) => {
        this.entries = response.data.valueRanges[0].values;
        this.entries.push('test123');
      });

      
    }
  },

  computed:{

    date_function: function () {

      const today = new Date();
      const date = today.getDate() + '.' + (today.getMonth()+1) + '.' + today.getFullYear();
      return date;     
    },

    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    },
  },

  mounted() {
    this.getData();
  }
}
</script>

<style>
#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  margin-top: 37px;
  margin-left: 30px;    
  }

body, html {
  background: #E8EFF4;
  height:'200px';
}
</style>
