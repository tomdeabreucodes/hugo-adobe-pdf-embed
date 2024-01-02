## About
Hugo theme component providing a shortcode to easily embed PDF documents using Adobe's Embed API.

## Features
The shortcode `adobepdf` embeds a PDF of your choosing into your content.

### Mandatory Parameter
#### url
The URL of the PDF to embed e.g.
```go
{{< adobepdf "https://acrobatservices.adobe.com/view-sdk-demo/PDFs/Bodea%20Brochure.pdf" >}}
```
Or using the named parameter `url`:
```go
{{< adobepdf url="https://acrobatservices.adobe.com/view-sdk-demo/PDFs/Bodea%20Brochure.pdf" >}}
```

### Optional Parameters
#### name
Specify the name of the file which will be displayed at the top of the embed, if not provided, it will default to the url.

#### embedMode
Specify the embed mode. Options:
- `FULL_WINDOW`
- `SIZED_CONTAINER`
- `IN_LINE`
- `LIGHT_BOX`

If none provided, it will default to `IN_LINE`. View the [Adobe docs](https://developer.adobe.com/document-services/docs/overview/pdf-embed-api/howtos/#embed-modes) for more info.

## Installation

1. Add `hugo-adobe-pdf-embed` as a submodule to be able to get upstream changes later `git submodule add https://github.com/tomdeabreucodes/hugo-adobe-pdf-embed.git themes/hugo-adobe-pdf-embed`
2. Add `hugo-adobe-pdf-embed` as the left-most element of the `theme` list variable in your site's or theme's configuration file `config.yaml` or `config.toml`. 
    
    *`config.toml`*
    ```toml
    theme = ["hugo-adobe-pdf-embed", "main-theme"]
    ```
3. Configure your Adobe Embed API credentials in `hugo-adobe-pdf-embed`'s config file

    The Adobe PDF Embed API provides unlimited free access, however you do still need to [create a an api key](https://acrobatservices.adobe.com/dc-integration-creation-app-cdn/main.html?api=pdf-embed-api).

    Once you have your client ID, it will need to be added to your site parameters.

    *./themes/hugo-adobe-pdf-embed/config.toml*
    ```toml
    [params]
        adobeClientId = <Add your API key here>
    ```
    **NOTE:** Please be mindful that this is a private credential, so if you are publishing this config in a public place, take the necessary precautions to conceal it.

4. On one of your content pages, add the shortcode:
    ```go
    {{< adobepdf "https://acrobatservices.adobe.com/view-sdk-demo/PDFs/Bodea%20Brochure.pdf" >}}
    ```
5. Customise with parameters as needed
