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

#### width
Manually determine the width of the `div` container. Default 100%
#### height
Manually determine the height of the `div` container. Default auto

## Installation

1. Add `hugo-adobe-pdf-embed` as a submodule to be able to get upstream changes later `git submodule add https://github.com/tomdeabreucodes/hugo-adobe-pdf-embed.git themes/hugo-adobe-pdf-embed`
2. Add `hugo-adobe-pdf-embed` as the left-most element of the `theme` list variable in your site's or theme's configuration file `config.yaml` or `config.toml`. 
    
    *`config.toml`*
    ```toml
    theme = ["hugo-adobe-pdf-embed", "main-theme"]
    ```
3. Configure your Adobe Embed API credentials in `hugo-adobe-pdf-embed`'s config file

    The Adobe PDF Embed API provides unlimited free access, however you do still need to [create a an api key](https://acrobatservices.adobe.com/dc-integration-creation-app-cdn/main.html?api=pdf-embed-api).

    Tip: for local testing you can create a separate credential with `localhost` as the domain.
    Once you have your client ID, it will need to be added to your site parameters.

    *./themes/hugo-adobe-pdf-embed/config.toml*
    ```toml
    [params]
        adobeClientId = <Add your API key here>
    ```

4. Update your theme or sites `layout/partials/head.html` file to load the necessary Adobe script. If you prefer to not update the theme one directly, you can copy your theme's `head.html` to your root's `layout/partials` folder and edit it there, as this will be [prioritised in the lookuip order](https://gohugo.io/templates/partials/#partial-template-lookup-order).

    Add the following code between the `<head>` tags:
    ```go
    {{ if .HasShortcode "adobepdf" }}
        {{ partial "adobeloader.html" . }}
    {{ end }}
    ``` 

    The condition means that it will not be loaded unless the shortcode is present.

5. On one of your content pages, add the shortcode:
    ```go
    {{< adobepdf "https://acrobatservices.adobe.com/view-sdk-demo/PDFs/Bodea%20Brochure.pdf" >}}
    ```

6. Customise with parameters as needed
