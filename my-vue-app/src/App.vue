<template>

  <navbar
      :pages="pages"
      :active-page="activePage"
      :nav-link-click="(index) => activePage = index">
  </navbar>

  <PageViewer
      :page="pages[activePage]">
  </PageViewer>
  

</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue'

export default {
  components: {
      PageViewer,
      Navbar
  },
  data() {
      return {
          activePage: 0,
          pages: [
              {
                  link: { text: 'Home', url: "index.html" },
                  pageTitle: 'Home Page',
                  content: 'This is the Home Content',
              },
              {
                  link: { text: 'About', url: "About.html" },
                  pageTitle: 'About Page',
                  content: 'This is the About Content',
              },
              {
                  link: { text: 'Contact', url: "Contact.html" },
                  pageTitle: 'Contact Page',
                  content: 'This is the Contact Content',
              }
          ],
      };
  },
}
</script>