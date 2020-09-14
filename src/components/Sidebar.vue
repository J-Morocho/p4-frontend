<template>
    <div class="sidebar-page">
        <section class="sidebar-layout">
             <b-sidebar
                position="static"
                :mobile="mobile"
                :expand-on-hover="expandOnHover"
                :reduce="reduce"
                type="is-light"
                open
            >
                <div class="p-1">
                    <div class="block">
                    </div>
                    <b-menu class="is-custom-mobile">
                        <b-menu-list label="Categories">
                            <b-menu-item icon="logout" label="Logout"></b-menu-item>
                        </b-menu-list>
                    </b-menu>
                </div>
            </b-sidebar>

        </section>
    </div>
</template>

<style scoped>

.p-1 {
    background-color: #E9E9E9;
}

.sidebar-page {
    height: 100vh;
    background-color: #E9E9E9;;
};
</style>