<!-- <template>
    <div>
      <div v-for="(videoUrl, index) in videoUrls" :key="index" class="youtube-container">
        <div width="400" height="400">
        <iframe :src="videoUrl" frameborder="0" allowfullscreen width="200" height="200"></iframe>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        videoUrls: [ 
        'https://www.youtube.com/embed/-lgYPgpEXEs',
        'https://www.youtube.com/embed/82EvWpWSogM',
        'https://www.youtube.com/embed/HCbisGApCy4',
        'https://www.youtube.com/embed/96lOJ-QwFsw',
        'https://www.youtube.com/embed/U3AWs1nC5I4',
        'https://www.youtube.com/embed/JqRl0cDBGeI',
        'https://www.youtube.com/embed/GcAWYSc369w',
        'https://www.youtube.com/embed/kr7f3MeAyOk' ,
        'https://www.youtube.com/embed/_STgFkHTaBQ' ,
        'https://www.youtube.com/embed/dzGT6BCLHHc' ,
        'https://www.youtube.com/embed/vid6hyL7gBg'    
       
      ]
      };
    }
  };
  </script>
  
  <style scoped>
  .youtube-container {
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 56.25%; /* Aspect ratio 16:9 */
    overflow: hidden;
    margin-bottom: 20px; /* Optional: Add some spacing between videos */
  }
  
  .youtube-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  </style> -->

  <template>
    <div><h2>Class 10 Animated Videos</h2>
      <div class="button-container">
        <button 
          v-for="(video, index) in videoUrls" 
          :key="index" 
          :style="{ backgroundColor: buttonColors[index] }" 
          @click="selectVideo(video.url)">
          {{ index + 1 }}. {{ video.title }}
        </button>
      </div>
      <div class="youtube-container" v-if="selectedVideoUrl">
        <iframe :src="selectedVideoUrl" frameborder="0" allowfullscreen></iframe>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        videoUrls: [
          { title: 'Solar System part1', url: 'https://www.youtube.com/embed/-lgYPgpEXEs' },
          { title: 'Solar System Part2', url: 'https://www.youtube.com/embed/82EvWpWSogM' },
          { title: 'Newtons Law', url: 'https://www.youtube.com/embed/HCbisGApCy4' },
          { title: 'Electricity', url: 'https://www.youtube.com/embed/96lOJ-QwFsw' },
          { title: 'Magnetism', url: 'https://www.youtube.com/embed/U3AWs1nC5I4' },
          { title: 'Coin and Feature Experiment', url: 'https://www.youtube.com/embed/JqRl0cDBGeI' },
          { title: 'Universal Law of Motion', url: 'https://www.youtube.com/embed/GcAWYSc369w' },
          { title: 'Human Eye', url: 'https://www.youtube.com/embed/kr7f3MeAyOk' },
          { title: 'Trigonometry', url: 'https://www.youtube.com/embed/_STgFkHTaBQ' },
          { title: 'Mathematical Construct', url: 'https://www.youtube.com/embed/dzGT6BCLHHc' },
          { title: 'Probability', url: 'https://www.youtube.com/embed/vid6hyL7gBg' }
        ],
        buttonColors: [
          '#3333FF', '#3333FF', '#3333FF', '#3333FF', 
          '#3333FF', '#3333FF', '#3333FF', '#3333FF', 
          '#3333FF', '#3333FF', '#3333FF'
        ],
        selectedVideoUrl: null
      };
    },
    methods: {
      selectVideo(url) {
        this.selectedVideoUrl = url;
      }
    }
  };
  </script>

<style scoped>
.button-container {
  display: grid;
  grid-template-columns: repeat(5, 1fr); /* Display 5 items per row */
  gap: 10px;
  margin-bottom: 20px;
  justify-items: center; /* Center the buttons horizontally */
}

button {
  padding: 10px 20px;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s, transform 0.3s;
  width: 100%;
  max-width: 300px;
}

button:hover {
  opacity: 0.9;
  transform: scale(1.05);
}

.selected-video-container {
  text-align: center;
  margin-bottom: 20px;
}

.youtube-container {
  position: relative;
  width: 100%;
  height: 0;
  padding-bottom: 56.25%; /* Aspect ratio 16:9 */
  overflow: hidden;
  margin-top: 10px;
}

.youtube-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

@media (max-width: 1200px) {
  .button-container {
    grid-template-columns: repeat(4, 1fr); /* 4 items per row */
  }
}

@media (max-width: 992px) {
  .button-container {
    grid-template-columns: repeat(3, 1fr); /* 3 items per row */
  }
}

@media (max-width: 768px) {
  .button-container {
    grid-template-columns: repeat(2, 1fr); /* 2 items per row */
  }

  button {
    font-size: 14px;
    padding: 8px 16px;
  }

  .youtube-container {
    padding-bottom: 75%; /* Adjust aspect ratio for smaller screens */
  }
}

@media (max-width: 480px) {
  .button-container {
    grid-template-columns: 1fr; /* 1 item per row */
  }

  button {
    font-size: 12px;
    padding: 6px 12px;
  }

  .youtube-container {
    padding-bottom: 100%; /* Adjust aspect ratio for very small screens */
  }
}
</style>
  
  <!-- <style scoped>
  .button-container {
    display: grid;
    grid-template-columns: repeat(6, 1fr); /* Display 5 items per row */
    gap: 5px;
    margin-bottom: 20px;
    justify-items: center; /* Center the buttons horizontally */
  }
  
  button {
    padding: 10px 20px;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px; /* Slightly larger font size for better readability */
    transition: background-color 0.3s, transform 0.3s;
    width: 100%; /* Make buttons take the full width */
    max-width: 300px; /* Optional: Limit the maximum width */
  }
  
  button:hover {
    opacity: 0.9;
    transform: scale(1.05); /* Slightly enlarge the button on hover */
  }
  
  .youtube-container {
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 56.25%; /* Aspect ratio 16:9 */
    overflow: hidden;
    margin-bottom: 20px; /* Optional: Add some spacing between videos */
  }
  
  .youtube-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  .tabs{
    display:grid;
  }
  </style> -->


  

  
  