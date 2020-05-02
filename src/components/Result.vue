<template>
  <div class="card">
    <div class="card-horizontal">
      <div class="img-thumbnail m-2">
        <img :src="this.result.image" />
      </div>
      <div class="card-body">
        <h4 class="card-title">{{ this.result.title }}</h4>
        <p class="card-text">{{ this.result.description }}</p>
        <p v-html="customText">{{ this.result.customText }}</p>
      </div>
    </div>
    <div class="card-footer">
      <div class="row">
        <div class="col">
          <div class="btn-group" role="group">
            <button
              type="button"
              class="btn btn-light btn-sm"
              data-toggle="modal"
              :data-target="`#${this.result.source}Modal`"
            >
              <font-awesome-icon icon="eye" />
            </button>
            <a role="button" :href="this.result.link" target="_blank" class="btn btn-light btn-sm">
              <font-awesome-icon icon="external-link-alt" />
            </a>
            <!-- <button type="button" class="btn btn-light btn-sm" @click="generatePDF">
              <font-awesome-icon icon="file-download" />
            </button>-->
            <!-- <button type="button" class="btn btn-light btn-sm" @click="printPDF">
              <font-awesome-icon icon="print" />
            </button> -->
          </div>
        </div>
        <!-- <div class="col text-right">
          <img src="assets\wikipedia-footer.png" class="footer-icon" />
        </div> -->
      </div>
    </div>
    <div
      class="modal fade"
      :id="`${this.result.source}Modal`"
      tabindex="-1"
      role="dialog"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-xl" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <iframe :src="this.result.modalLink" width="100%"></iframe>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
    result: Object
  },
  data: function() {
    return {
      customText: null
    };
  },
  methods: {
    //   request: function(url, onload) {
    //     console.debug(`New request\n${url}`);
    //     var request = new XMLHttpRequest();
    //     request.open("GET", url, true);

    //     request.onload = function() {
    //       if (this.status >= 200 && this.status < 400) {
    //         console.debug(`Request successful\n${url}.`);
    //         onload(this.response);
    //       } else {
    //         // We reached our target server, but it returned an error
    //         console.error(`Server error for ${url}.`);
    //       }
    //     };

    //     request.onerror = function() {
    //       // There was a connection error of some sort
    //       console.error(`Connection error for ${url}.`);
    //     };

    //     request.send();
    //   },
    //   generatePDF: function() {
    //     this.request(
    //       `http://api.pdflayer.com/api/convert?access_key=194b887f0fc2e87df8b4abadb1b20c79&document_url=${this.result.link}`,
    //       function(data) {
    //         document.getElementById
    //       }
    //     );
    //   }
    // printPDF: function() {
    //   var win = window.open(
    //     this.result.link,
    //     "_blank",
    //     "height=600,width=800"
    //   );
    //   console.log(win);
    //   win.focus();
    //   //win.onload = function() {
    //   //  alert("Hello");
    //   //    print();
    //   //};
    //   //win.onload = "alert('hello');"

    //   setTimeout(function() {
    //     win.print();
    //     win.close();
    //   }, 3000);
    // }
  },
  created() {
    // Check if image doesn't exist
    // if (this.result.source && this.result.image == null) {
    //   document.getElementsByClassName("img-thumbnail").style.display = "none";
    // }
    this.customText = this.result.customText;
  }
};
</script>

<style scoped>
iframe {
  height: 75vh;
  border: none;
}
.card-horizontal {
  display: flex;
  flex: 1 1 auto;
}
</style>
