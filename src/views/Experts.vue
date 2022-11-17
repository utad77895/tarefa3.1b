<template>
  <b-container fluid>
    <!-- Header -->
        <header class="masthead bg-secondary text-white text-center">
    <b-row>
      <b-col>
    
          <img class="masthead-avatar mb-2" src="@/assets/animalec.png" />
          <p class="masthead-subheading font-weight-light">
            Aprender tudo sobre animais de uma forma divertida!
          </p>
      </b-col>
    </b-row>      
          <b-row>
            <b-col>
              <b-button
                variant="light"
                href="#rules"
                class="p-2 mr-2"
              >
                <i class="fas fa-info-circle mr-2"></i>COMO JOGAR?
              </b-button>
               <b-button
                variant="danger"                
                
                class="p-2 mr-2"
                @click="showRanking()"
              >
               <i class="fas fa-chart-line mr-2"></i>VER RANKING
              </b-button>
            </b-col>
          </b-row>
        </header>
      
    <!-- Experts section -->
    <section class="page-section bg-danger" id="rules">
      <b-container fluid>
        <h4
          class="page-section-heading text-center text-uppercase text-white mb-5"
        >
          EXPERTS PAGE
        </h4>
        <b-row class="mt-5 mb-5">
          <b-col cols="2"></b-col>
          <b-col class="text-center">
            <i class="fas fa-star fa-3x" style="color:white"></i>
            <p>
               <strong>Júlia Almeida</strong> Especialista em Macacos!
            </p>
          </b-col>
          <b-col cols="2"></b-col>
          <b-col class="text-center">
            <i class="fas fa-star fa-3x" style="color:white"></i>
            <p><strong>António Silva</strong> Especialista em Leões!
            </p>
          </b-col>
          <b-col cols="2"></b-col>
        </b-row>
        <b-row class="mb-5">
          <b-col cols="2"></b-col>
          <b-col class="text-center">
            <i class="fas fa-star fa-3x" style="color:white"></i>
            <p><strong>Joana Silva </strong>Especialista em Crocodilos!
            </p>
          </b-col>
          <b-col cols="2"></b-col>
          <b-col class="text-center">
            <i class="fas fa-star fa-3x" style="color:white"></i>
            <p><strong>João Cordeiro </strong>Especialista em Girafas!</p>
          </b-col>
          <b-col cols="2"></b-col>
        </b-row>

      </b-container>
    </section>
    

    <!-- Footer -->
    <footer class="footer text-center">
      <div class="container">
        <div class="row">
          <!-- Footer Location -->
          <div class="col-lg-4 mb-5 mb-lg-0">
            <h4 class="text-uppercase mb-4">Criadores</h4>
            <p class="lead mb-0">
              <a href="mailto:ricardo.queiros@gmail.com" target="_blank"
                >Ricardo Queirós</a
              >
              <br /><a href="mailto:filipeportela@iotech.pt" target="_blank"
                >Filipe Portela</a
              >
            </p>
          </div>

          <!-- Footer Social Icons -->
          <div class="col-lg-4 mb-5 mb-lg-0">
            <h4 class="text-uppercase mb-4">PRESENÇA DIGITAL</h4>
            <a class="btn btn-outline-light btn-social mx-1" href="#">
              <i class="fab fa-fw fa-facebook-f"></i>
            </a>
            <a class="btn btn-outline-light btn-social mx-1" href="#">
              <i class="fab fa-fw fa-twitter"></i>
            </a>
            <a class="btn btn-outline-light btn-social mx-1" href="#">
              <i class="fab fa-fw fa-linkedin-in"></i>
            </a>
            <a class="btn btn-outline-light btn-social mx-1" href="#">
              <i class="fab fa-fw fa-dribbble"></i>
            </a>
          </div>

          <!-- Footer About Text -->
          <div class="col-lg-4">
            <h4 class="text-uppercase mb-4">Sobre o Animalec</h4>
            <p class="lead mb-0">
              Animalec usa tema de Bootstrap com licença MIT, gratuito e criado
              por
              <a href="http://startbootstrap.com" target="_blank"
                >StartBootstrap</a
              >.
            </p>
          </div>
        </div>
      </div>
    </footer>

    <!-- Copyright Section -->
    <section class="copyright py-4 text-center text-white">
      <div class="container">
        <small>Copyright &copy; ANIMALEC 2020</small>
      </div>
    </section>

    <!-- Scroll to Top Button (Only visible on small and extra-small screen sizes) -->
    <div class="scroll-to-top d-lg-none position-fixed">
      <a
        class="js-scroll-trigger d-block text-center text-white rounded"
        href="#page-top"
      >
        <i class="fa fa-chevron-up"></i>
      </a>
    </div>
  </b-container>
</template>

<script>
import { FETCH_ANIMALS } from "@/store/animals/animal.constants";
import { FETCH_USERS } from "@/store/users/user.constants";
import { SEND_EMAIL } from "@/store/constants";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "Home",
  data: function() {
    return {
      name: "ricardo",
      email: "ricardo.queiros@gmail.com",
      subject: "teste",
      message: "isto é um teste!"
    };
  },
  computed: {
    ...mapGetters(["getMessage", "auth/isUserLoggedIn"])
  },
  methods: {
    showRanking() {
      router.push({ name: "ranking" });
    },
    send() {
      this.$store
        .dispatch(`${SEND_EMAIL}`, this.$data)
        .then(
          () => this.$alert(this.getMessage, "E-mail enviado!", "success"),
          err => this.$alert(`${err.message}`, "Erro", "error")
        );
    }
  },
  created() {
    if (this.isUserLoggedIn) {
      this.$store.dispatch(`animal/${FETCH_ANIMALS}`);
      this.$store.dispatch(`user/${FETCH_USERS}`);
    }
  }
};
</script>
