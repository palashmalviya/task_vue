<template>
 <ul>
    <router-link to="/">
    <li style="--i:#243b55;--j:#141e30;">
      <span class="icon">
        <ion-icon name="home-outline"></ion-icon>
      </span>
      <span class="title"> Home</span>
    </li>
    </router-link>

    <router-link to="/about">
    <li style="--i:#141e30 ;--j:#243b55;">
    
      <span class="icon">
        <ion-icon name="person-outline"></ion-icon>
      </span>
      <span class="title">About Me</span>
    </li>
    </router-link>
  </ul>
  <router-view/>

  <footer>
        <p>Designed By  @Pa&#8467ash Ma&#8467viya</p>
  </footer>
</template>

<style>
#app {
  font-family: Candara;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

ul {
  position: relative;
  display: flex;
  gap: 25px;
}

ul li {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  list-style: none;
  width: 60px;
  height: 60px;
  border-radius: 60px;
  background: linear-gradient(45deg,#ffffff, #243b5541);

  
  box-shadow: 0 10px 25px rgba(53, 53, 53, 0.5);
  transition: 0.5s;
  cursor: pointer;
}

ul li:hover {
  width: 180px;
  box-shadow: 0 10px 25px rgb(0, 0, 0, 0);
}

ul li::before {
  content: "";
  position: absolute;
  inset: 0;
  opacity: 0;
  border-radius: 60px;
  transition: 0.5s;
  background: linear-gradient(45deg, var(--i), var(--j));
}

ul li:hover::before {
  opacity: 1;
}

ul li::after {
  content: "";
  position: absolute;
  top: 10px;
  width: 100%;
  height: 100%;
  border-radius: 60px;
  opacity: 0;
  transition: 0.5s;
  background: linear-gradient(45deg, var(--i), var(--j));
  filter: blur(20px);
  z-index: -1;
}

ul li:hover::after {
  opacity: 0.5;
}

ul li ion-icon {
  color: rgba(20, 20, 20, 0.644);
  font-size: 1.75em;
  transition: 0.5s;
  transition-delay: 0.25s;
}

ul li:hover ion-icon {
  color: rgb(185, 173, 173);
  font-size: 1.75em;
  transform: scale(0);
  transition-delay: 0s;
}

ul li span {
  position: absolute;
}

ul li .title {
  color: #ffff;
  font-size: 1.2em;
  text-transform: uppercase;
  transform: scale(0);
  transition: 0.5s;
  transition-delay: 0s;
}

ul li:hover .title {
  transform: scale(1);
  transition-delay: 0.25s;
}

footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  bottom: 0;
  background: #1A1E25;
  color: #868c96;
}

footer p {
  font-size:18px;
  padding: 1px 0;
  text-align: center;
}
</style>
