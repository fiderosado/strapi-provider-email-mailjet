# strapi-provider-email-mailjet

[Strapi](http://strapi.io/) email service for [Mailjet](https://mailjet.com/)

# Prerequisites

You will need to have the plugin `strapi-plugin-email` installed in you Strapi project.

# Installation

```
# using yarn
yarn add strapi-provider-email-mailjet

# using npm
npm i strapi-provider-email-mailjet
```

# Configuration

| Variable                     | Type   | Description                                                                                   | Required | Default   |
| ---------------------------- | ------ | --------------------------------------------------------------------------------------------- | -------- | --------- |
| provider                     | string | The name of the provider you use                                                              | yes      |           |
| providerOptions              | object | Provider options                                                                              | yes      |           |
| providerOptions.publicApiKey | string | Mailjet public API key. See your [MailJet API keys](https://app.mailjet.com/account/api_keys) | yes      |           |
| providerOptions.secretApiKey | string | Mailjet secret API key. See your [MailJet API keys](https://app.mailjet.com/account/api_keys) | yes      |           |
| settings                     | object | Settings                                                                                      | no       | {}        |
| settings.defaultFrom         | string | Default sender mail address                                                                   | yes      | undefined |
| settings.defaultFromName     | string | Default sender name                                                                           | yes      | undefined |
| settings.defaultTo           | string | Default receiver mail address                                                                 | yes      | undefined |
| settings.defaultToName       | string | Default receiver name                                                                         | yes      | undefined |

### Example config file

Path - `config/plugins.js`

```javascript
module.exports = ({ env }) => ({
  // ...
  email: {
    provider: "mailjet",
    providerOptions: {
      publicApiKey: env("MAILJET_PUBLIC_KEY"),
      secretApiKey: env("MAILJET_SECRET_KEY"),
    },
    settings: {
      defaultFrom: "scott@ijs.to",
      defaultFromName: "Scott from iJS.to",
      defaultTo: "john.doe@ijs.to",
      defaultToName: "Johnny Bravodoe",
    },
  },
  // ...
});
```

# API

Strapi Mailjet Plugin enables you to interact with Mailjet API via custom methods listed below.

This API is a subset of the [MailJet API](https://dev.mailjet.com/email/reference/).

## Available Methods

You can request additional actions by submitting a Feature Request or a Pull Request.

### Usage example

> Note: To access the custom methods API, you need to call it vai `strapi.plugins.email.provider.CUSTOM_METHOD` and NOT `strapi.plugins.email.services.email.CUSTOM_METHOD`

```javascript
await strapi.plugins.email.provider
  .addContactToList({
    id: "email@example.com",
    listId: "mailingListId",
  })
  .catch((error) => console.log(error))
  .then((response) => console.log(response));
```

### **addContactToList**

| Field  | Type   | Description                          | Required | Default |
| ------ | ------ | ------------------------------------ | -------- | ------- |
| listId | String | MailJet List ID to which add contact | yes      |         |
| id     | String | Contact's email or MailJet ID        | yes      |         |

### **createContact**

| Field | Type   | Description              | Required | Default |
| ----- | ------ | ------------------------ | -------- | ------- |
| email | String | Contact's email          | yes      |         |
| name  | String | Full name of the contact | no       |         |

### **createContactList**

| Field | Type   | Description              | Required | Default |
| ----- | ------ | ------------------------ | -------- | ------- |
| name  | String | Name of the contact list | yes      |         |

### **retrieveContact**

| Field     | Type   | Description                   | Required | Default |
| --------- | ------ | ----------------------------- | -------- | ------- |
| contactId | String | Contact's email or MailJet ID | yes      |         |

---

# Licence

- [MIT](https://github.com/ijsto/strapi-provider-email-mailjet/blob/master/LICENSE.md)

### Credits

Authors:
[Scott Agirs](https://github.com/scottagirs)

Initially published by [sboutet06](https://github.com/sboutet06)
