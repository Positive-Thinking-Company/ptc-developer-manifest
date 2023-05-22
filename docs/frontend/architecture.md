# Architecture

## Feature based folder structure

You can create a folder per functional module, for example:

```js
> modules
    > admin
        > components
        > shared
        > views
    > products
    > cart
    > user
```

Each module folder contains a folder for its components, a shared folder for the helpers, models and services which are not related to an API, and one for the views/pages.<br>
To see the difference a view/page and a component, see <a href="architecture.md?id=components-correctly-divided">Components correctly divided</a>.

If a module is too big with too many pages and components, it can be functionaly subdivided:

```js
> modules
    > user
        > profile
            > components
            > shared
            > views
        > registration
            > components
            > shared
            > views
```

We shouldn't have interactions between the files of different modules, if it's the case, the file (model, component, helper...) needs to be moved to the common folder.

## Components correctly divided
### Pages distinguished from components 

We can conceptually distinguish the pages/views from the components, even if technically they are both components.
The pages are the components being called by the router.<br> 
For example, if you call mywebsite/products, you will tell your router to display the ProductPage component.
The components are the blocks called in the pages.<br>
We can separate the pages from the components by putting them in a pages or views folder and/or prefixing their name with "page" or "view".

```js
> modules
    > products
        > components
            ProductCard.vue
            ProductsList.vue
            ProductDetail.vue
            SimilarProducts.vue
        > views
            ProductsPage.vue
            ProductDetailPage.vue
```

### Components division

Let's see a bad practice with a Products.vue page component: 

```html
<h1>Products</h1>
<div v-for="product in products">
    <div class="product-card">
        <img :src="product.image" />
        <span>{{ product.name }}</span>
        <span>{{ product.price }}</span>
    </div>
</div>
```

The right division is:

ProductsPage.vue
```html
<h1>Products</h1>
<ProductsList :products="products"/>
```

ProductsList.vue
```html
<div v-for="product in products">
    <ProductCard :product="product"/>
</div>
```

ProductCard.vue
```html
<div class="product-card">
    <img :src="product.image" />
    <span>{{ product.name }}</span>
    <span>{{ product.price }}</span>
</div>
```

ProductsPage will retrieve the data from the store and pass it to the ProductsList component, so that the ProductsList component can be reused in another page with another list of products.<br>
The ProductCard component is also provided with a product object so that it can be used anywhere in the project.

Even if the component is functionally isolated, <b>if it gets too big (more than 100 lines of html)</b>, it can be divided in more parts (some forms can get huge for example).

## Common code clearly identified

In order not to have duplicated code or functional modules using the code of other functional modules, we need a common folder subdivided by category of common code:

```js
> common
    > components
    > filters
    > models
    > services
    > styles
    ...
```

Moving a function of component being used by several modules to the common folder is easy to identify and easy to do, but we can also anticipate, even if the component, helper or css class is only used in one module for the moment. Some examples:
- layout components or custom form components, cards components,
- date filters,
- array and dates helper functions,
- css styles common to the app (colors, forms styling, typography, spacing, tables...)

## State management

Any app should have a shared state across the components/pages which is adapted to the size and complexity of the project.
It can be a simple hand-made class if the project is very small and don't interact with an API, or an existing library (ngrx, redux, vuex, pinia...).

It is better if the store is divided by functional sub-stores, just like the functional modules :

```js
> stores
    > admin-store
    > products-store
    > cart-store
    > user-store
```

And just like the components modules, if a store is getting to big, it can be divided into smaller functionnal pieces:

```js
> stores
    > user
        > user-profile-store
        > user-registration-store
```

The API calls are done from the store's actions methods (not from the components directly).
The services doing the API calls can be located inside the store's folder:

```js
> stores
    > products-store
        products-store.ts
        > services
            products.service.ts
```

## Decoupled types
