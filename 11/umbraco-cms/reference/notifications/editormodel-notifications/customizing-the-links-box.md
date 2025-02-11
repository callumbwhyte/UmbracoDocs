# Customizing the "Links" box

For a content item, Umbraco will show a **Links** box within the **Info** content app. By default, this box will show one or more links to content item.

![image](../../../../../10/umbraco-cms/reference/notifications/editormodel-notifications/images/properties-info-app.png)

With the `SendingContentNotification` event, we can manipulate the links in the `Urls` property. This could be by replace it with custom links although a URL provider would be more suitable:

```
public void Handle(SendingContentNotification notification)
{
    notification.Content.Urls = new[]
    {
        new UrlInfo($"/products/?id={notification.Content.Id}", true, null)
    };
}
```

If the content item has multiple cultures, we can specify the link culture like this:

```
public void Handle(SendingContentNotification notification)
{
    notification.Content.Urls = new[]
    {
        new UrlInfo($"https://mysite.com/products/?id={notification.Content.Id}", true, "en-US"),
        new UrlInfo($"https://mysite.dk/produkter/?id={notification.Content.Id}", true, "da-DK")
    };
}
```

or remove the box entirely by providing an empty list of links:

```
public void Handle(SendingContentNotification notification)
{
    notification.Content.Urls = null;
}
```
