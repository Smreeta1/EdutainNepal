<template>
<div class="dashboard">
    <div class="sidebar">
        <div class="logo">
            <img src="../assets/student-finger.png" alt="Logo" class="logo-image">
            <div class="profile-detail">

                <p>welcome:{{name }}</p>
                <p>{{ email }}</p>
                <!-- <p>Time:{{ timeSpentInSeconds }}</p> -->
            </div>
        </div>
        <hr>
        <nav class="nav">
            <router-link to="/" class="nav-item">Home</router-link>
            <router-link to="/change-password" class="nav-item">ChangePassword</router-link>
            <button @click="showProgressReport = true" class="nav-item">Generate Report</button>
            <a href="login" class="nav-item" v-on:click="logout">Logout</a>
            
        </nav>
    </div>
    <div class="main-content">
        <div class="landing-page" v-if="!showContent">
        <!-- Landing page content -->
        <div class="landing-page-text">
  <p>Welcome to the Dashboard!</p>
  <p>Select an option from the menu to get started.</p>
        </div>

        <img src="../assets/landing-page-image.png" alt="Landing Page Image" class="landing-page-image">
       
        </div>
        <div v-if="showProgressReport">
          <ProgressReport :quizScore="quizScore" />
      </div>
    </div>
</div>
</template>

<script>
    import axios from 'axios';
    import ProgressReport from './ProgressReport.vue'
    export default {
        name: 'DashboardContent',
        components:{
        ProgressReport
        },
        props:{
           
            quizScore: Number
        
        },
        data() {
            return {
                name: '', // This will store the user's name fetched from the server
                email: '',
                // startTime: new Date(),
                // timeSpentInSeconds: 0
                showProgressReport:false,
                showContent :false,
            };
        },
        // mounted() {
        //     setInterval(this.updateTimeSpent, 1000); // Update every second
        // },
        methods: {
            logout() {
                localStorage.clear();
                this.$router.push({
                    name: 'LogIn'
                });
            },
            fetchUserData() {
                const authToken = JSON.parse(localStorage.getItem("user-value"));
                if (!authToken || !authToken.access) {
                    this.$router.push({
                        name: 'signUp',
                    });
                    return;
                }
                axios.get('https://edunp.pythonanywhere.com/api/profile/', {
                        headers: {
                            'Authorization': `Bearer ${authToken.access}`
                        }
                    })
                    .then(response => {
                        this.name = response.data.name; // Assuming the API returns an object with a 'name' field
                        this.email = response.data.email;
                    })
                    .catch(error => {
                        console.error('Error fetching user data:', error);
                        this.$router.push({
                            name: 'signUp'
                        }); // Redirect to login on error (e.g., token expired)
                    });
            },
            // updateTimeSpent() {
            //     const currentTime = new Date();
            //     const difference = currentTime.getTime() - this.startTime.getTime();
            //     this.timeSpentInSeconds = Math.floor(difference / 1000);
            // },
            // formatTime(seconds) {
            //     const hours = Math.floor(seconds / 3600);
            //     const minutes = Math.floor((seconds % 3600) / 60);
            //     const remainingSeconds = seconds % 60;

            //     return `${this.pad(hours)}:${this.pad(minutes)}:${this.pad(remainingSeconds)}`;
            // },
            // pad(number) {
            //     return (number < 10 ? "0" : "") + number;
            // }
            generateProgressReport() {
      this.showProgressReport = true;
      this.showContent = false; // Hide landing page content when progress report is generated
    }
        },
        mounted() {
            this.fetchUserData(); // Call fetchUserData when component mounts
            // setInterval(this.updateTimeSpent, 1000); // Update every second

        }
    };
</script>

<style scoped>
    .dashboard {
        display: flex;
        height: 100vh;
    }

    .profile-detail {
        color: #efd52d;
    }

    .sidebar {
        width: 250px;
        background-color: #4A90E2;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        height: auto;
    }

    .logo {
        padding: 20px;
    }

    .logo img {
        max-width: 100%;
        border-radius: 50%;
        /* Makes the image round */
    }

    .nav {
        margin-top: 20px;
    }

    .nav-item {
        display: block;
        padding: 10px 20px;
        text-decoration: none;
        color: #333333;
        transition: background-color 0.3s;
        border: 1px solid white;
        border-radius: 10px;
        margin-top: 5px;
        background-color: #4A90E2;
        
    }
    .nav button{
        width:100%;
        font-size:medium;
    }

    .nav-item:hover {
        background-color: #efd52d;
    }

    .main-content {
        flex: 1;
        padding: 20px;
    }

    /* Example profile component */
    .profile {
        background-color: #f5f5f5;
        padding: 20px;
        border-radius: 5px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    /* Media query for mobile devices */
    @media (max-width: 768px) {
        .dashboard {
            flex-direction: column;
            /* Stack sidebar and main content vertically */
        }

        .sidebar {
            width: 100%;
            /* Make sidebar take full width on mobile */
        }

        .nav {
            padding: 0 20px;
            /* Add horizontal padding to nav items */
        }

        .nav-item {
            padding: 10px 0;
            /* Adjust padding of nav items */
            text-align: center;
            /* Center-align nav items */
        }
    }

    .landing-page-image {
  width: calc(100% - 250px); /* Adjust the width based on your layout */
  max-width: 100%; /* Ensure the image does not exceed its container */
  height: auto;
  border-radius: 2px; /* Maintain aspect ratio */
}
.landing-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 0px;
  }

  .landing-page-content {
    border: 2px solid #ccc; /* Border around the image */
    border-radius: 10px;
    padding: 20px;
    margin-top: 20px;
  }

 

  .landing-page-text {
    font-size: 32px;
    font-weight: bold;
    margin-top: 0px;
    font-style:italic;
    transition: color 0.3s;
  }

  .landing-page-text:hover {
  color: #4A90E2; /* Change color on hover */
}
.landing-page-text p {
  overflow: hidden;
  white-space: nowrap;
}

</style>



