<template>
  <section class="page-section">
    <b-container>
      <HeaderPage title="Editar Patrocinador" />

      <!--FORM-->
      <b-row>
        <b-col cols="2"></b-col>
        <b-col cols="8">
          <form @submit.prevent="update">
            <div class="form-group">
              <input v-model="sponsor.name" type="text" class="form-control form-control-lg" id="txtName"
                placeholder="escreve o nome" required />
            </div>
            <div class="form-group">
              <select id="sltGroup" class="form-control form-control-lg" v-model="sponsor.category" required>
                <option value>-- SELECIONA CATEGORIA --</option>
                <option value="institucional">Institucional</option>
                <option value="tematico">Temático</option>
                <option value="promocional">Promocional</option>
                <option value="outros">Outros</option>
              </select>
            </div>
            <div class="form-group">
              <input v-model="prefanimal" type="text" class="form-control form-control-lg" id="txtAnimal"
                placeholder="escreve o animal favorito" required />
            </div>
            <div class="form-group">
              <textarea id="txtDescription" class="form-control form-control-lg" placeholder="escreve descrição"
                cols="30" rows="10" v-model="sponsor.description" required></textarea>
            </div>
            <button type="button" class="btn btn-outline-success btn-lg mr-2" @click="removeComments()">
              <i class="fas fa-edit"></i> REMOVER COMENTÁRIOS
            </button>
            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-edit"></i> ATUALIZAR
            </button>
            <router-link :to="{ name: 'listSponsors' }" tag="button" class="btn btn-outline-danger btn-lg">
              <i class="fas fa-window-close"></i> CANCELAR
            </router-link>
          </form>
        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { EDIT_SPONSOR } from "@/store/sponsors/sponsor.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "EditSponsor",
  components: {
    HeaderPage
  },
  data: () => {
    return {
      sponsor: {}
    };
  },
  computed: {
    ...mapGetters("sponsor", ["getSponsorsById", "getMessage"])
  },
  methods: {
    removeComments() {
      this.sponsor.comments.length = 0
      this.$alert("Comentários removidos, clique em atualizar!", "Comentários!", "success");
    },
    update() {
      this.$store.dispatch(`sponsor/${EDIT_SPONSOR}`, this.$data.sponsor).then(
        () => {
          this.$alert(this.getMessage, "Sponsor atualizado!", "success");
          router.push({ name: "listSponsors" });
        },
        err => {
          this.$alert(`${err.message}`, "Erro", "error");
        }
      );
    }
  },
  created() {
    this.sponsor = this.getSponsorsById(this.$route.params.sponsorId);
  }
};
</script>

<style scoped>
.center_div {
  margin: 0 auto;
  width: 80%;
}
</style>