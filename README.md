# strapi-provider-upload-google-cloud-storage

**Non-Official** Google Cloud Storage Provider for Strapi Upload

## Installation

Install the package from your app root directory

```
cd /path/to/strapi/
npm install strapi-provider-upload-google-cloud-storage --save
```

## Setting up Google authentification

1. In the GCP Console, go to the **Create service account key** page.. 
    - **[Go to the create service account key page](https://console.cloud.google.com/apis/credentials/serviceaccountkey)**
2. From the **Service account** list, select **New service account**.
3. In the **Service account name** field, enter a name.
4. From the **Role** list, select **Storage > Administrator**.   
5. Click **Create**. A JSON file that contains your key downloads to your computer.

## Setting up Strapi upload configuration

1.To enable the provider, create or edit the file at ./extensions/upload/config/settings.json

```json
{
  "provider": "google-cloud-storage",
  "providerOptions": {
    "serviceAccount": "${process.env.GCS_SERVICE_ACCOUNT || 'GCS_SERVICE_ACCOUNT_JSON'}",
    "bucketName": "${process.env.GCS_BUCKET_NAME || 'GCS_BUCKET_NAME'}",
    "bucketLocation": "${process.env.GCS_BUCKET_LOCATION || 'GCS_BUCKET_LOCATION'}",
    "baseUrl": "${process.env.GCS_BASE_URL || 'GCS_BASE_URL'}"
  }
}
```
2. Copy the full content of the downloaded JSON file from GCP
2. Set the json value into the "serviceAccount" field using environment variable or paste the json as string. 
3. Set an existing multi-regional Bucket name into the "bucketLocation" field.
5. Save the configuration
6. Enjoy !

## Optional - Setting up Strapi from environment variable

If you prefer, you can set up the configuration into `config/custom.json` file like this :
```json
{
  "customConfig": "This configuration is accessible through strapi.config.environments.development.myCustomConfiguration",
  "gcs": {
    "serviceAccount": "${process.env.GCS_SERVICE_ACCOUNT || 'GCS_SERVICE_ACCOUNT_JSON'}",
    "bucketName": "${process.env.GCS_BUCKET_NAME || 'GCS_BUCKET_NAME'}",
    "bucketLocation": "${process.env.GCS_BUCKET_LOCATION || 'GCS_BUCKET_LOCATION'}",
    "baseUrl": "${process.env.GCS_BASE_URL || 'GCS_BASE_URL'}"
  }
}
```
You can rename the `environment variables` as you like.

#### Bucket `baseUrl` options :
- https://storage.googleapis.com/{bucket-name}
- https://{bucket-name}
- http://{bucket-name}

## Important information

If the bucket doesn't exist, the plugin will try to create it for you.
So be carefull when you select the multi-regional option, because your bucket will be located inside.

## Resources

* [MIT License](LICENSE.md)

## Links

- [Strapi website](http://strapi.io/)
- [Strapi community on Slack](http://slack.strapi.io)
- [Strapi news on Twitter](https://twitter.com/strapijs)


