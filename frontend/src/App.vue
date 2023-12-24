<template>
  <div :class="isAuthenticated && !loading ? backgroundMapper[albums[index].name.toLowerCase()] || backgroundMapper.default : 'default-background'"
    id="app">
    <b-spinner v-if="isAuthenticated && loading"
      style="width: 250px; height: 250px; position: absolute; top: 33%; left: 42%">
    </b-spinner>
    <div v-if="isAuthenticated && !loading" class="d-flex h-80 align-items-center" style="position: absolute; top: 17%;">
      <b-col>
        <b-row>
          <b-button @click="openModal('add-album-modal')" style="width: 10%; margin-left: 75.75%; margin-bottom: 1%"
            variant="dark">
            Adicionar álbum
          </b-button>
        </b-row>
        <b-row class="w-100" align-h="center">
          <b-col class="align-self-center d-flex justify-content-end">
            <chevron-left-icon style="cursor: pointer" size="6x" @click="previousAlbum">
            </chevron-left-icon>
          </b-col>
          <b-col class="d-flex justify-content-center" cols="3">
            <b-img v-if="albums[index - 1]" :src="albums[index - 1].image_url" class="rounded image-size">
            </b-img>
            <b-img v-else-if="albums.length > 2" :src="albums[albums.length - 1].image_url" class="rounded image-size">
            </b-img>
          </b-col>
          <b-col @mouseleave="hover = false" class="d-flex justify-content-center position-relative" cols="3">
            <b-img style="z-index: 1" :src="albums[index].image_url" class="rounded image-size detail-album-image"
            :class="hover ? 'detail-album-image-hover' : ''">
          </b-img>
            <div v-if="!hover" class="w-100 h-100 position-relative">
              <b-button style="z-index: 10" variant="dark" class="align-details-icon"
                @click="hover = true; detailAlbum(albums[index].id)">
                <info-icon size="1x" style="cursor: pointer">
                </info-icon>
                Ver detalhes
              </b-button>
              <b-button style="z-index: 10" variant="dark" class="align-delete-icon"
              @click="setSelectedAlbum(albums[index])">
              <trash-icon size="1x" style="cursor: pointer">
              </trash-icon>
            </b-button>
            <b-button @click="setSelectedAlbumInfo(albums[index])" style="z-index: 10" variant="dark"
                class="align-edit-icon">
                <edit-icon size="1x" style="cursor: pointer">
                </edit-icon>
              </b-button>
            </div>
            <b-spinner v-if="loadingDetails" variant="white" style="z-index: 10; position: absolute; width: 100px; height: 100px; top: 45%; left: 38%">
            </b-spinner>
            <div style="z-index: 2" v-if="hover && !loadingDetails" class="detail-album-content rounded">
              <b-row class="pt-2">
                Álbum: {{ albumDetails.name }}, {{ albumDetails.year }} - {{ albumDetails.recorder }}
              </b-row>
              <b-row class="pt-1 align-text">
                Descrição: {{ albumDetails.description }}
              </b-row>
              <b-row class="pt-1">
                Faixas:
                <ul>
                  <li v-for="i, index in albumDetails.tracks" :key="index">{{ i }}</li>
                </ul>
              </b-row>
              <b-row style="margin-top: -10px">
                Valor: R$ {{ albumDetails.valor }}
              </b-row>
            </div>
          </b-col>
          <b-col class="d-flex justify-content-center" cols="3">
            <b-img v-if="albums[index + 1]" :src="albums[index + 1].image_url" class="rounded image-size">
            </b-img>
            <b-img v-else :src="albums[0].image_url" class="rounded image-size"></b-img>
          </b-col>
          <b-col class="align-self-center">
            <chevron-right-icon size="6x" style="cursor: pointer" @click="nextAlbum">
            </chevron-right-icon>
          </b-col>
        </b-row>
      </b-col>
    </div>
    <div v-else-if="!isAuthenticated && loading" class="container-login">
      <div class="text">
        <b-row>
          <strong class="align-login-text">Login</strong>
        </b-row>
        <b-row>
          <label for="email-credential" style="margin-left: -6px">Email:</label>
          <b-form-input id="email-credential" v-model="emailCredential" placeholder="julia.souza@pucminas.com.br">
          </b-form-input>
        </b-row>
        <b-row class="mt-2">
          <label for="password-credential" style="margin-left: -6px">Senha:</label>
          <b-form-input type="password" id="password-credential" v-model="passwordCredential" placeholder="********">
          </b-form-input>
        </b-row>
        <b-row align-h="center" class="mt-3" style="margin-bottom: -1%">
          <b-button @click="login" size="sm" style="width: 30%">
            Entrar
          </b-button>
        </b-row>
        <hr style="border: 1px solid rgba(255, 255, 255, 1)">
        <b-row class="text-center mt-3" style="margin-bottom: -1%">
          <b-col>
            <u @click="openModal('create-account-modal')" style="cursor: pointer">Criar conta</u>
          </b-col>
        </b-row>
      </div>
    </div>
    <!--MODALS-->
    <b-modal id="confirm-delete-album-modal" cancel-title="Cancelar" ok-title="Excluir" @ok="deleteAlbum(selectedAlbum.id)" hide-header>
      <ConfirmDeleteAlbumModal />
    </b-modal>
    <b-modal id="add-album-modal" cancel-title="Cancelar" ok-title="Adicionar" hide-header hide-footer
      @hide="selectedAlbum = {}">
      <AddAlbumModal :currentAlbumName="selectedAlbum.name" :currentReleaseYear="selectedAlbum.year"
        :currentRecorder="selectedAlbum.recorder" :currentDescription="selectedAlbum.description"
        :currentValue="selectedAlbum.valor" :currentImageUrl="selectedAlbum.image_url" :albumId="selectedAlbum.id"
        :currentTracks="selectedAlbum.tracks" :token="token" />
    </b-modal>
    <b-modal id="create-account-modal" cancel-title="Cancelar" ok-title="Criar" hide-header hide-footer>
      <CreateAccountModal />
    </b-modal>
  </div>
