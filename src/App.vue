<template>
  <div id="app">

    <div :style="{'margin-left': marginContainer}">
    
      <h1 :style=heading>{{ title }}</h1>
      <h1 :style=date>{{ currentDate }}</h1>
    
          <ul v-if="entries" :style="{'margin-left': marginContainer, 'padding-left': paddingZero}">
            <li :style='[entryContainer, entrySeparator]' v-for="entry in entries" :key='entry'><div :style=entryTime>{{ entry[1].replace(/\//g, '.') }} / {{ entry[0] }}</div><h3 :style=entryTitle>{{ entry[2] }}</h3><div :style=entryContent>{{ entry[3] }}</div></li>
          </ul>

          <div v-else style="padding-left:15px">
            <h1>No database entries.</h1>
            <img :src=warning alt="Warning Sign" style="height: 100px">
          </div>

          <p :style="{'margin-left': marginContainer}">{{ timerMS }}</p>

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
      timerMS: 0,
      warning: require('../src/assets/warning.png'),
      assetHeight: '50px',
      marginContainer: '15px',
      sheet_id: "1hABjKywxfrKfKgygWyDtlKxfZ-ZMolhMXd3uFFKVXxI",
      api_token: "AIzaSyDn0LwBJRiTQHAvvlsn3UHC-Q2WkrZYlcc",
      entries: [],
      title: 'Welcome to Opportunity',
      logoBar: {
          display: 'flex',
          'justify-content': 'space-between',
          background: 'white',
          width: '100%',
          position: 'fixed',
          bottom: '0',
          margin: 0,
      },
      justifyContentBetween: 'space-between',
      alignContent: 'space-between',
      containerWidth: '1000px',
      paddingZero: 0,
      logo1: require('../src/assets/STZH_SEB_Logo.png'),
      logo2: require('../src/assets/Opportunity.png'),
      logo3: require('../src/assets/SAG_Logo_De.png'),
      backgroundWhite: 'white',
      heading: {
        'font-weight': '900',
        color: '#323D4A',
        'font-size': '62px',
        margin: 0,
        'padding-left': '15px',
      },
      date: {
        'font-weight': '500',
        color: '#9AA7B1',
        'font-size': '62px',
        'padding-top': '15px',
        'padding-bottom': '15px',
        'padding-left': '15px',
        margin: 0,
      },
      entryContainer: {
        background: '#0F05A0',
        'padding-left': '30px',
        width: '970px',
        'box-shadow': '15px 10px 10px black',
      },
      entrySeparator: {
        'margin-bottom': '20px',
      },
      entryTime: {
      'font-weight': '900',
      color: '#EB5E00',
      'font-size': '28px',
      margin: 0,
      'padding-top': '20px',
      },
      entryTitle: {
      'font-weight': '900',
      color: '#FFBFAB',
      'font-size': '28px',
      margin: 0,
      },
      entryContent: {
      'font-weight': '500',
      color: '#FFBFAB',
      'font-size': '28px',
      'padding-bottom': '20px',
      },           
    }
  },

  methods: {

    getData() {
      axios.get(this.gsheet_url).then((response) => {
        this.entries = response.data.valueRanges[0].values;
      });      
    },

    refreshData() {

      this.currentDate;
      this.getData();

    },
  },

  computed:{

    currentDate: function () {

      const today = new Date();

      const date = today.getDate() + '.' + (String((today.getMonth()+1))).padStart(2, '0') + '.' + today.getFullYear();
      return date;     
    },

    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    },
  },

  mounted() {

    this.getData();

    let interval=21000;

    let timeDisplay = 1000*60;
    let minutesOrSeconds = "Minute(n)";

    let timer = () => {     
      
      if (interval < 60000) {timeDisplay = 1000; minutesOrSeconds="Sekunde(n)";}
      this.timerMS = "Seite wird in " + Math.ceil(interval/timeDisplay) +" "+minutesOrSeconds+" aktualisiert.";

      if (interval <= 0) {interval = 1800000; timeDisplay = 1000*60; minutesOrSeconds = "Minute(n)"; this.refreshData();}
      
      interval-=1000;

    }

    setInterval(timer, 1000);

}
}

</script>

<style>
#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  margin-top: '37px';  
  }

body, html {
  background: #E8EFF4;
  height:'200px';
}

ul
{
    list-style-type: none;
}
</style>
