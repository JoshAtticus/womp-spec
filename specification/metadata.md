# Metadata
When posting or displaying posts, womp-compatible clients are expected to attach metadata to the posts and parse metadata attached to posts that have them. Metadata is a **required** feature for womp compatibility.

All wasteof posts are HTML, typically in a format like this

```html
<p>Hello, world!</p>
```

womp metadata can be included in the `<p>` element using the `alt` attribute. For example:

```html
<p alt='{"womp": "1.0.0", "clientName": "wo.mbat", "clientVersion": "2.4.1", "enableOpenGraph": true"}'>Hello, world!</p>
```

The `alt` attribute of the first `<p>` element is chosen, as it is never shown to users, even on non-womp-compatible clients, nor is it stripped by the server.

## Schema
|                 | Description                                                                                                                                                         | Type    | Default Value | Available from version | Required? |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|---------------|------------------------|-----------|
| womp            | Indicates womp metadata presence and client's implementation version                                                                                                | String  | 1.0.0         | 1.0.0                  | True      |
| clientName      | User-friendly client name. Maximum 20 characters.                                                                                                                   | String  | N/A           | 1.0.0                  | False     |
| clientVersion   | User-friendly client version. Maximum 10 characters.                                                                                                                | String  | N/A           | 1.0.0                  | False     |
| enableOpenGraph | Enables Open Graph link previews on compatible clients. This value should only be present if your client supports Open Graph link previews.                         | Boolean | true          | 1.0.0                  | False     |
| linkPreviewSize | (If supported by client) determines whether link preview should be "large", "small" or "auto". When "auto", size should be determined by client like it usually is. | String  | auto          | 1.0.0                  | False     |

If an optional part of the schema is not included, your client should assume the default value if applicable. If a required part of the schema is not included, your client should ignore the metadata entirely, as it is invalid.

Please ensure your client **validates** all metadata and requirements, such as character limits.

## Parsing Metadata
When parsing metadata, it's important to note that the wasteof api HTML escapes the content. For example, quotation marks (`""`) may be turned into `&quot;&quot;`

## Editing Posts
When editing posts, you should avoid modifying the existing metadata attached to the post, unless:

- No metadata is present, or;
- The metadata was placed there by a previous version of your client (if clientName AND clientVersion are present)

## Displaying Metadata
If you want, you can **optionally** display the client name (and optionally version) when users click on posts. It's recommended to display this as small, muted text, such as next to a post's timestamp for example.