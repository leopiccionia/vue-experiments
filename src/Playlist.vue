<template>
  <div id="the-player">
    <div class="header" :style="{ backgroundImage: `url(${coverArt})` }">
      <div class="header-mask">
        <div class="grid">
          <img class="cover-art" :src="coverArt" alt="">
          <div class="details">
            <div class="album">Abbey Road</div>
            <div class="artist" aria-label="By:">The Beatles</div>
            <div class="year">1969</div>
          </div>
        </div>
      </div>
    </div>
    <div class="playlist">
      <div class="grid">
        <div class="row title">
          <div class="song">
            <div class="number">№</div>
            Song
          </div>
          <div class="length">Length</div>
        </div>
        <div class="row" v-for="(song, index) in songs" :key="song.name">
          <div class="song">
            <div class="number">{{ index + 1 }}</div>
            {{ song.name }}
          </div>
          <div class="length">{{ song.length }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Playlist',
    computed: {
      coverArt () {
        return 'https://upload.wikimedia.org/wikipedia/en/4/42/Beatles_-_Abbey_Road.jpg';
      },
      songs () {
        return [
          { name: `Come Together`, length: '4:19' },
          { name: `Something`, length: '3:02' },
          { name: `Maxwell's Silver Hammer`, length: '3:27' },
          { name: `Oh! Darling`, length: '3:27' },
          { name: `Octopus's Garden`, length: '2:51' },
          { name: `I Want You (She's So Heavy`, length: '7:47' },
          { name: `Here Comes the Sun`, length: '3:05' },
          { name: `Because`, length: '2:45' },
          { name: `You Never Give Me Your Money`, length: '4:03' },
          { name: `Sun King`, length: '2:26' },
          { name: `Mean Mr. Mustard`, length: '1:06' },
          { name: `Polythene Pam`, length: '1:13' },
          { name: `She Came In Through the Bathroom Window`, length: '1:58' },
          { name: `Golden Slumbers`, length: '1:31' },
          { name: `Carry That Weight`, length: '1:36' },
          { name: `The End`, length: '2:05' },
          { name: `Her Majesty`, length: '0:23'}
        ]
      }
    }
  }
</script>

<style lang="scss">
  :root {
    font-family: sans-serif;
    font-size: 16px;
  }

  body {
    background-color: #222;
    color: #DDD;
    min-height: 100vh;
    margin: 0;
    padding: 0;
    overflow-x: hidden;
    width: 100vw;
  }

  .grid {
    margin: auto;
    max-width: 1000px;
    width: 100%;
  }

  .header {
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
  }

  .header-mask {
    background-color: rgba(34, 34, 34, 0.9);
    backdrop-filter: blur(5px);
    height: 100%;
    line-height: 1.5;
    padding: 20px;

    .grid {
      display: flex;
    }
  }

  .cover-art {
    box-shadow: 0 0 10px #222;
    height: 180px;
    max-height: 40vw;
    max-width: 40vw;
    width: 180px;
  }

  .details {
    display: flex;
    flex-direction: column;
    margin-left: 1em;
    justify-content: flex-end;
  }

  .album {
    font-size: 1.5rem;
    font-weight: bold;
  }

  .artist {
    font-size: 1.2rem;
  }

  .year {
    color: #AAA;
  }

  .playlist {
    padding: 20px;
  }

  .playlist .row {
    display: flex;
    border-bottom: 1px solid #2D2D2D;
    justify-content: space-between;
    padding: 0.5em;

    &.title {
      font-weight: bold;
      border-bottom-color: #555;
    }

    &:last-child {
      border-bottom: none;
    }
  }

  .song {
    display: flex;
  }

  .song .number, .length {
    color: #999;
  }

  .song .number {
    display: inline-block;
    min-width: 2rem;
  }

  .length {
    margin-left: 1em;
  }

  .row.title * {
    color: white;
  }
</style>
