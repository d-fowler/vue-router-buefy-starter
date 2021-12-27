<template>
  <section>
    <div>
      <b-button
        type="is-primary"
        @click="qRModal();startCounter()"
        icon-left="qrcode"
        outlined
      >Scanner</b-button>
    </div>
    <!--Display parking Info  -->
    <div v-show="scan">
      <p>
        <b-button
          type="is-text"
          icon-left="map-marked"
          style="margin-top: 5px;
    margin-bottom: 5px;"
          @click="linkToGoogleMap()"
        >Nice Etoile</b-button>
      </p>
      <p>
        14h30 -
        <b>({{counter}})</b>
      </p>
      <b-button
        type="is-text"
        icon-left="plus"
        style="margin-top: 5px;
    margin-bottom: 5px;"
        @click="isPlaceNumberActive=!isPlaceNumberActive;parkingPlace=true"
      >Num. Place <span v-show="parkingPlace">(E.3,146)</span></b-button>
      <br>
      <b-button type="is-primary" icon-left="euro-sign" @click="estimateModal()">Estimer</b-button>
    </div>

    <div
      class="card"
      v-show="scan"
      style="margin-top: 10px;
    margin-left: 16px;
    margin-right: 16px;"
    >
      <header class="card-header">
        <p class="card-header-title">Places pour les voitures électriques</p>
        <span class="card-header-icon" aria-label="more options">
          <b-icon type="is-success" icon="leaf"></b-icon>
        </span>
      </header>
      <div class="card-content">
        <div class="content">
          <table class="table">
            <thead>
              <tr>
                <th></th>
                <th>
                  <abbr>Num</abbr>
                </th>
                <th>
                  <abbr>Etage</abbr>
                </th>
                <th>
                  <abbr>Dispo.</abbr>
                </th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>
                  <b-icon icon="plug"></b-icon>
                </td>
                <td>146</td>
                <td>1er</td>
                <td>
                  <span class="tag is-success">Oui</span>
                </td>
              </tr>
              <tr>
                <td>
                  <b-icon icon="plug"></b-icon>
                </td>
                <td>213</td>
                <td>2éme</td>
                <td>
                  <span class="tag is-success">Oui</span>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- Display History -->
    <div class="card" style="margin-top: 50px;
    margin-left: 16px;
    margin-right: 16px;">
      <header class="card-header">
        <p class="card-header-title">Historique</p>
        <span class="card-header-icon" aria-label="more options">
          <b-icon icon="history"></b-icon>
        </span>
      </header>
      <div class="card-content">
        <div class="content">
          <table class="table">
            <thead>
              <tr>
                <th></th>
                <th>
                  <abbr>Date</abbr>
                </th>
                <th>
                  <abbr>Parking</abbr>
                </th>
                <th>
                  <abbr>Cout</abbr>
                </th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>
                  <b-icon icon="parking"></b-icon>
                </td>
                <td>11/10/19</td>
                <td>Nice Etoile (Nice)</td>
                <td>5€</td>
              </tr>
              <tr>
                <td>
                  <b-icon icon="parking"></b-icon>
                </td>
                <td>11/10/19</td>
                <td>Polygone Riviera</td>
                <td>10€</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <b-modal :active.sync="isPlaceNumberActive" :width="640" scroll="keep">
      <div class="modal-card" style="width: auto">
        <header class="modal-card-head">
          <p class="modal-card-title">
            <i class="fas fa-parking" aria-hidden="true"></i>
            le QR code de votre Place
          </p>
        </header>
        <section class="modal-card-body">
          <vue-web-cam></vue-web-cam>
        </section>
        <footer class="modal-card-foot">
          <button class="button" type="button" @click="$parent.close()">Fermer</button>
          <button class="button is-primary" @click="$parent.close()">Ok</button>
        </footer>
      </div>
    </b-modal>
  </section>
</template>
<script>
import Camera from "./camera";

export default {
  name: "Home",
  components: {
    "vue-web-cam": Camera
  },
  data() {
    return {
      scan: false,
      parkingPlace:false,
      counter: 0,
      counterInterval: null,
      isPlaceNumberActive: false
    };
  },
  methods: {
    linkToGoogleMap() {
      window.open(
        "https://www.google.fr/maps/place/Parking+Nice+Etoile/@43.7018425,7.2665441,17z/data=!3m1!4b1!4m5!3m4!1s0x12cddaa646352405:0xa5e6ce7f8a1d61d6!8m2!3d43.7018386!4d7.2687328",
        "_blank"
      );
    },
    qRModal() {
      this.scan = true;
      this.$buefy.modal.open(
        `<p class="image is-4by3">
                        <img src="https://www.dummies.com/wp-content/uploads/324172.image0.jpg">
                    </p>`
      );
    },
    estimateModal() {
      this.scan = true;
      this.$buefy.modal.open(
        `
          <div class="modal-card" style="width: auto">
                    <header class="modal-card-head">
                        <p class="modal-card-title">
        <i class="fas fa-euro-sign" aria-hidden="true"></i>
        Estimation   
                        </p>
                    </header>
                    <section class="modal-card-body">
                   <p style="text-align:center">Actuellement vous avez Dépensé <u>10 minutes</u>
                   </p>
                   <p style="text-align:center"> <b>5€</b> </p>
                    </section>
                    <footer class="modal-card-foot">
                        <button class="button" type="button" @click="$parent.close()">Fermer</button>
                        <button class="button is-primary" @click="$parent.close()">Ok</button>
                    </footer>
                </div>
        `
      );
    },

    startCounter() {
      this.stopCounter();
      let start = new Date();
      let consumed = new Date();

      this.counterInterval = setInterval(() => {
        consumed = new Date(new Date().getTime() + 5 * 60000);
        this.counter = this.secondsToHMS(
          Math.trunc((start.getTime() - consumed.getTime()) / 1000) * -1
        );
      }, 1000);
    },
    stopCounter() {
      clearInterval(this.counterInterval);
    },
    secondsToHMS(secs) {
      let z = n => (n < 10 ? "0" : "") + n;
      let sign = secs < 0 ? "-" : "";
      secs = Math.abs(secs);
      return sign + z((secs / 3600) | 0) + ":" + z(((secs % 3600) / 60) | 0);
    }
  }
};
</script>

<style>
.modal {
  z-index: 99;
}
.modal-card {
  margin-right: 16px !important;
  margin-left: 16px !important;
}
</style>
