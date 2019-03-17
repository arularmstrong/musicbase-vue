<template>  
    <div>    
        <h2>Dashboard</h2>

<select v-model="record">
  <option v-for="record in records" :key="record" v-bind:value="record" >{{record.name}}</option>
</select>
 <button v-on:click="listAlbumsUnderRecord">List albums under record</button>
        <button v-on:click="listArtistsUnderRecord">List artists under record</button>
<div class="list">
<ol v-if="recordData.length">
  <li v-for="item in recordData" :key="item">
    {{item.name}}
  </li>
</ol></div>

<select v-model="album">
  <option v-for="album in albums" :key="album" v-bind:value="album">{{album.name}}</option>
</select>
 <button v-on:click="listArtistsUnderAlbum">List artists under album</button>
<div class="list">
<ol v-if="albumData.length">
  <li v-for="item in albumData" :key="item">
    {{item.name}}
  </li>
</ol></div>

<select v-model="artist">
  <option v-for="artist in artists" :key="artist" v-bind:value="artist">{{artist.name}}</option>
</select>
    <button v-on:click="listAlbumsUnderArtist">List albums under Artist</button>
<div class="list">
<ol v-if="artistData.length">
  <li v-for="item in artistData" :key="item">
    {{item.name}}
  </li>
</ol></div>

       
    </div>
</template>  
<script>  
    import axios from "axios"    
    import router from "../router"    
    export default {    
        name: "Dashboard",    
        data: function(){
               return{ records: [],
                        albums: [],
                        artists:[],
                        recordData: [],
                        albumData: [],
                        artistData: []}
  },    
        methods: {    
            
            
        fetchRecordLabels: function(){
                let self = this
                axios.post("/api/list_records")
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "records", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })    
        },
         fetchAlbums: function(){
                let self = this
                axios.post("/api/list_albums")
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "albums", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })    
        },
         fetchArtists: function(){
                let self = this
                axios.post("/api/list_artists")
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "artists", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })    
        },
        listAlbumsUnderRecord: function(){
                let self = this
                let data = {    
                        recordId: this.record.id
                    }  
                axios.post("/api/list_albums_under_record", data)
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "recordData", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })   
                
        },
         listArtistsUnderRecord: function(){
                let self = this
                let data = {    
                        recordId: this.record.id
                    }  
                axios.post("/api/list_artists_under_record", data)
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "recordData", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })   
                
        },
        listArtistsUnderAlbum: function(){
                let self = this
                let data = {    
                        albumId: this.album.id
                    }  
                axios.post("/api/list_artists_under_album", data)
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "albumData", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })   
                
        },
        listAlbumsUnderArtist: function(){
                let self = this
                let data = {    
                        artistId: this.artist.id
                    }  
                axios.post("/api/list_albums_under_artist", data)
                    .then((response) => {    
                        console.log(response.data.data)    
                      self.$set(this, "artistData", response.data.data)    
                    })    
                    .catch((errors) => {    
                        console.log(errors)  
                    })   
                
        }
        },    
        mounted() {     
          
          axios.defaults.headers.post['Authorization'] = 'Bearer '+ localStorage.getItem('token')
          this.fetchRecordLabels()
          this.fetchAlbums()
          this.fetchArtists()
        }    
    }
</script>