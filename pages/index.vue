<template>
  <section class="section">
    <div class="container content">
      <div class="columns is-centered">
        <div class="column is-half">
          <br>
          <br>
          <h1 class="title has-text-warning has-text-centered">
            Random Quotes 🍪
          </h1>
          <p class="has-text-success has-text-weight-bold has-text-centered">
            Click Random Button to Get Random Quotes from Different Quote Categories.
          </p>
          <div class="buttons is-centered">
            <button id="installPWA" class="button is-info read-random" @click.prevent="showInstallPrompt()">
              ⚛ Install App
            </button>
          </div>
          <div class="notification has-text-weight-bold read-more">
            <p>{{ results.quotes }}</p>
            <br>
          </div>
          <p class="has-text-white">
            💌 {{ loading ? "Loading Data" : results.author }}
          </p>
          <br>
          <div class="buttons is-centered">
            <button class="button is-success read-random" @click.prevent="getResult">
              {{ loading ? "🔄 New Quotes" : "🔄 Random" }}
            </button>
            <button
              v-clipboard:copy="results.quotes +'\n\n💌 ' + results.author"
              v-clipboard:success="onCopy"
              v-clipboard:error="onError"
              class="btn button is-link read-random"
              type="button"
            >
              📝 Copy Word
            </button>
          </div>
          <br>
          <br>
          <div class="notification is-warning">
            <br>
            <p class="has-text-weight-bold has-text-centered">
              Our Free Telegram Bot Just start and Get random Quotes.
              <br>
              <br>
              <span class="buttons is-centered">
                <a href="https://t.me/quoteswritten_bot" class="button is-danger read-random" target="_blank" rel="nofollow noopener">🤖 Start Bot</a>
              </span>
              <br>
              This Web App was Dedicated to Quotes Lover ❤💚<br>
              Quotes are Collected from Different Sources.
            </p>
            <br>
            <div class="buttons is-centered">
              <a href="https://github.com/mskian/vue-random-quotes" class="button is-success read-random" target="_blank" rel="nofollow noopener">📦 Souce Code</a>
              <a href="https://github.com/mskian/quotes-data" class="btn button is-link read-random" target="_blank" rel="nofollow noopener">🗃 API Data</a>
            </div>
            <br>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import { debounce } from 'lodash'
import intializePwa from '~/helpers/pwa'
import 'bulma/css/bulma.min.css'
export default {
  data () {
    return {
      showInstallPrompt: null,
      results: {}
    }
  },
  head () {
    return {
      meta: [
        {
          hid: 'og:url',
          property: 'og:url',
          content: 'https://quotes.santhoshveer.com' + this.$route.path
        }
      ]
    }
  },
  async mounted () {
    this.showInstallPrompt = await intializePwa()
  },
  beforeMount () {
    this.getResult()
  },
  created () {
    this.debounceName = debounce(this.getResult)
  },
  methods: {
    getResult () {
      this.loading = true
      axios.get('https://api.sanweb.info/quotes/').then((response) => { this.results = response.data[0]; this.loading = false })
      this.$toast.success('New Quote Updated', {
        duration: 500
      }
      )
    },
    onCopy (e) {
      this.$toast.info('Quote Copied', {
        duration: 500
      }
      )
    },
    onError (e) {
      alert('Failed to copy Quote')
    }
  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Baloo+Thambi+2:wght@400;500;600;700;800&display=swap');
body {
  font-size: 16px;
  background-color: #1d3557;
  height: 100vh;
  color: rgba(0, 0, 0, 0.6);
  font-family: 'Baloo Thambi 2', cursive;
  font-weight: 600;
  line-height: 1.618;
	-webkit-font-smoothing: antialiased;
	-moz-font-smoothing: grayscale;
	overflow-x: hidden;
}
::-webkit-scrollbar {
    width: 8px;
    height: 8px;
  }
  ::-webkit-scrollbar-thumb {
    background-color: rgba(175, 180, 247, 0.302);
    border-radius: 8px;
  }
  ::-webkit-scrollbar-thumb:hover {
    background-color: rgba(97, 245, 78, 0.5);
}
h1{font-weight:700;font-size:23px;}
h2{font-weight:700;font-size:21px;}
h3{font-weight:700;font-size:20px;}
h4{font-weight:700;font-size:18px;}
h5{font-weight:700;font-size:18px;}
h1, h2, h3, h4, h5, h6 {
    color: #050505;
    word-wrap: break-word;
    -webkit-hyphens: auto;
    -moz-hyphens: auto;
    -ms-hyphens: auto;
    -o-hyphens: auto;
    hyphens: auto;
}
p,
button,
input,
textarea,
.control,
.label,
.notice {
	text-align: center;
	margin: 0 auto;
}
.title {
  color:#d9ee1c;
  font-weight: 800;
}
a:hover, a:focus, a:active {
    color: #010508;
}
.content a {
    color: #ffffff;
}
.notification {
  background-color: #e4f89b;
  color: rgb(29, 7, 7);
}
.read-more {
	display: flex;
	flex-grow: 0.3;
	font-weight: 600;
	font-size: 20px;
	box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
	border-radius: 30px;
	padding: 35px;
  padding-bottom: 18px;
	-moz-osx-font-smoothing: grayscale;
	-webkit-font-smoothing: antialiased !important;
	-moz-font-smoothing: antialiased !important;
	text-rendering: optimizelegibility !important;
}
.read-random {
	display: flex;
	flex-grow: 0.3;
  font-family: 'Baloo Thambi 2', cursive;
	font-weight: 800;
	font-size: 13px;
	box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
	border-radius: 32px;
	padding: 10px;
	-moz-osx-font-smoothing: grayscale;
	-webkit-font-smoothing: antialiased !important;
	-moz-font-smoothing: antialiased !important;
	text-rendering: optimizelegibility !important;
}
.input-box,
textarea,
.sign-button {
	width: 45rem !important;
	min-height: 3rem;
}
button {
    max-width: 100%;
}
table {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
    padding: 12px;
    -moz-osx-font-smoothing: grayscale;
   -webkit-font-smoothing: antialiased !important;
   -moz-font-smoothing: antialiased !important;
   text-rendering: optimizelegibility !important;
   border-bottom:2px solid #bbb !important;background-color:#d3d3d3
}
th {
   white-space: nowrap;
}
.cooked table thead,.d-editor-preview table thead{border-bottom:2px solid #bbb !important;background-color:#d3d3d3}.cooked table tr,.d-editor-preview table tr{border-bottom:1px solid #bbb}
.is-horizontal-center {
    justify-content: center;
}
code {
    word-break: break-all;
}
pre code {
    padding: 0;
    font-size: inherit;
    line-height: inherit;
    color: inherit;
}
.content h1 {
    font-size:28px;
    font-weight: 800;
}
.content h2 {
    font-size:21px;
    font-weight: 700;
}
.content h3 {
    font-size:20px;
    font-weight: 700;
}
.content h4 {
    font-size:18px;
    font-weight: 700;
}
footer p {
    font-size: 15px;
    font-weight: 700;
}
</style>
