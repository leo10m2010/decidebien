<template>
  <v-container>
    <v-flex xs12 md6 pt-4>
      <v-card height="100%">
        <v-card-text class="px-4">
          <p>
            Este app está en línea gracias al auspicio de
            <a href="https://www.transparencia.org.pe/"
              >ASOCIACIÓN CIVIL TRANSPARENCIA</a
            >
            y a la generosa donación de amig@s. Para ver la lista responsables,
            aportantes, colaboradores y más información sobre los filtros,
            revisa aquí. Esta plataforma fue iniciada por José Incio y ahora
            cuenta con much@s colaboradores Cualquier error con la data escribe
            a:
            <a href="mailto:" target="_top">therenatoem@gmail.com</a>
          </p>
          <h4>Donantes:</h4>
          <ul>
            <li>Angelina Cotler (@CotlerAngelina)</li>
            <li>Javier Tarrillo (@jtarrillov)</li>
            <li>Eliana Carlin (@ElianaCarlin)</li>
            <li>Ricardo Moran (@RicardoMoran)</li>
            <li>Michele Gabriela Fernandez (@La_micha)</li>
          </ul>
          <h4>Desarrolladores:</h4>
          <h5>Vue</h5>
          <ul>
            <li>Luis Salas (Github: zettai )</li>
            <li>Antonio Cucho (Github: antoniocuga )</li>
          </ul>
          <h5>Shiny version</h5>
          <ul>
            <li>José Incio (@jlincio)</li>
            <li>Malena Maguina (Github: malenamaguina)</li>
            <li>Samuel Calderon (Github: calderonsamuel )</li>
          </ul>
          <h5>Android</h5>
          <ul>
            <li>Renato Ez (Github:leo10m2010)</li>
          </ul>
          <h4>Web Oficial</h4>
          <ul>
           <li>decidebien.pe</li>
          </ul>
        </v-card-text>
      </v-card>
    </v-flex>
    <v-flex xs12 md6 pt-4>
      <v-card height="100%" disabled>
        <v-card-title primary-title>
          <div>
            <h1 class="headline">Escríbenos</h1>
          </div>
        </v-card-title>

        <v-card-text class="px-4">
          <form
            @submit.prevent="handleSubmit"
            name="preguntas"
            netlify-honeypot="bot-field"
            action="/success/"
            data-netlify="true"
            method="post"
            netlify
          >
            <input type="hidden" name="form-name" value="contact" />
            <p class="hidden-pot">
              <label>
                Don’t fill this out:
                <input name="bot-field" />
              </label>
            </p>
            <label class="form-label" for="name">Nombre</label>
            <input
              class="form-field"
              name="name"
              id="name"
              v-model="formData.name"
            />
            <label class="form-label" for="email">Correo Electrónico</label>
            <input
              class="form-field"
              name="email"
              id="email"
              v-model="formData.email"
            />
            <label class="form-label" for="message">Mensaje</label>
            <textarea
              class="form-field"
              name="message"
              id="message"
              v-model="formData.message"
            ></textarea>
            <div class="text-center">
              <input class="form-button primary" type="submit" value="Enviar" />
            </div>
          </form>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-container>
</template>

<style scoped>
.hidden-pot {
  display: none;
}

input.form-field,
select,
textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
}

input[type="email"],
select,
textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
}

input[type="submit"] {
  width: 40%;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>

<script>
export default {
  data() {
    return {
      formData: {}
    };
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          key => encodeURIComponent(key) + "=" + encodeURIComponent(data[key])
        )
        .join("&");
    },
    handleSubmit(e) {
      fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": e.target.getAttribute("name"),
          ...this.formData
        })
      })
        .then(() => this.$router.push("/"))
        .catch(error => alert(error));
    }
  }
};
</script>
