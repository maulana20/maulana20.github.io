---
layout: post
title: Cara Mudah Install Vue Template Pada Laravel
github: https://www.techiediaries.com/laravel/how-to-install-vuejs-in-laravel-6-7-by-example/
image: data:image/png;base64,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
language: vue | Laravel
---

### 1. Menginstall Depedency
Di sini kita perlu menginstall depedency pada laravel untuk menghubungkan dengan ui Vue nantinya.
```bash
composer require laravel/ui
```

Kemudian install Vue.
```bash
php artisan ui vue
```

```bash
npm install
```

### 2. Membuat Component
Pada langkah ini kita akan membuat contoh component baru pada `resources\js\components\Attachment.vue`.
```bash
<template>
    <div>
        <div>
            <div v-for="attachment in dataAttachments" v-bind:key="attachment.id" class="mb-3">
                <div>
                    <a :href="attachment.full_url" target="_blank">{{ ( attachment.title ? attachment.title : getFileName(attachment.url) ) }}</a>
                    <input type="hidden" name="update_attachment[]" :value="attachment.id"/>
                    <button type="button" class="btn btn-nooutline btn-nooutline-main"  onclick="this.parentNode.parentNode.removeChild(this.parentNode);"><i class="fas fa-times"></i></button>
               </div>
            </div>
            <div v-for="(attachment, index) in attachments" v-bind:key="index" class="mb-3">
                <div class="p-1 border d-inline-block">
                    <input type="file" name="attachments[]" accept=".pdf,application/msword,application/vnd.ms-excel,application/vnd.openxmlformats-officedocument.wordprocessingml.document" required>
                </div>
                <button type="button" class="btn btn-nooutline btn-nooutline-main" onclick="this.parentNode.parentNode.removeChild(this.parentNode);"><i class="fas fa-times"></i></button>
            </div>
            <div>
                <button type="button" class="btn btn-outline btn-outline-main" v-on:click="addFieldAttach">Add More</button>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        props: {
            db: Array,
        },
        data() {
            return {
                attachments : [],
                dataAttachments: []
            }
        },
        mounted: function() {
            this.setAttachments()
        },
        methods: {
            setAttachments: function() {
                this.dataAttachments = this.db
            },
            addFieldAttach: function() {
                this.attachments.push({})
            },
            getFileName: function (str) {
                return new String(str).substring(str.lastIndexOf('/') + 1);
            }
        }
    }
</script>
```

Tambahkan component yang telah kita buat pada `resources\js\app.js`.
```bash
Vue.component('attachment', require('./components/Attachment.vue').default);
```

Panggil pada view blade.
```bash
<attachment :db="[]"></attachment>
```

Kemudian generate vue dengan menjalankan perintah.

Development
```bash
npm run watch/dev
```
Production
```bash
npm run prod
```

### Catatan
- Jika component yang kita buat tidak tampil, pastikan pada layout dalam body di panggil id `app` nya.
- Jika styling mengalami perubahan, pastikan pada `resources\sass\*` kalian kembalikan ke semula.
- Jika terdapat plugin pada `resources\js\app.js` sebelumnya, kalian bisa kembalikan plugin tersebut cukup bagian require nya saja.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.techiediaries.com/laravel/how-to-install-vuejs-in-laravel-6-7-by-example/) tersebut.
