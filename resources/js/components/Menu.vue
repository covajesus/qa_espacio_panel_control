<template>
    <div>
        <!-- /.navbar -->
        <!-- Sidebar -->
        <div class="sidebar">
            <!-- Sidebar Menu -->
            <nav class="mt-2">
                <ul class="nav nav-pills nav-sidebar flex-column" data-widget="treeview" role="menu" data-accordion="false">
                    <!-- Add icons to the links using the .nav-icon class
                        with font-awesome or any other icon font library -->
                    <li class="nav-item">
                        <router-link to="/" class="nav-link active" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-home"></i>
                            Inicio
                        </router-link>
                    </li>
                    <li class="nav-item" v-if="add_section == 1 || edit_section == 1 || delete_section == 1 || copy_section == 1 || order_section == 1">
                        <router-link to="/sections" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-puzzle-piece"></i>
                            Secciones
                        </router-link>
                    </li>
                    <li class="nav-item" v-if="add_category == 1 || edit_category == 1 || delete_category == 1 ||copy_category == 1 || order_category == 1">
                        <router-link to="/categories" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-stairs"></i>
                            Categorías
                        </router-link>
                    </li>
                    <li class="nav-item" v-if="add_content == 1 || edit_content == 1 || delete_content == 1 || copy_content == 1 || order_content == 1">
                        <router-link to="/contents" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-newspaper"></i>
                            Contenidos
                        </router-link>
                    </li>
                    <li class="nav-item" v-if="watch_audit == 1">
                        <router-link to="/audits" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-magnifying-glass"></i>
                            Auditorías
                        </router-link>
                    </li>
                    <li class="nav-item" v-if="add_rol == 1 || edit_rol == 1 || delete_rol == 1">
                        <router-link to="/rols" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-user-lock"></i>
                            Rols
                        </router-link>
                    </li>
                    <li class="nav-item" v-if="add_user == 1 || edit_user == 1 || delete_user == 1">
                        <router-link to="/users" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-users"></i>
                            Usuarios
                        </router-link>
                    </li>
                    <li class="nav-item">
                        <router-link to="/settings" class="nav-link" data-widget="pushmenu" @click="toggleSidebar">
                            <i class="nav-icon fas fa-user"></i>
                            Perfil
                        </router-link>
                    </li>
                    <li class="nav-item">
                        <a @click="Logout" href="javascript:;" class="nav-link">
                            <i class="nav-icon fas fa-door-open"></i>
                            Salir
                        </a>
                    </li>
                </ul>
            </nav>
            <!-- /.sidebar-menu -->
        </div>
        <!-- /.sidebar -->
    </div>
  </template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            rol_id: '',
            sidebarVisible: true,
            add_section: '',
            edit_section: '',
            delete_section: '',
            copy_section: '',
            order_section: '',
            add_category: '',
            edit_category: '',
            delete_category: '',
            copy_category: '',
            order_category: '',
            add_content: '',
            edit_content: '',
            delete_content: '',
            copy_content: '',
            order_content: '',
            watch_audit: '',
            add_user: '',
            edit_user: '',
            delete_user: '',
            add_rol: '',
            edit_rol: '',
            delete_rol: '',
        }
    },
    methods: {
        toggleSidebar() {
            const pushMenuBtn = this.$refs.pushMenuBtn;

            $(pushMenuBtn).PushMenu('toggle');
        },
        Logout() {
            const token = localStorage.getItem('token')

            localStorage.removeItem('token');
            localStorage.removeItem('id');
            localStorage.removeItem('rol_id');
            localStorage.removeItem('names');
            localStorage.removeItem('email');
            localStorage.removeItem('add_section');
            localStorage.removeItem('edit_section');
            localStorage.removeItem('delete_section');
            localStorage.removeItem('copy_section');
            localStorage.removeItem('order_section');
            localStorage.removeItem('add_category');
            localStorage.removeItem('edit_category');
            localStorage.removeItem('delete_category');
            localStorage.removeItem('copy_category');
            localStorage.removeItem('order_category');
            localStorage.removeItem('add_content');
            localStorage.removeItem('edit_content');
            localStorage.removeItem('delete_content');
            localStorage.removeItem('copy_content');
            localStorage.removeItem('order_content');
            localStorage.removeItem('watch_audit');
            localStorage.removeItem('add_user');
            localStorage.removeItem('edit_user');
            localStorage.removeItem('delete_user');
            localStorage.removeItem('add_rol');
            localStorage.removeItem('edit_rol');
            localStorage.removeItem('delete_rol');
            
            window.location.href = '/';
        },
        get_permissions(rol_id) {
            axios
                .get("https://qa.paneldecontrolem.cl/api/rol/" + rol_id)
                .then((response) => {
                    this.add_section = response.data.rol_permissions.add_section;
                    this.edit_section = response.data.rol_permissions.edit_section;
                    this.delete_section = response.data.rol_permissions.delete_section;
                    this.copy_section = response.data.rol_permissions.copy_section;
                    this.order_section = response.data.rol_permissions.order_section;
                    this.add_category = response.data.rol_permissions.add_category;
                    this.edit_category = response.data.rol_permissions.edit_category;
                    this.delete_category = response.data.rol_permissions.delete_category;
                    this.copy_category = response.data.rol_permissions.copy_category;
                    this.order_category = response.data.rol_permissions.order_category;
                    this.add_content = response.data.rol_permissions.add_content;
                    this.edit_content = response.data.rol_permissions.edit_content;
                    this.delete_content = response.data.rol_permissions.delete_content;
                    this.copy_content = response.data.rol_permissions.copy_content;
                    this.order_content = response.data.rol_permissions.order_content;
                    this.watch_audit = response.data.rol_permissions.watch_audit;
                    this.add_user = response.data.rol_permissions.add_user;
                    this.edit_user = response.data.rol_permissions.edit_user;
                    this.delete_user = response.data.rol_permissions.delete_user;
                    this.add_rol = response.data.rol_permissions.add_rol;
                    this.edit_rol = response.data.rol_permissions.edit_rol;
                    this.delete_rol = response.data.rol_permissions.delete_rol;
                    

                    localStorage.setItem('add_section', response.data.rol_permissions.add_section)
                    localStorage.setItem('edit_section', response.data.rol_permissions.edit_section)
                    localStorage.setItem('delete_section', response.data.rol_permissions.delete_section)
                    localStorage.setItem('copy_section', response.data.rol_permissions.copy_section)
                    localStorage.setItem('order_section', response.data.rol_permissions.order_section)
                    localStorage.setItem('add_category', response.data.rol_permissions.add_category)
                    localStorage.setItem('edit_category', response.data.rol_permissions.edit_category)
                    localStorage.setItem('delete_category', response.data.rol_permissions.delete_category)
                    localStorage.setItem('copy_category', response.data.rol_permissions.copy_category)
                    localStorage.setItem('order_category', response.data.rol_permissions.order_category)
                    localStorage.setItem('add_content', response.data.rol_permissions.add_content)
                    localStorage.setItem('edit_content', response.data.rol_permissions.edit_content)
                    localStorage.setItem('delete_content', response.data.rol_permissions.delete_content)
                    localStorage.setItem('copy_content', response.data.rol_permissions.copy_content)
                    localStorage.setItem('order_content', response.data.rol_permissions.order_content)
                    localStorage.setItem('watch_audit', response.data.rol_permissions.watch_audit)
                    localStorage.setItem('add_user', response.data.rol_permissions.add_user)
                    localStorage.setItem('edit_user', response.data.rol_permissions.edit_user)
                    localStorage.setItem('delete_user', response.data.rol_permissions.delete_user)
                    localStorage.setItem('add_rol', response.data.rol_permissions.add_rol)
                    localStorage.setItem('edit_rol', response.data.rol_permissions.edit_rol)
                    localStorage.setItem('delete_rol', response.data.rol_permissions.delete_rol)
                })
                .catch((error) => {
                    if (
                        error ==
                        "AxiosError: Request failed with status code 401"
                    ) {
                        this.incorrect_login_data = true;
                        this.loading = false;
                    }
                });
            },
    },
    async created() {
        this.get_permissions(localStorage.getItem('rol_id'));

        this.rol_id = localStorage.getItem('rol_id');

        
    }
}
</script>