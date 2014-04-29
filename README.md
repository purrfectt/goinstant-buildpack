goinstant-buildpack
===================

Heroku buildpack for [GoInstant](https://goinstant.com) applications (served with [Harp](https://github.com/sintaxi/harp)).

### Fork the Example

Why read about it when you can just get to using it? [Fork the example](https://github.com/jeffandersen/goinstant-buildpack-example).

### How it Works

The GoInstant buildpack automatically exposes your `GOINSTANT_CONNECT_URL` environment variable (provided by the GoInstant [Heroku addon](https://addons.heroku.com/goinstant) to your EJS or Jade templates. Simply place your publicly accessible templates/assets in `./public` of your repository, and print out the `GOINSTANT_CONNECT_URL` variable. [Harp](https://github.com/sintaxi/harp) then serves the contents of your repository statically (and handles the template compiling).

### Using with Addon

When creating your heroku application, specify the buildpack option. With this method, the GoInstant addon will be installed for you.

```bash
heroku create your-app-name --buildpack=https://github.com/jeffandersen/goinstant-buildpack
```

Adding it to an existing application is as easy as:

```bash
heroku config:add BUILDPACK_URL=https://github.com/jeffandersen/goinstant-buildpack.git
heroku addons:add goinstant
```

### Using without Addon

When using an existing GoInstant account you must first create your application, then apply the buildpack:

```bash
heroku create your-app-name
heroku config:add BUILDPACK_URL=https://github.com/jeffandersen/goinstant-buildpack.git
```

You must then create a `harp.json` file in your project's root which contains the following structure:

```json
{
  "globals": {
    "GOINSTANT_CONNECT_URL": "https://goinstant.net/account-name/application"
  }
}
```

### Harp Buildpack

Not using GoInstant? This buildpack is based on the [Harp Buildpack by Zeke](https://github.com/zeke/harp-buildpack).
Use that buildpack for serving your static files when you're not using GoInstant as a backend.

### License

MIT
