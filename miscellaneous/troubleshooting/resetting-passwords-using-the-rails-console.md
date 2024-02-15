# Resetting passwords (using the Rails console)

{% hint style="warning" %}
This page requires some technical knowledge about server administration, and also requires you to have direct access to the server where your Terrastories server is hosted. \
\
If the content of this page feels unfamiliar to you, get someone acquainted with server administration to help you.
{% endhint %}

It may happen that a user is locked out of their community space because they lost their credentials; or, for your Terrastories server, you have lost the password to your super admin account.

Currently, there is no user interface to reset passwords, although we want to make it possible for super admin users to reset the password of a community admin user upon request.

It can be done using the [Rails console](https://guides.rubyonrails.org/command\_line.html), however.

Depending on your hosting environment, the way you access the Rails console may differ:

* On a "Field Kit" or Kakawa Terrastories server, you will need to first get into the `terrastories-web` Docker container's shell, like this:

```
$ docker compose exec web /bin/bash
```

* For online hosting services like Heroku, you can either use a web console or access the server via ssh.

Once you are logged into the Docker container, you can access the rails console from the Terrastories directory:

```
bin/rails console
```

Now, you can update the password for the user (in case of the Terrastories super-user, the username is `terrastories-super`):

```
u = User.find_by(email: email)
u.update!(password: "newpassword", password_confirmation: "newpassword")
```

