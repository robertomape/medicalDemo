<template>
  <div class="xray-viewer">
    <header class="header">
      <div class="logo">PEDIATRX</div>
      <div class="header-buttons">
        <img src="@/assets/Picture11.svg" />
        <img src="@/assets/Picture12.svg" />
        <img src="@/assets/Picture13.svg" />
        <img src="@/assets/Picture14.svg" />
        <img src="@/assets/Picture15.svg" style="margin-right: 1000px;"/>
        <img src="@/assets/Picture8.svg" />
        <img src="@/assets/Picture10.svg" alt="Arrow"/>
        <button :class="['run-button', { 'disabled': isLoading }]" @click="startLoading">{{ runButtonText }}</button>
      </div>
    </header>
    <div class="content">
      <div class="thumbnails" v-if="showThumbnails">
        <div class="thumbnail">
          <img :src="imageSrc" alt="X-ray 1" />
          <p>
            Study description: X-ray<br />Series des: Low
            <a href="#">Contrast</a>
          </p>
        </div>
        <div class="thumbnail">
          <img :src="imageSrc" alt="X-ray 2" />
          <p>
            Study description: X-ray<br />Series des: Noise
            <a href="#">Reduction</a>
          </p>
        </div>
      </div>
      <div class="thumbnails" v-if="!showThumbnails">
        <div class="thumbnailresults">
          <div class="results-panel">
            <div class="header">
              <span>RESULTS</span>
              <div class="status-lights">
                <div class="light red"></div>
                <div class="light yellow"></div>
                <div class="light green"></div>
              </div>
            </div>
            <div class="section">
              <h3>LESIONS DETECTED</h3>
              <div class="item">
                <span>INFILTRATES</span>
                <span>70%</span>
              </div>
              <div class="item">
                <span>ATELECTASIS</span>
                <span>82%</span>
              </div>
              <div class="item">
                <span>CONSOLIDATION</span>
                <span>20%</span>
              </div>
              <div class="item">
                <span>PLEURAL EFFUSION</span>
                <span>10%</span>
              </div>
            </div>
            <div class="section">
              <h3>PATHOGEN</h3>
              <div class="item">
                <span>VIRAL</span>
                <span>89%</span>
              </div>
              <div class="item">
                <span>BACTERIAL</span>
                <span>11%</span>
              </div>
            </div>
            <div class="footer">
              <span>POSIBLE PNEUMONIA</span>
              <span class="percentage">90%</span>
            </div>
          </div>
        </div>
      </div>
      <div class="main-image">
        <img :src="mainImageSrc" alt="Main X-ray" />
      </div>
      <div class="patient-info">
        <div class="patient-info-pack">
          <p><span>Patient ID:</span> 1343254</p>
          <p><span>Study date:</span> 13052024</p>
          <p><span>History:</span></p>
          <p><span>Patient age:</span> 05</p>
          <p><span>Patient sex:</span> male</p>
          <p><span>Study description:</span> X-ray</p>
          <p><span>Series description:</span> High <a href="#">Contrast</a></p>
          <p><span>Modality:</span> X-ray</p>
        </div>
      </div>
    </div>
    <div v-if="isLoading" class="loading-bar-container">
      <div class="loading-bar">
        <div class="loading-progress"></div>
      </div>
      <p class="loading-text">Loading...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "XRayViewer",
  data() {
    return {
      imageSrc: require("@/assets/Picture1.png"),
      mainImageSrc: require("@/assets/Picture1.png"),
      isLoading: false,
      showThumbnails: true,
      runButtonText: 'RUN' // Nuevo estado para el texto del botón
    };
  },
  methods: {
    startLoading() {
      if (this.isLoading) return;
      this.isLoading = true;
      this.runButtonText = 'Generating Info...'; // Cambiar el texto del botón al hacer clic
      setTimeout(() => {
        this.mainImageSrc = require("@/assets/Picture2.png");
        this.isLoading = false;
        this.showThumbnails = false;
        this.runButtonText = 'Generate Info'; // Cambiar el texto del botón después de la carga
      }, 3000); // Cambia la imagen después de 3 segundos
    },
  },
};
</script>

<style scoped>
.xray-viewer {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background-color: #1e1e1e;
  color: white;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #4a4a4a;
  padding: 10px;
}

.logo {
  font-size: 24px;
}

.header-buttons {
  display: flex;
  gap: 10px;
}

.header-buttons button {
  border: none;
  color: white;
  cursor: pointer;
  background: none;
}

.run-button {
  background-color: #076fde !important;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  font-weight: bold;
  color: white;
}

.run-button.disabled {
  background-color: gray;
  cursor: not-allowed;
}

.content {
  display: flex;
  flex-grow: 1;
}

.thumbnails {
  display: flex;
  flex-direction: column;
  gap: 5px;
  background-color: #2e2e2e;
  padding: 5px;
}

.thumbnail {
  background-color: black;
  padding: 10px;
  border-radius: 5px;
  text-align: center;
  width: 300px;
}

.thumbnail img {
  width: 100%;
  height: auto;
  border-radius: 5px;
}

.thumbnail p {
  font-size: 14px;
}

.thumbnail a {
  color: #ff7f50;
  text-decoration: underline;
}

.main-image {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  background-color: black;
  position: relative;
  padding: 10px;
  width: 100%;
}

.main-image img {
  width: 70%;
}

.patient-info {
  text-align: right;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  background-color: black;
  width: 30%;
}

.patient-info p {
  margin: 0;
}

.patient-info-pack {
  position: absolute;
  margin: 0;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
  padding-right: 10px;
}

.patient-info span {
  font-weight: bold;
}

.patient-info a {
  color: #06fff3;
  text-decoration: underline;
}

.loading-bar-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  background-color: rgba(30, 30, 30, 0.9);
  color: white;
  text-align: center;
}

.loading-bar {
  position: relative;
  width: 80%;
  height: 30px;
  background-color: #4a4a4a;
  border-radius: 5px;
  overflow: hidden;
  margin-bottom: 20px;
}

.loading-progress {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #007bff;
  animation: loading 2s infinite;
}

@keyframes loading {
  0% {
    transform: translateX(-100%);
  }
  50% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(100%);
  }
}

.loading-text {
  font-size: 18px;
  font-weight: bold;
}

/*TABLA CONTENIDOS DE RESULTADO*/
.results-panel {
  width: 250px;
  background-color: #4a4a4a;
  border-radius: 10px;
  padding: 10px;
  color: white;
  font-family: Arial, sans-serif;
  position: absolute;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 10px;
  border-bottom: 1px solid #333;
}

.status-lights {
  display: flex;
  gap: 5px;
}

.light {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.red {
  background-color: red;
}

.yellow {
  background-color: yellow;
}

.green {
  background-color: green;
}

.section {
  margin: 10px 0;
}

.section h3 {
  margin: 5px 0;
  font-size: 14px;
  font-weight: bold;
  text-align: center;
  background-color: #5a5a5a;
  padding: 5px;
  border-radius: 5px;
}

.item {
  display: flex;
  justify-content: space-between;
  padding: 5px 0;
}

.footer {
  background-color: #5a5a5a;
  padding: 10px;
  border-radius: 5px;
  text-align: center;
  font-weight: bold;
}

.percentage {
  display: block;
  font-size: 18px;
  margin-top: 5px;
}

.thumbnailresults {
  padding: 10px;
  border-radius: 5px;
  text-align: center;
  width: 300px;
}
</style>
