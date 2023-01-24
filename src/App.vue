<template>
  <div id="app" @keydown.esc="closeModal">
    <!-- Tugas:
    1. Buat supaya modal login tidak muncul saat page pertama dibuka
    2. Buat tombol login pada navbar untuk menampilkan modal
    3. Tambahkan tombol X pada kanan atas modal
    4. Buat fitur untuk menutup modal saat: 
        - Klik tombol batal
        - Klik tombol X yang dibuat pada nomor 3
        - Klik area diluar modal
        - Tekan tombol escape pada keyboard
    5. Reset form email & password agar selalu kosong saat modal dibuka
    6. Tambahkan animasi sederhana saat modal muncul & menghilang
    
    Penilaian:
    - Kerapian & efisiensi code
    - Metode yang digunakan dalam manipulasi DOM
    - Metode animasi yang digunakan
    
    Tips: untuk menggunakan library, bisa klik tulisan "JavaScript + No-Library (pure JS)" dibawah.
     -->

    <nav>
      <div class="container">
        <a id="login" href="#" @click.prevent="showModal">Login</a>
      </div>
    </nav>

    <div
      class="modal"
      :class="{ showModal: isActive }"
      @click.prevent="closeOutModal"
    >
      <div class="modal-box" ref="modalBox">
        <div class="close" @click.prevent="closeModal">&times;</div>
        <form id="myForm" ref="reset">
          <div class="form-control">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              placeholder="john@example.com"
              class="form-input"
            />
          </div>
          <div class="form-control">
            <label for="password">Password</label>
            <input type="password" id="password" class="form-input" />
          </div>
          <div style="text-align: right">
            <button class="btn batal" @click.prevent="closeModal">Batal</button>
            <button class="btn btn-primary">Masuk</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data: function () {
    return {
      isActive: false,
    };
  },

  methods: {
    showModal() {
      this.isActive = !this.isActive;
    },
    closeModal() {
      this.isActive = false;
      // reset form
      this.$refs.reset.reset();
    },
    closeOutModal(e) {
      // area close
      if (e.target.matches(".modal")) {
        this.isActive = false;
        // reset form
        this.$refs.reset.reset();
      }
    },
  },
};
</script>

<style>
#app {
}

* {
  box-sizing: border-box;
}
body {
  font-family: arial;
  margin: 0;
}
nav {
  background-color: #2277ff;
  color: white;
}
.container {
  /* width: 1024px; */
  width: 100%;
  margin: 0 auto;
}
nav .container {
  display: flex;
  justify-content: flex-end;
}
nav .container a {
  padding: 0.5rem 1rem;
  display: inline-block;
}

.modal {
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  position: fixed;
  top: 0;
  left: 0;
  justify-content: center;
  align-items: center;
  opacity: 0;
}

.showModal {
  bottom: 0;
  right: 0;
  opacity: 1;
  transition: opacity ease-in-out 300ms;
}

.modal-box {
  background-color: white;
  width: 100%;
  max-width: 24rem;
  padding: 1rem;
  position: relative;
}

.close {
  position: absolute;
  top: -15px;
  right: -15px;
  width: 25px;
  height: 25px;
  background: coral;
  color: white;
  text-align: center;
  line-height: 25px;
  border-radius: 15px;
  cursor: pointer;
}

.form-input {
  border: 1px solid #ccc;
  border-radius: 0.2rem;
  display: block;
  padding: 0.5rem 1rem;
  width: 100%;
}

.form-control {
  margin-bottom: 1rem;
}
.form-control label {
  font-weight: 500;
  font-size: 0.875rem;
}

.btn {
  border-width: 1px;
  border-radius: 0.2rem;
  padding: 0.5rem 1rem;
  border-color: #eeeeee;
  background-color: #eeeeee;
}
.btn-primary {
  border-color: #2277ff;
  background-color: #2277ff;
  color: white;
}

a {
  text-decoration: none;
  color: white;
  font-weight: bold;
}
</style>
