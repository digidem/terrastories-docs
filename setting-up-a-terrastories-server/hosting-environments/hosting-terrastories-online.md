# 🌐 Hosting Terrastories online

{% hint style="warning" %}
This page may require some technical knowledge about server hosting and deployment. If the content of this page feels unfamiliar to you, get someone acquainted with information technology (IT) to help you.
{% endhint %}

_This workflow is for hosting your own Terrastories server online using Heroku and AWS._

To set up your own online Terrastories server, you need to have the following in place:

* **A fork of the Terrastories application on Github** which is what you will deploy as your Terrastories server application.
* **A Mapbox account access key and default map style** to use for new communities that you set up on your server.
* **A cloud storage bucket** to store media content uploaded to Terrastories.
* **A cloud application platform account** to host and run the Terrastories application.\


Currently, Terrastories is set up to work with Amazon AWS S3 cloud storage buckets, and the Heroku web application platform. The following workflow describes how to set up an online Terrastories server using these two services; however, it should be possible to deploy Terrastories using other services as well, but it may require further customizing Terrastories to work with those services. (There is already some scaffolding for using services like Azure in the Terrastories Rails [storage.yml](https://github.com/Terrastories/terrastories/blob/master/rails/config/storage.yml) file)

### 1. Fork the Terrastories repository on Github <a href="#_oudfmiq0in7h" id="_oudfmiq0in7h"></a>

On Github, fork the Terrastories repository master branch at [https://github.com/terrastories/terrastories](https://github.com/terrastories/terrastories) to your own account. This codebase is what will be deployed on your online Terrastories server. You can make any customizations that you want (or create branches), but it is recommended that you keep your fork up-to-date with the Terrastories master codebase.

### 2. Set up a Mapbox account and get access token and a map style URL <a href="#_8m0149ljf3eq" id="_8m0149ljf3eq"></a>

Terrastories uses Mapbox.com as the background map when set up online. You will need an access token associated with your account, as well as a URL to your map style of choice. These will be provided as a default for communities created on your Terrastories server. Once a community has been set up, the community administrator can then change the Mapbox map URL and access token via the Themes settings.

If you haven’t already done so, sign up for a Mapbox account at [https://mapbox.com](https://mapbox.com/) and copy down your access token, along with a map style URL of your choice. You will need these later when setting up Heroku.

### 3. Set up an Amazon AWS S3 bucket <a href="#_pkbmzjxz4c6d" id="_pkbmzjxz4c6d"></a>

On Amazon’s AWS website at [https://aws.amazon.com](https://aws.amazon.com/), sign up for an account and make your way to the Amazon S3 section of the web console. If you are not familiar with Amazon S3, please check out Amazon’s [Getting Started](https://aws.amazon.com/s3/getting-started/) guide.

Create a bucket for storing data in S3. Depending on your use case, the properties here may vary, and you should be careful in ensuring that your bucket is sufficiently secure in your local context. We recommend the following:

* Block _all_ public access (bucket settings)
* Set up an access control policy, or grantee with list/read/write access
* Data encryption

Copy down the following information for your bucket, as you will need it later when setting up Heroku:

* AWS Bucket Region
* AWS Bucket Name
* AWS User Access Key
* AWS User Secret Access Key

AWS Pricing is calculated per the resources used. For Terrastories, this will mainly be storage, and requests & data retrievals. As of early 2022 the [prices ](https://aws.amazon.com/s3/pricing/)are very low, with storage estimated to be $0.023 per GB per month, for buckets under 50 TB. This is the only necessary cost associated with hosting Terrastories online – there are free tiers available for all other services (Mapbox, Heroku).

### 4. Set up a Heroku account <a href="#_v94upnqk8vy3" id="_v94upnqk8vy3"></a>

Navigate to [https://heroku.com](https://heroku.com/) and sign up for an account. As of December 2022, this needs to be a Hobby account ($7/month), or higher to improve your server’s performance and security (SSL).

Create a new app with your name of choice, and optionally add it to a pipeline if you plan to do staging (i.e. with a development and production server).

In the Deploy section, connect the app to Github, and find your forked Terrastories repo to connect.

In the Resources section, add a `Heroku Postgres` add-on. For an experimental online Terrastories servers, the Mini plan ($0.01/month) might be sufficient, or you could upgrade to a Basic plan $9/month). Check the Heroku database pricing guidelines for more information on your needs.

In the Settings section, you need to add some environmental Config Vars. Provision the following:

| Key                         | Value                                                                                                                            |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| ACTIVE\_STORAGE\_SRC        | production                                                                                                                       |
| AWS\_ACCESS\_KEY            | _Add your AWS user access key here._                                                                                             |
| AWS\_BUCKET\_NAME           | _Add your AWS bucket name here._                                                                                                 |
| AWS\_SECRET\_ACCESS\_KEY    | _Add your AWS bucket name here._                                                                                                 |
| AWS\_REGION                 | _Add the region for your AWS bucket name here._                                                                                  |
| DATABASE\_URL               | _This will be provided by setting up the Heroku Postgres add-on._                                                                |
| LANG                        | en\_US.UTF-8                                                                                                                     |
| MAPBOX\_ACCESS\_TOKEN       | _Add your Mapbox access token here_                                                                                              |
| MAPBOX\_STYLE               | _Add your default Mapbox style here._                                                                                            |
| PROJECT\_PATH               | rails                                                                                                                            |
| RACK\_ENV                   | production                                                                                                                       |
| RAILS\_ENV                  | production                                                                                                                       |
| RAILS\_LOG\_TO\_STDOUT      | enabled                                                                                                                          |
| RAILS\_MASTER\_KEY          | 7a0c538b904d5919af7c11470f3b7a4b                                                                                                 |
| RAILS\_SERVE\_STATIC\_FILES | enabled                                                                                                                          |
| SECRET\_KEY\_BASE           | 53316f279e788bae0a2d4f65ec3e213368e216a9ce18757e5305eb854dee98be34dc1f160b6a165832797be1f699a66d4109fd7f719888cbf920e6196fb18500 |

Next, in the Settings section, add the following two buildpacks (in this order):

* `https://github.com/timanovsky/subdir-heroku-buildpack`
* `heroku/ruby`

Optionally, in the Settings section, set up an SSL Certificate and a Custom Domain. This is recommended for any public-facing servers, to ensure that the data will be kept secure, and also to have a URL hosted on your own domain (i.e. something like terrastories.yourwebsite.com).

Lastly, as of March 2022, currently Heroku apps with a `heroku-20` stack are not deploying Terrastories due to our Ruby dependency being out of date. For the time being, you need to downgrade the Heroku stack to `heroku-18` by installing the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) on your system and running the following command: `heroku stack:set heroku-18 -a your-app-name`. However, we hope to have our stack upgraded to work with `heroku-20` by early 2023.

Now you are ready to deploy. In the Deploy section, choose the branch that you want to deploy, either via Automatic Deployment or Manual.

Once you have successfully deployed, one task remains: seeding the database so you can access the Terrastories `super admin` to start creating communities. To do this, click on the More button on the right right and then Run Console. Enter the following command: `rake db:seed`. Once that finishes, your app should be all set up. You can find the URL of your Terrastories server in the Settings section in Heroku.\
****
