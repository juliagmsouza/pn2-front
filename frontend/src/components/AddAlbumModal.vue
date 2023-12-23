<template>
    <div>
        <b-row class="pt-1 px-2">
            <label for="title-input" style="margin-left: -6px">Título do álbum:</label>
            <b-form-input id="title-input" v-model="albumName">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="release-date-input" style="margin-left: -6px">Ano de lançamento do álbum:</label>
            <b-form-input id="release-date-input" v-model="releaseYear">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="recorder-input" style="margin-left: -6px">Gravadora:</label>
            <b-form-input id="recorder-input" v-model="recorder">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="description-input" style="margin-left: -6px">Descrição:</label>
            <b-form-textarea id="description-input" v-model="description" rows="5" no-resize>
            </b-form-textarea>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="value-input" style="margin-left: -6px">Valor do álbum:</label>
            <b-form-input id="value-input" v-model="value">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="image-url-input" style="margin-left: -6px">URL da imagem da capa do álbum:</label>
            <b-form-input id="image-url-input" v-model="imageUrl">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <b-col cols="11">
                <label for="tracks-input" style="margin-left: -6px">Adicionar faixa:</label>
                <b-form-input id="tracks-input" v-model="track" style="margin-left: -12px">
                </b-form-input>
            </b-col>
            <b-col cols="1">
                <b-button @click="addTrack(track)" style="margin-top: 24px; margin-left: -14px"
                    :disabled="track.length === 0">
                    <plus-icon size="1x">
                    </plus-icon>
                </b-button>
            </b-col>
        </b-row>
        <b-row v-if="tracks.length > 0" class="pt-1" style="margin-left: 1px">
            Faixas:
            <ul>
                <li v-for="i, index in tracks" :key="index" style="margin-left: 12px">{{ i }}</li>
            </ul>
        </b-row>
        <hr style="width: 107%; margin-left: -16px">
        <b-row align-h="end">
            <b-col class="justify-content-end d-flex" cols="7" style="padding-right: 0">
                <b-button @click="closeModal" variant="secondary">
                    Cancelar
                </b-button>
                <b-button style="margin-left: 4%; margin-right: 3%" variant="primary" :disabled="albumName.length === 0 || releaseYear.length === 0 || recorder.length === 0 || description.length === 0 || value.length === 0 || imageUrl.length === 0 || tracks.length === 0">
                    {{ currentAlbumName ? 'Editar Álbum' : 'Adicionar Álbum' }}
                </b-button>
            </b-col>
        </b-row>
    </div>
</template>

<script>
import { PlusIcon } from 'vue-feather-icons'
export default {
    components: {
        PlusIcon
    },
    props: {
        currentAlbumName: { type: String, required: false, default: '' },
        currentReleaseYear: { type: String, required: false, default: '' },
        currentRecorder: { type: String, required: false, default: '' },
        currentDescription: { type: String, required: false, default: '' },
        currentValue: { type: String, required: false, default: '' },
        currentImageUrl: { type: String, required: false, default: '' },
        currentTracks: { type: Array, required: false, default: () => {return []} }
    },
    data() {
        return {
            albumName: '',
            releaseYear: '',
            recorder: '',
            description: '',
            value: '',
            imageUrl: '',
            track: '',
            tracks: [],
        }
    },
    mounted(){
        this.albumName = this.currentAlbumName
        this.releaseYear = this.currentReleaseYear
        this.recorder = this.currentRecorder
        this.description = this.currentDescription
        this.value = this.currentValue
        this.imageUrl = this.currentImageUrl
        this.tracks = this.currentTracks
    },
    methods: {
        addTrack(val) {
            this.tracks.push(val)
            this.track = ''
        },
        closeModal() {
            this.$bvModal.hide('add-album-modal')
        }
    }
}
</script>