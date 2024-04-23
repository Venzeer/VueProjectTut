<template>

  <navbar
      :pages="pages"
      :active-page="activePage"
      >
  </navbar>

  <PageViewer
      v-if="pages.length > 0"  
      :page="pages[activePage]">
  </PageViewer>
  
  <create-page
    @page-created="pageCreated">
  </create-page>

</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue'
import CreatePage from './components/CreatePage.vue';

export default {
    components: {
        PageViewer,
        Navbar,
        CreatePage
    },
    created() {
        this.getPages();

        this.$bus.$on('navbarLinkActivated', (index) => {
            this.activePage = index
        })
    },
    data() {
        return {
            activePage: 0,
            pages: [],
        };
    },
    methods: {
        async getPages() {
            let pages = await fetch('pages.json');
            let data = await pages.json();

            this.pages = data
        },
        pageCreated(pageObj){
            this.pages.push(pageObj)
        }
    }
}
</script>