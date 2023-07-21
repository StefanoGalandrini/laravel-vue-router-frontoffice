<script>
export default {};
</script>

<template>
  <footer class="footer-distributed container-fluid fixed-bottom">
    <div class="row row-cols row-cols-md row-cols-sm">
      <div class="contents d-flex justify-content-between z-1">
        <div class="footer-left">
          <ul class="footer-links d-flex gap-2">
            <li class="list-unstyled">
              <router-link :to="{ name: 'home' }">
                Home
              </router-link>
            </li>

            <li class="list-unstyled">
              <router-link :to="{ name: 'about' }">
                Chi siamo
              </router-link>
            </li>

            <li class="list-unstyled">
              <router-link :to="{ name: 'drinks' }">
                Cocktails
              </router-link>
            </li>

            <li class="list-unstyled">
              <router-link :to="{ name: 'contacts' }">
                Contacts
              </router-link>
            </li>
          </ul>
          
          <div class="text-light">MixTales &copy; 2023</div>
        </div>

        <div class="footer-right">
          <a href="#"><i class="fa-brands fa-facebook"></i></a>
          <a href="#"><i class="fa-brands fa-twitter"></i></a>
          <a href="#"><i class="fa-brands fa-instagram"></i></a>
          <a href="#"><i class="fa-brands fa-tiktok"></i></a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style lang="scss" scoped>
$primary-color: #da00ff;

li {
  color: $primary-color;
}

/* FOOTER LINKS */

.footer-distributed ul.footer-links {
  font-size: 18px;
  font-weight: bold;
  color: #ffffff;
  margin: 0 0 10px;
  padding: 0;
  transition: ease 0.25s;
}

.footer-distributed ul.footer-links a {
  display: inline-block;
  line-height: 1.8;
  text-decoration: none;
  color: inherit;
  transition: ease 0.25s;
}

.footer-distributed .footer-links a:before {
  font-size: 20px;
  left: 0;
  color: #fff;
  display: inline-block;
  padding-right: 5px;
}

.footer-distributed .footer-links:before {
  content: none;
}

.footer-distributed .footer-right {
  float: right;
  margin-top: 14px;
  max-width: 180px;
}

.footer-distributed .footer-right a {
  display: inline-block;
  width: 35px;
  height: 35px;
  border-radius: 2px;
  font-size: 20px;
  color: #ffffff;
  text-align: center;
  line-height: 35px;
  margin-left: 3px;
  transition: all 0.25s;
}

.footer-distributed .footer-right a:hover {
  transform: scale(1.1);
  -webkit-transform: scale(1.1);
}

.footer-distributed ul.footer-links a:hover {
  text-decoration: underline;
}
</style>
