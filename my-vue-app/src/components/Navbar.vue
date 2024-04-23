<template>
    <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Tutorial</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-o">
                <li v-for="(page, index) in publishedPages" class="nav-item" :key="index">
                    <NavbarLink
                      :page="page"
                      :isActive="activePage == index"
                      @click.prevent="navLinkClick(index)">
                    </NavbarLink>
                    
                </li>
            </ul>

            <form class="d-flex" action="">
                <button 
                    class="btn"
                    :class="`btn-${getNextTheme}`"
                    @click.prevent="changeTheme"> Toggle {{ getNextTheme }} mode</button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';
export default {
    components: {
        NavbarLink
    },
    created() {
        this.getTheme();
    },
    props: ['pages', 'activePage', 'navLinkClick'],
    computed: {
        getNextTheme() {
            if (this.theme == 'light') {
                return 'dark'
            } 

            return 'light'
        },
        publishedPages() {
            return this.pages.filter(pg => pg.published)
        }
    },
    data() {
        return {
            theme: 'light'
        };
    },
    methods: {
        changeTheme() {
            let theme = 'light';
            if (this.theme == 'light') {
                theme = 'dark';
            }

            this.theme = theme;
            this.storeTheme();
        },
        storeTheme() {
            localStorage.setItem('theme', this.theme);
        },
        getTheme() {
            let theme = localStorage.getItem('theme');

            if (theme) {
                this.theme = theme;
            }
        }
    }      
}
</script>