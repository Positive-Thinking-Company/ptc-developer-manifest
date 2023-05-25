# Error handling

## Checkpoints
[filename](./errors-handling.checkpoints.md ':include')

## Generic handling of technical errors

All the errors not specifically caught by a try/catch can be handled by the javascript global error handler:

```js
  window.onerror = function (message, source, lineno, colno, error) {
    // manage the error here
  };
```

Framework-specific global error can also be caught. In vuejs for example: 

```js
// error-handler.service.ts:
export const vueConfigErrorHandler = (err, vm, info) => {
  // manage the error here
};

// main.ts
const app = createApp(App);
app.config.errorHandler = vueConfigErrorHandler;

```

It is a choice to display or not those errors to the user.<br>
The most important thing is to log it as it is technical errors that need to be fixed.

## Handling API calls errors

Every API call should be surrounded by a try/catch, in order to display a custom message to the user and to avoid blocking the app.

```js
// loadProducts action of the products store:
  try {
        this.setLoading(true);
        const products = await productsService.getProducts();
        this.products = products;
    } catch (e) {
    MessageService.getInstance().handleError(e, 'errors.loadProducts');
    } finally {
    this.setLoading(false);
    }

```

The MessageService will display a formatted error to the user, using the error message contained in "e" and the corresponding message in the translation file.

```json
  "errors": {
    "loadProducts": "An error occurred while retrieving the list of products.",
    ...

```

## Displaying errors to the user

After being caught and threated, the errors need to be displayed to the user. For example the user needs to know that the form he/she sent has been rejected by the server, and why.

In the MessageService class seen above, a specific action is defined for each kind of server error:

```js
      switch (errorResponse.status) {
        case 401:
          // set the error title as 'you don't have the right to...
          // maybe redirect to login page
          break;
        ...
        case 500:
          // get the error detail message from the http response
          break;
```

Once the error message is created and formatted, it can be sent to a Messages or Notifications store storing an array of error messages.<br>

This array is watched by a notifications common component that will display a snackbar or and error banner each time it detects that a new element has been added to the errors array.