<template>
    <div>
      <v-row>
        <v-col>
            <v-simple-table>
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">Arquivo</th>
                    <th class="text-left">Link</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="arquivo in arquivos" :key="arquivo.name">
                    <td v-if="arquivo.type == 'dir'">
                        <v-icon class="icon">mdi-folder</v-icon>
<v-chip @click="listaArquivosDento(arquivo.path)">{{ arquivo.name }}</v-chip>
                    </td>
                    <td v-else>
                    <v-icon class="icon">mdi-file-outline</v-icon>
                    {{ arquivo.name }}
                    </td>
                    <td>
                  <a :href="arquivo.html_url" target="_blank">link</a>
                    </td>
                  </tr>
                <v-icon v-if="caminhoNovo.length > 0" class="ml-4" @click="volta">mdi-arrow-left</v-icon>
                </tbody>
              </template>
          </v-simple-table>
        </v-col>
      </v-row>
    </div>
</template>

  <script>
  
    import {api} from '~api'
  
    export default {
      props: ['repo'],
      data: () => ({
        arquivos: [],
        caminhoNovo: [],
        caminhoAtual: null,
        loading: false,
      }),
      methods: {
        async listaArquivos(){
            this.loading = true
            const arquivosEntra = await api.listaArquivos(this.repo.owner.login, this.repo.name)
            this.arquivos = this.arquivos.concat(arquivosEntra)
            this.loading = false;
        },
          async listaArquivosDento(path){
            console.log(this.arquivos)
            this.loading = true
            this.arquivos = await api.listaArquivosDento(this.repo.owner.login,
                this.repo.name,
                path)
              this.caminhoNovo.push(path);
              this.currentPath = path;
              this.loading = false;
          },
        async volta(){
            this.caminhoNovo.pop()
            if (this.caminhoNovo.length == 1) {
              let caminhoVelho = this.caminhoNovo[0]
              this.arquivos = await api.listaArquivosDento(this.repo.owner.login, this.repo.name, caminhoVelho)
              this.caminhoAtual = caminhoVelho
            } else {
              let caminhoVelho = ''
              this.arquivos = await api.listaArquivosDento(this.repo.owner.login, this.repo.name, caminhoVelho)
              this.caminhoAtual = caminhoVelho
            }
        },
      },
      watch: {
        repo(){
        this.issues = []
          this.arquivos = []
          this.caminhoAtual = null
          this.caminhoNovo = []
          if (this.repo) {
            this.listaArquivos()
          } else {
            this.arquivos = []
            this.caminhoAtual = null
            this.caminhoNovo = []
          }
        }
      }
    }
  </script>
