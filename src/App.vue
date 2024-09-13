<template>
  <div id="app" :style="{ backgroundColor: backgroundColor }">
    <header>
      <h1>Welcome to My Project</h1>
    </header>

    <main>
      <div class="content">
        <section class="card">
          <h2>Click Counter</h2>
          <div class="counter">
            <p>Count: {{ count }}</p>
            <div class="counter-buttons">
              <button @click="decrementCount" class="btn decrement-btn">-</button>
              <button @click="incrementCount" class="btn increment-btn">+</button>
            </div>
          </div>
        </section>

        <section class="card carousel-section">
          <h2>Image Carousel</h2>
          <div class="carousel">
            <img :src="currentImage" alt="Carousel Image" class="carousel-image" />
            <div class="carousel-controls">
              <button @click="prevImage" class="btn">Previous</button>
              <button @click="nextImage" class="btn">Next</button>
            </div>
          </div>
        </section>

        <section class="card">
          <h2>Change Background Color</h2>
          <div class="current-color-box" :style="{ backgroundColor: backgroundColor }"></div>
          <div class="color-changer">
            <button @click="changeBackgroundColor" class="btn">Change Color</button>
          </div>
          <div class="color-options">
            <h3>Select a Color:</h3>
            <div class="color-picker">
              <button
                v-for="(color, index) in colors"
                :key="index"
                :style="{ backgroundColor: color }"
                @click="setColor(color)"
                class="color-btn"
              ></button>
            </div>
          </div>
        </section>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
      backgroundColor: '#2F4F4F',
      images: [
        'https://i.pinimg.com/564x/49/59/f0/4959f007d6ed0f02ca5743a8b2bd223b.jpg',
        'https://i.pinimg.com/564x/59/17/b3/5917b3a1286508193a4f751585e47466.jpg',
        'https://i.pinimg.com/736x/7b/0a/be/7b0abe7dd01ed2debd46e91a251d3442.jpg',
        'https://i.pinimg.com/736x/b0/ef/82/b0ef8243550c4baf6de4d6027e45abd3.jpg',
        'https://i.pinimg.com/564x/89/c2/43/89c2438a7d9994d4ba095eb79304f394.jpg',
        'https://i.pinimg.com/564x/b3/b2/ca/b3b2caabfcb0b93be1b4201ed5d8bf12.jpg',
        'https://i.pinimg.com/736x/5b/73/26/5b73263ee7c1836c145ca404bb999736.jpg'
      ],
      currentImageIndex: 0,
      colors: ['#72EDF2', '#5151E5', '#FF6F61', '#FFCE00', '#4CAF50', '#FFEB3B', '#FFC107', '#673AB7',
        '#FF5725', '#9C27B0']
    };
  },
  computed: {
    currentImage() {
      return this.images[this.currentImageIndex];
    }
  },
  methods: {
    incrementCount() {
      this.count++;
    },
    decrementCount() {
      if (this.count > 0) {
        this.count--;
      }
    },
    changeBackgroundColor() {
      const randomIndex = Math.floor(Math.random() * this.colors.length);
      this.backgroundColor = this.colors[randomIndex];
    },
    setColor(color) {
      this.backgroundColor = color;
    },
    nextImage() {
      this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length;
    },
    prevImage() {
      this.currentImageIndex =
        (this.currentImageIndex - 1 + this.images.length) % this.images.length;
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap');

/* General Styling */
html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#app {
  font-family: 'Poppins', sans-serif;
  text-align: center;
  color: #e0e0e0;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background: linear-gradient(135deg, #1E1E1E, #2F4F4F);
  transition: background-color 0.5s ease;
}

header {
  margin-bottom: 30px;
}

h1 {
  color: #00d4ff;
  margin: 0;
  font-size: 3em;
 text-shadow: 0 1px 2px rgba(0, 212, 255, 0.3), 0 2px 4px rgba(0, 212, 255, 0.2);
}

/* Layout and Grid */
.content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  max-width: 1200px;
  width: 100%;
}

/* Card Styling */
.card {
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 15px;
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
  color: #fff;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2), 0 4px 8px rgba(0,0,0,0.1);

}

/* Counter Section */
.counter {
  font-size: 2em;
  margin: 10px 0;
}

.counter-buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

/* Buttons Styling */
.btn {
  background-color: #00d4ff;
  color: #fff;
  border: none;
  padding: 14px 28px;
  border-radius: 30px;
  cursor: pointer;
  transition: background-color 0.4s ease-in-out, transform 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 212, 255, 0.2), 0 1px 3px rgba(0, 0, 0, 0.1);
}

.btn:hover {
  background-color: #FF6F61;
  transform: scale(1.05);
}

/* Increment and Decrement Buttons */
.increment-btn {
  background-color: #00d4ff;
}

.decrement-btn {
  background-color: #FF6F61;
}

/* Carousel Styling */
.carousel-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.carousel {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.carousel-image {
  width: 100%;
  max-width: 350px;
  height: auto;
  border-radius: 15px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  margin-bottom: 10px;
  transition: transform 0.3s ease;
}

.carousel-image:hover {
  transform: scale(1.05);
}

/* Color Picker Styling */
.color-picker {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.current-color-box {
  width: 100px;
  height: 100px;
  margin: 10px auto 20px;
  border-radius: 15px;
  border: 2px solid #fff;
  transition: background-color 0.3s ease;
}

.color-btn {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin: 5px;
  border: none;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.color-btn:hover {
  transform: scale(1.2);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}
</style>