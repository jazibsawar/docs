---
sidebarDepth: 2
---

# Extensions

Cosmic JS Extensions enable you to customize the Cosmic JS Dashboard experience to create custom experiences in your Bucket Dashboard.
Pre-built Extensions are available for demo and install.

![Screenshot of Cosmic JS dashboard](/docs/screenshots/dashboard-screenshot.jpg)

## Getting started

Go to _Your Bucket > Settings > Extensions_. There are [pre-built Extensions available for install](https://cosmicjs.com/extensions) to extend the functionality of your Bucket. All of the code is open source. You can also build your own Extensions. They are simply [JAMstack](https://jamstack.org/) apps (static web app built using HTML / CSS / JavaScript).

### Adding an extension

1. Go to _Your Bucket > Extensions > Add Extension_
1. You can add either an Extension that points to a URL (https required, X-Frame Options enabled) or upload a zip file that contains a static web app.

## How to add an Extension via URL

You can add an Extension by URL (https required, X-Frame Options enabled), title and icon.

![Screenshot of adding extension by URL](/docs/screenshots/add-extension-url.png)

### Query parameters

After adding your Extension, query parameters are attached to the URL for easy connection to your Bucket. The format looks like this:

```
https://my-custom-webapp.netlify.com?bucket_slug=your-bucket-slug&read_key=your-bucket-read-key&write_key=your-bucket-write-key
```

| Name                 | Description                                                                                                                                                   |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bucket_slug          | Your Bucket slug. Use this to connect to your Cosmic JS Bucket for read / write / edits.                                                                      |
| read_key             | Your Bucket read key. Needed to read from your Bucket if this value is set in your Bucket > Settings > Basic.                                                 |
| write_key            | Your Bucket write key. Needed for writes to your Bucket if this value is set in your Bucket > Settings > Basic.                                               |
| [custom key / value] | You can add unlimited custom query pamaters such as 3rd-party API keys to connect to different services. Find this in your Cosmic JS Extension settings page. |

## How to add a static web app extension

Check out the [Extension Starter](https://github.com/cosmicjs/extension-starter) to see a basic HTML / CSS / JavaScript example.

Add a static web app Extension to your Bucket by uploading a zipped folder that includes at least the following required files:

```
. (Your extension folder)
├── extension.json (Optional)
├── index.html
```

### Extension settings

The `extension.json` file sets information about your Extension. Add an optional [Font Awesome icon](http://fontawesome.io/icons/) to create a custom icon in the side nav. Add an image URL as the thumbnail image next to your Extension. Example:

```json
{
  "title": "Product Manager",
  "font_awesome_class": "fa-tags",
  "image_url": "https://this-is-your-thumbnail-url.xyz"
}
```

### Optional import data

Along with the Extension info, you can import data to the destination Bucket. By adding an `objects` array, you are able to import Objects. By adding an `object_types` array, you are able to import Object Types.

```json
{
  "title": "Product Manager",
  "font_awesome_class": "fa-tags",
  "image_url": "http://this-is-your-thumbnail-url.xyz"
  "objects": [
    {
      "title": "Product 1",
      "slug": "product-1",
      "type_slug": "products",
      "metafields": [
        {
          "title": "Image",
          "key": "image",
          "value": "1234asdf1234.jpg"
        },
        {
          "title": "Price",
          "key": "price",
          "value": "$12.99"
        }
      ]
    },
    {
      "title": "Product 2",
      "slug": "product-2",
      "type_slug": "products",
      "metafields": [
        {
          "title": "Image",
          "key": "image",
          "value": "4321asdf1234.jpg"
        },
        {
          "title": "Price",
          "key": "price",
          "value": "$14.99"
        }
      ]
    }
  ],
  "object_types": [
    {
      "title": "Products",
      "slug": "products",
      "singular": "Product",
      "metafields":[
        {
          "title": "Image",
          "key": "image",
          "type": "file",
          "value": ""
        },
        {
          "title": "Price",
          "key": "price",
          "type": "text",
          "value":""
        }
      ]
    }
  ]
}
```

### Preparing Your Extension for Upload

The static site folder contents:

![Screenshot of how to compress build folder - Part 1](/docs/screenshots/compress-1.png)

Compress the folder:

![Screenshot of how to compress build folder - Part 2](/docs/screenshots/compress-2.png)

Then upload the Extension to your Cosmic JS Bucket located in *Your Bucket > Extensions > Add Extension*.

![Screenshot of add extension](/docs/screenshots/add-extension-zip.png)

## Contribute

Submit your idea to the [Cosmic JS contribution page](https://cosmicjs.com/contribute). We'll showcase your awesome Cosmic JS Extension and you'll get free stuff. 😎

Any questions? Reach out to us on our [Slack channel](https://cosmicjs.com/community) and reach out to us [on Twitter](https://twitter.com/cosmic_js).
