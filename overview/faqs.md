# FAQs

{% hint style="info" %}
For help with technical issues using Terrastories, see the [troubleshooting](../miscellaneous/troubleshooting/ "mention") and [support.md](../miscellaneous/support.md "mention") sections.
{% endhint %}

* [Who made Terrastories? ](faqs.md#who-made-terrastories)
* [Is Terrastories free to use? ](faqs.md#is-terrastories-free-to-use)
* [How do you install Terrastories? ](faqs.md#how-do-you-install-terrastories)
* [What is the difference between Terrastories and story maps? ](faqs.md#what-is-the-difference-between-terrastories-and-story-maps)
* [Is Terrastories a data collection tool? ](faqs.md#is-terrastories-a-data-collection-tool)
* [What kind of data does Terrastories work with? ](faqs.md#is-terrastories-a-data-collection-tool)
* [What languages is Terrastories available in? ](faqs.md#what-languages-is-terrastories-available-in)
* [How does Terrastories work offline? ](faqs.md#how-does-terrastories-work-offline)
* [Who will have access to my data? ](faqs.md#who-will-have-access-to-my-data)
* [Can you help me deploy Terrastories? ](faqs.md#can-you-help-me-deploy-terrastories)
* [How can I report bugs or problems using Terrastories?](faqs.md#how-can-i-report-bugs-or-problems-using-terrastories)

## Who made Terrastories?

Terrastories was built by a volunteer team of open-source stewards and a community of developers, in close collaboration with Indigenous partners and allied NGOs.

Terrastories was conceived in 2018 by geographers from the [Amazon Conservation Team](https://amazonteam.org) when working with the [Matawai](https://amazonteam.org/maps/lands-of-freedom), an Afro-descendant Maroon community in Suriname, and was first built by [Ruby for Good](https://rubyforgood.org), a volunteer collective of Ruby developers. Since then, numerous open-source volunteers have contributed to Terrastories, and several organizations and foundations have made small grants to Terrastories including Tech Matters and the Association for Tribal Archives, Libraries, and Museums (ATALM).

Currently, Terrastories is being stewarded and maintained by Digital Democracy and a team of open-source stewards. Active stewards include Rudo Kemper, Laura Mosher, and Luandro Vieira.

Digital Democracy is a non-profit organization that works in solidarity with marginalized communities to use technology to defend their rights. For more information on Digital Democracy and our partners, visit [our website](https://www.digital-democracy.org).

We would like to acknowledge a past team of stewards who were pivotal to the early success of Terrastories, including: Miranda Wang, Kalimar Maia, Jason Hinebaugh, Ian Norris, and others.

## Is Terrastories free to use?

Yes, Terrastories is free to install and use, and our [license](https://github.com/Terrastories/terrastories/blob/master/LICENSE) permits open modification and distribution.

## How do you install Terrastories?

Terrastories is a web application that you can host online, offline, or on a mesh network. For more information on hosting, please see the **Setting up a Terrastories Server** section (starting with [hosting-environments](../setting-up-a-terrastories-server/hosting-environments/ "mention")).

Digital Democracy also maintains an online Terrastories server at [https://our.terrastories.app](https://our.terrastories.app). If you would like to request a community account on our server, please [write to us](mailto:info@digital-democracy.org).

## What is the difference between Terrastories and story maps?

Today, there are numerous tools that can be used for sharing stories with interactive maps; for example, ArcGIS StoryMaps, Mapbox's Storytelling template, StoryMaps.JS, Leaflet Storymaps, and more.

The biggest difference between Terrastories and these tools is that **Terrastories is built for mapping and maintaining a database of place-based stories, whereas these other tools are more designed for telling stories using an interactive map.**

There are several other key differences between Terrastories and these applications:

1. Terrastories has a content management system (called member dashboard) for easily managing and determining access for mapped content.
2. Terrastories can easily work offline, whereas most of these tools either require internet access or technical expertise for offline setup.
3. Terrastories has a system of granular permissions that can be used to restrict access to sensitive content.

## Is Terrastories a data collection tool?

Terrastories can be better understood as a content management system and a visualization tool than a data collection tool.&#x20;

If you have access to a Terrastories server (online or offline), you _could_ directly enter data about Places, Stories, and Speakers via the Terrastories administrative menu on both mobile devices and desktop computers, but it's worth stressing that there are better and more bespoke tools for this kind of work. It's also not possible to capture audio, video, or images through the Terrastories user interface at this time.&#x20;

We recommend using Terrastories in tandem with another tool for data and story collection and capture. You could use [Mapeo](https://mapeo.app) (or any other mapping tool on the Earth Defenders Toolkit [Toolfinder](https://earthdefenderstoolkit.com/toolfinder)) for mapping places, and any device audio / video recording tool for capturing stories. These can then be entered into Terrastories (either one-by-one or through the Terrastories import feature).

## What kind of data does Terrastories work with?

There are three kinds of data in Terrastories: `stories`, `places`, and `speakers`. Each have a series of fields you may fill in, and you can also attach media attachments specific to each data type. In addition to text fields, `places` also have latitude and longitude fields which are used to place stories on the map.

For more information on Terrastories data, see [exploring-and-creating-stories-speakers-and-places.md](../using-terrastories/using-the-terrastories-member-dashboard/exploring-and-creating-stories-speakers-and-places.md "mention").

## What languages is Terrastories available in?

Currently, Terrastories is available in Amharic, English, Spanish, Hindi, Japanese, Matawai, Dutch, Portuguese, Punjabi, Swahili, and Chinese (Mandarin).

Terrastories can be translated into additional languages on Github. For more information, see [translating-terrastories.md](../miscellaneous/translating-terrastories.md "mention").

## How does Terrastories work offline?

Terrastories is a web application that can be hosted online or offline. The Terrastories codebase comes equipped with everything you need for the application to work offline, including a default offline map tileset if you need it.

When installed for offline usage, Terrastories may be run through the browser much like an online website. It may be accessed at the URL `terrastories.local` (or a custom path if set up). You just need to be connected to the device hotspot (if it is a "Field Kit" setup), or the community mesh network.

## Who will have access to my data?

Terrastories is built so you can control who has access to your data. You can restrict access to your stories by setting them to only be viewable by community members, editors, or admins. For more about this, see [setting-up-users-and-roles.md](../using-terrastories/using-the-terrastories-member-dashboard/setting-up-users-and-roles.md "mention").

You can also set your community to be viewable by the public, or not. If there _is_ a public view, only unrestricted stories are shown, and you can ensure that the background map is different from your community view. For more about this, see [setting-up-a-public-view-for-your-community.md](../using-terrastories/using-the-terrastories-member-dashboard/setting-up-a-public-view-for-your-community.md "mention").

Lastly, the _super admin_ of a Terrastories server does not have access to your data. Through the [navigating-the-super-admin-dashboard.md](../setting-up-a-terrastories-server/navigating-the-super-admin-dashboard.md "mention"), a Terrastories _super admin_ may view some basic metrics about your community like how many stories, places, and speakers have been created, and the last time the community has had some activity; but the data itself is not accessible to the _super admin_.

## Can you help me deploy Terrastories?

There is a community of active users and maintainers of Terrastories that participate in our public #terrastories channel on the [Ruby for Good Slack](https://rubyforgood.slack.com/join/shared\_invite/zt-1kfeimohe-KL\~\~\~6Lkof7G94\_7Ojd\_Hw#/shared-invite/email) and on our [Earth Defenders Toolkit Forum](https://forum.earthdefenderstoolkit.com/). We encourage you to consult these spaces for additional tips and ideas on how people are using Terrastories.

Digital Democracy's core team is very small and we have limited capacity to provide direct accompaniment for implementing Mapeo outside of our existing partnerships. In some cases we are able to offer support. To read more about the way we work with partners and different levels of support, see [here](https://drive.google.com/file/d/1c9C1-6v1EHKnfrYDsBn3VNu5qS\_pUNMC/view?usp=sharing).

## How can I report bugs or problems using Terrastories?

There is community of active users and maintainers of Terrastories that participate in our public chat channel on Slack. To join the conversation or seek help on technical issues, you can the public #terrastories channel on the [Ruby for Good Slack](https://rubyforgood.slack.com/join/shared\_invite/zt-1kfeimohe-KL\~\~\~6Lkof7G94\_7Ojd\_Hw#/shared-invite/email).