</template>

<script>
import { ChevronLeftIcon, ChevronRightIcon, TrashIcon, EditIcon, InfoIcon } from 'vue-feather-icons'
import AddAlbumModal from './components/AddAlbumModal.vue'
import ConfirmDeleteAlbumModal from './components/ConfirmDeleteAlbumModal.vue'
import CreateAccountModal from './components/CreateAccountModal.vue'
import axios from 'axios'

export default {
  components: {
    InfoIcon,
    EditIcon,
    TrashIcon,
    AddAlbumModal,
    ChevronLeftIcon,
    ChevronRightIcon,
    CreateAccountModal,
    ConfirmDeleteAlbumModal,
  },
  name: 'App',
  data() {
    return {
      albumDetails: {},
      loadingDetails: false,
      loading: true,
      token: '',
      baseUrl: 'https://taylorswiftalbums.onrender.com',
      passwordCredential: '',
      emailCredential: '',
      isAuthenticated: false,
      hover: false,
      index: 1,
      selectedAlbum: {
        name: ''
      },
      albums: [],
      backgroundMapper: {
        'taylor swift': 'taylor-swift-background-color',
        'fearless': 'fearless-background-color',
        'speak now': 'speak-now-background-color',
        'red': 'red-background-color',
        '1989': 'nineteen-eighty-nine-background-color',
        'reputation': 'reputation-background-color',
        'lover': 'lover-background-color',
        'folklore': 'folklore-background-color',
        'evermore': 'evermore-background-color',
        'midnights': 'midnights-background-color',
        'default': 'midnights-background-color'
      }
    }
  },
  mounted() {
    this.$root.$on('reloadList', async () => {
      await this.listAlbums()
    })
  },
  methods: {
    nextAlbum() {
      if (this.index === this.albums.length - 1) {
        this.index = 0;
      } else this.index++;
    },
    previousAlbum() {
      if (this.index === 0) {
        this.index = this.albums.length - 1;
      } else this.index--;
    },
    openModal(val) {
      this.$bvModal.show(val)
    },
    async setSelectedAlbumInfo(val) {
      await this.detailAlbum(val.id, true)
      this.selectedAlbum = this.albumDetails
      console.log('selected', this.selectedAlbum)
      this.openModal('add-album-modal')
    },
    async login() {
      try {
        const data = {
          login: this.emailCredential,
          password: this.passwordCredential
        }
        const response = await axios.post(`${this.baseUrl}/security/login`, data)
        console.log('responseeee', response)
        if (response.status === 200) {
          this.token = `Bearer ${response.data.token}`
          this.listAlbums()
          this.isAuthenticated = true
        }
      } catch (err) {
        alert('Erro inesperado ao fazer login. Por favor tente novamente!')
      }
    },
    async listAlbums() {
      console.log('ta aqui', this.token)
      try {
        this.loading = true
        const response = await axios.get(`${this.baseUrl}/albums`, { headers: { authorization: this.token } })
        if (response.status === 200) {
          this.albums = response.data
          if (this.albums.length === 1) {
            this.index = 0;
          }
          this.loading = false
        }
      } catch (err) {
        alert('Erro inesperado ao listar álbums. Por favor tente novamente!')
      }
    },
    async detailAlbum(id, isEdit = false) {
      try {
        if (!isEdit) {
          this.loadingDetails = true
        }  
        const response = await axios.get(`${this.baseUrl}/album/${id}`, { headers: { authorization: this.token } })
        if (response.status === 200) {
          this.albumDetails = response.data[0]
          this.loadingDetails = false
        }
      } catch (err) {
        alert('Erro inesperado ao detalhar álbum. Por favor tente novamente!')
      }
    },
    async deleteAlbum(id) {
      try {
        const response = await axios.delete(`${this.baseUrl}/album/${id}`, { headers: { authorization: this.token } })
        if (response.status === 200) {
          await this.listAlbums()
          alert('Álbum deletado com sucesso!')
        }
      } catch (err) {
        alert('Erro inesperado ao deletar álbum. Por favor tente novamente!')
      }
    },
    async setSelectedAlbum(val) {
      this.selectedAlbum = val
      this.openModal('confirm-delete-album-modal')
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Rubik");

html,
body {
  height: 100vh;
  width: 100vw;
  margin: 0;
}

#app {
  height: inherit;
  font-family: "Rubik";
  width: inherit;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.taylor-swift-background-color {
  background: rgb(13, 180, 222);
  background: radial-gradient(circle, rgba(13, 180, 222, 1) 0%, rgba(45, 198, 83, 1) 100%);
}

.fearless-background-color {
  background: rgb(236, 206, 117);
  background: radial-gradient(circle, rgba(236, 206, 117, 1) 0%, rgba(145, 108, 57, 1) 100%);
}

.speak-now-background-color {
  background: rgb(178, 152, 220);
  background: radial-gradient(circle, rgba(178, 152, 220, 1) 0%, rgba(151, 58, 168, 1) 100%);
}

.red-background-color {
  background: rgb(237, 72, 57);
  background: radial-gradient(circle, rgba(237, 72, 57, 1) 0%, rgba(202, 15, 46, 1) 100%);
}

.nineteen-eighty-nine-background-color {
  background: rgb(237, 224, 212);
  background: radial-gradient(circle, rgba(237, 224, 212, 1) 0%, rgba(144, 224, 239, 1) 85%);
}

.reputation-background-color {
  background: rgb(108, 117, 125);
  background: radial-gradient(circle, rgba(0, 0, 0, 1) 0%, rgba(108, 117, 125, 1) 100%);
}

.lover-background-color {
  background: rgb(238, 174, 202);
  background: radial-gradient(circle, rgba(238, 174, 202, 1) 0%, rgba(148, 187, 233, 1) 100%);
}

.folklore-background-color {
  background: rgb(167, 147, 130);
  background: radial-gradient(circle, rgba(167, 147, 130, 1) 0%, rgba(173, 181, 189, 1) 100%);
}

.evermore-background-color {
  background: rgb(229, 147, 95);
  background: radial-gradient(circle, rgba(229, 147, 95, 1) 0%, rgba(106, 69, 46, 1) 100%);
}

.midnights-background-color {
  background: rgb(118, 146, 167);
  background: radial-gradient(circle, rgba(118, 146, 167, 1) 0%, rgba(2, 9, 35, 1) 100%);
}

.image-size {
  max-width: 100%;
  height: 100%;
}

.main-row-position {
  padding-top: 50px
}

.detail-album-image {
  position: absolute;
  top: 0;
  left: 50;
}

.detail-album-image-hover {
  transform: scale(1.2);
  filter: grayscale(20%) brightness(0.3)
}

.detail-album-content {
  position: absolute;
  top: 0;
  left: 40;
  width: 85%;
  max-height: 100%;
  transform: scale(1.2);
  color: white;
  font-size: 11px;
}

.align-text {
  text-align: justify;
  text-justify: inter-character
}

.align-delete-icon {
  position: absolute;
  top: 88%;
  left: 87%;
}

.align-edit-icon {
  position: absolute;
  top: 88%;
  left: 74%;
}

.align-details-icon {
  position: absolute;
  top: 88%;
  left: 2.5%;
}

.default-background {
  background: url("./assets/AA.png");
}

.container-login {
  width: 27%;
  background-color: transparent;
  padding: 25px;
  border: 2px solid #FFFFFF;
  backdrop-filter: blur(10px);
  border-radius: 8px;
  position: absolute;
  top: 35%;
  left: 40%
}

.align-login-text {
  margin-left: -2%;
  margin-bottom: 2%
}

.text {
  color: #FFFFFF
}
</style>
