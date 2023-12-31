# Flex Configuration Updater
This is a simple set of scripts that help deploy Flex configuration settings. Currently it only supports setting `ui_attributes` properties and `taskrouter_skills` within the [Flex UI Configuration](https://www.twilio.com/docs/flex/developer/ui/configuration).  

- `ui_attributes` managed per environment 
- `taskrouter_skills` managed across all environments

The version controlled configuration is merged with the configuration already existing in the environment.


## To deploy to a hosted account from local (not typically neccessary)

_Note_ when running locally `plugin-flex-ts-template-zach-v2/public/appConfig.js` will take precedence over anything deployed

1. Make sure the dependent modules are installed
```bash
npm install
```
2. Create your .env file
```bash
cp .env.example .env
```
3. have a twilio api key and secret for your account
    - follow this [guide](https://www.twilio.com/docs/glossary/what-is-an-api-key#how-can-i-create-api-keys) to setup an API key if you dont have one
4. Add `TWILIO_ACCOUNT_SID` and `TWILIO_API_KEY` and `TWILIO_API_SECRET` values to the `.env` file
5. Review/Edit the `taskrouter_skills.json` and ensure the skills match the ones you want to deploy.  This is used on every environment to deploy a common set of skills.  Note the skills in the file will be merged with any skills existing in the environment.
6. Run `npm run deploy` to update the hosted flex configuration.
  - this will generate a ui_attributes.my_hosted_flex.json, any settings in here will override any in ui_attributes.common.json when deployed to your hosted account
---

## To use with release pipeline

follow the instructions for setting up the release pipeline [here](/README.md#setup-a-project-with-release-pipeline);


# Configuring skills

The `taskrouter_skills.json` file defines skills that should be automatically deployed. The skills in the file will be merged with any skills existing in the environment. By default this is empty. Here is an example of how you can populate this file:

```json
[
    {
        "minimum": null,
        "multivalue": false,
        "name": "billing",
        "maximum": null
    },
    {
      "minimum": null,
      "multivalue": false,
      "name": "support",
      "maximum": null
    },
    {
      "minimum": null,
      "multivalue": false,
      "name": "offline_work",
      "maximum": null
    }
]
```
