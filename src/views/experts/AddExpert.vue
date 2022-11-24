<template>
  <!-- Portfolio Section -->
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar Especialista" />

      <!--FORM-->
      <b-row>
        <b-col cols="2"></b-col>
        <b-col>
          <form @submit.prevent="add">
            <div class="form-group">
              <input v-model="name" type="text" class="form-control form-control-lg" id="txtName"
                placeholder="escreve o nome" required />
            </div>
            <div class="form-group">
              <input v-model="job" type="text" class="form-control form-control-lg" id="txtJob"
                placeholder="escreve a profissão" required />
            </div>
            <div class="form-group">
              <select id="sltGroup" class="form-control form-control-lg" v-model="expertise" required>
                <option value>-- SELECIONA ESPECIALIDADE --</option>
                <option value="anfibio">ANFÍBIO</option>
                <option value="ave">AVE</option>
                <option value="mamifero">MAMÍFERO</option>
                <option value="peixe">PEIXE</option>
                <option value="reptil">RÉPTIL</option>
                <option value="geral">GERAL</option>
                <option value="extintos">ESPÉCIES VIA EXTINÇÃO</option>
              </select>
            </div>
            <div class="form-group">
              <textarea id="txtDescription" class="form-control form-control-lg" placeholder="escreve descrição"
                cols="30" rows="10" v-model="description" required></textarea>
            </div>
            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i> ADICIONAR</button>
            <router-link :to="{ name: 'listExperts' }" tag="button" class="btn btn-outline-danger btn-lg"><i
                class="fas fa-window-close"></i> CANCELAR</router-link>
          </form>
        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_EXPERT } from "@/store/experts/expert.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "AddExpert",
  components: {
    HeaderPage
  },
  data: () => {
    return {
      name: "",
      job: "",
      description: "",
      expertise: "",
      evaluation: [],
      comments: []
    };
  },
  computed: {
    ...mapGetters("expert", ["getMessage"])
  },
  methods: {
    add() {
      this.$store.dispatch(`expert/${ADD_EXPERT}`, this.$data).then(
        () => {
          this.$alert(this.getMessage, "Expert adicionado!", "success");
          router.push({ name: "listExperts" });
        },
        err => {
          this.$alert(`${err.message}`, "Erro", "error");
        }
      );
    }
  }
};
</script>
