<template>
  <footer class="footer" id="footer">
    <p>About Us</p>
    <p>© Copyright 2024</p>
    <p>Developed by Artemnchuk</p>
    <div class="contactUS">
      <a href="https://www.facebook.com/artemnchuk"
        ><img src="/public/facebook.svg" alt="facebook"
      /></a>
      <a href="https://www.twitter.com/artemnchuk"
        ><img src="/public/twitter.svg" alt="twitter"
      /></a>
      <a href="https://www.instagram.com/artemnchuk"
      > <img src="/public/instagram.svg" alt="" 
      /></a>
      <a href="https://www.linkedin.com/artemnchuk"
        ><img src="/public/linkedin.svg" alt="linkedin"
      /></a>
      <a href="https://www.github.com/artemnchuk"
      ><img src="/public/github.svg" alt="github" 
      /></a>
    </div>
  </footer>
</template>
<style scoped>
footer {
  min-height: 20vh;
  text-align: center;
  min-width: 100vw;
  padding: 10px;
  background-color: #222831;
}
footer p {
  margin: 5px;
  color: #e6e5e5;
}
img {
  filter: invert(1);
  width: 30px;
  height: 30px;
}
.contactUS {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 10px;
}
a img:hover {
  transition: 0.6s;
  transform: scale(1.2);
}
@media screen and (max-width: 700px) {
  footer {
    min-height: 25vh;
  }
}
</style>
