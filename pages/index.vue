<template>
    <div v-if=sessionAuthed>
        <register-login />
    </div>
    <div v-if=!sessionAuthed>
        <topnav />
    </div>
</template>

<script>
import Cookies from 'js-cookie';

export default {
    computed: {
        sessionAuthed() {
            return Cookies.get('Atlas.Affinity.Authed') == null;
        }
    },
    method: {
    }
}


</script>