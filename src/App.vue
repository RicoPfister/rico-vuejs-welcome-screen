<template>
  <div id="app">
    
    <h1 :style=heading>Welcome to Opportunity</h1>
    <h1 :style=date>08.08.2021</h1>

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

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      heading: {
      'font-weight': '900',
      color: '#323D4A',
      'font-size': '25px',
      padding: 0,
      margin: 0,      
      },
      date: {
      'font-weight': '500',
      color: '#9AA7B1',
      'font-size': '25px',
      padding: '10px 0',
      margin: 0,
      },
      entryContainer: {
      background: '#0F05A0',
      'padding-top': '11px',
      'padding-left': '14px',
      width: '380px',
      height: '50px',
      },
      entrySeparator: {
        'margin-bottom': '10px',
      },
      entryTime: {
      'font-weight': '900',
      color: '#EB5E00',
      'font-size': '10px',
      padding: 0,
      margin: 0,
      },
      entryTitle: {
      'font-weight': '900',
      color: '#FFBFAB',
      'font-size': '10px',
      padding: 0,
      margin: 0,
      },
      entryContent: {
      'font-weight': '500',
      color: '#FFBFAB',
      'font-size': '10px',
      padding: 0,
      margin: 0,
      },           
    }
  }
}
</script>

<style>
#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  margin-top: 20px;
  margin-left: 10px;    
  }

body {
  background: #E8EFF4;
}
</style>
