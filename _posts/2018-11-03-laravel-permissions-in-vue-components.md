---
layout: post
title: Laravel Permissions in Vue Components
published: true
twitter_plug: true
adsense: true
image: https://bit.ly/2RCY0gm
---

I use Spatie's excellent [laravel-permission](https://github.com/spatie/laravel-permission) package in a Laravel 5.7 application to create permissions, assign them to roles, and assign roles to users. I frequently want to check whether an authenticated user has a specific permission. The package includes Blade directives such as @hasrole and @can that can be used in views, but there isn't a standard for checking a user's permission within a Vue component. Passing props to each component can become tiresome and inconsistent. What if there was a better way?

The below, inspired by an older [post](https://medium.com/@sergiturbadenas/how-i-expose-laravel-permissions-in-vue-js-49dd05bedfce) from Sergi Tur Badenas, describes a pattern that can be used in Vue components that are used by a Laravel application to check whether an authenticated user has a specified permission. It should be easy to adjust accordingly for different ACL packages.

<!--excerpt-->

### STEP 1: Add accessor to User model that returns permissions

Add an [accessor](https://laravel.com/docs/5.7/eloquent-mutators#defining-an-accessor) to your User model that returns an array of permission names that the user has.

In app/User.php:

```php
use Spatie\Permission\Models\Permission;
use Illuminate\Support\Facades\Auth;
````

```php
public function getAllPermissionsAttribute() {
  $permissions = [];
    foreach (Permission::all() as $permission) {
      if (Auth::user()->can($permission->name)) {
        $permissions[] = $permission->name;
      }
    }
    return $permissions;
}
```

### STEP 2: Add a global javascript array of the user's permissions

In a file that is rendered on every page, such as resources/views/layouts/app.blade.php, globally define the permissions as a JavaScript array.

```php
<script>
  @auth
    window.Permissions = {!! json_encode(Auth::user()->allPermissions, true) !!};
  @else
    window.Permissions = [];
  @endauth
</script>
```

### STEP 3: Create a global mixins file with a method to check if a user has a permission

[Mixins](https://vuejs.org/v2/guide/mixins.html) are a great way to share functionality across components. In this case, we'll share a method named $can globally, across all components. It accesses the Permissions array that we set in the layout file.

Create a resources/assets/js/mixins/Permissions.vue file. Laravel does not ship with a mixins directory by default, so create the directory if you need to.

The new file should contain:

```php
<script>
  export default {
    methods: {
      $can(permissionName) {
        return Permissions.indexOf(permissionName) !== -1;
      },
    },
  };
</script>
```


### STEP 4: Import the mixin globally

Modify resources/assets/js/app.js to import the mixin

```javascript
import Permissions from './mixins/Permissions';
Vue.mixin(Permissions);
```

### STEP 5: Rebuild assets

If you're not watching your assets for changes.

```npm run dev```


### STEP 6: Check permissions in Vue components as needed

You can now use $can in v-if conditions in templates used by Vue components. 

For example, this would only show "You can edit posts." if a user had the "edit posts" permission:

```html
<div v-if="$can('edit posts')">You can edit posts.</div>
```

You can also access $can in the methods of Vue components.

Remember not to rely on the front-end alone, and always check permissions on the backend as well. 
