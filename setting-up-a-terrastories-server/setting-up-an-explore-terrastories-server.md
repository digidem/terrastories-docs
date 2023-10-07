# Setting up an Explore Terrastories server

{% hint style="warning" %}
These pages may require some technical knowledge about server hosting and deployment. If the content of this page feels unfamiliar to you, get someone acquainted with information technology (IT) to help you.
{% endhint %}

The [Broken link](broken-reference "mention") tool is a separate open-source application from the main Terrastories application, and requires a separate server setup. In short, Explore Terrastories queries a Terrastories server API which provides access to any unrestricted stories, which are the stories that may be accessed by a `viewer` role. (See [setting-up-users-and-roles.md](../using-terrastories/using-the-terrastories-member-dashboard/setting-up-users-and-roles.md "mention") for more information on roles and permissions).

### Deployment

You can spin up your own Explore Terrastories server and set it up to work with your own Terrastories server API. The Terrastories server API is protected through a CORS policy, and you have to provide environmental variables in both the Terrastories server AND the Explore Terrastories server in order for your Explore Terrastories application to have permission to access the API. Please see [the Github repository](https://github.com/terrastories/explore-terrastories) for more information.

Explore Terrastories is a [Create React App](https://create-react-app.dev/) and there are instructions for how to set up your own Explore Terrastories server on the above-linked Github repository.&#x20;

Create React App is a widely supported framework and there are detailed [instructions](https://create-react-app.dev/docs/deployment) on how to deploy Create React App on many environments including AWS, Azure, Firebase, Github Pages, Heroku, Netlify, Vercel, and more.

### Enabling access for communities

Once you have an Explore Terrastories server set up, you can enable communities to opt-in to using it by way of adding a `public_communities` feature flag. You can chose to enable it for your entire Terrastories server, a group of communities, or per each individual community.

For more information on how to do this, see[#features-working-with-feature-flags](navigating-the-super-admin-dashboard.md#features-working-with-feature-flags "mention").
