<script lang="ts">
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
//import { getAnalytics } from "firebase/analytics";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyCGV7RzWrZwQOEBghHPo60pYLWdODp29C8",
  authDomain: "piepie-b976e.firebaseapp.com",
  projectId: "piepie-b976e",
  storageBucket: "piepie-b976e.appspot.com",
  messagingSenderId: "158755755592",
  appId: "1:158755755592:web:f8a5d72be8f351ceb82a7d",
  measurementId: "G-YRCS0S5CCE"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
//const analytics = getAnalytics(app);
export default  app;
</script>