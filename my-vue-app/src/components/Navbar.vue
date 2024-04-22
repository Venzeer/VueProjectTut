<template>
    <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-o">
                <li v-for="(page, index) in pages" class="nav-item" :key="index">
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
    props: ['pages', 'activePage', 'navLinkClick'],
    computed: {
        getNextTheme() {
            if (this.theme == 'light') {
                return 'dark'
            } 

            return 'light'
        },
    },
    data() {
        return {
            theme: 'light'
        };
    },
    methods: {
        
        changeTheme() {
            let theme = 'light'
            if (this.theme == 'light') {
                theme = 'dark'
            }

            this.theme = theme
        }
    }      
}
</script>